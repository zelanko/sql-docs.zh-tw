---
title: Python 教學課程：滑雪工具租用
description: 在本教學課程中，您將在 SQL Server 機器學習服務中使用 Python 和線性迴歸來預測滑雪工具租用的數目。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 927816988be8882d4149115f6d4aee38dd3a8f3f
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727042"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Python 教學課程：在 SQL Server 機器學習服務中使用線性迴歸來預測滑雪工具租用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這個教學課程系列中 (總共四個部分)，您將在 [SQL Server 機器學習服務](../what-is-sql-server-machine-learning.md)中使用 Python 和線性迴歸來預測滑雪工具租用的數目。 本教學課程使用 [Azure Data Studio 中的 Python 筆記本](../../azure-data-studio/sql-notebooks.md)，但您也可以使用自己的 Python 整合式開發環境 (IDE)。

假設您擁有滑雪工具租用公司，而且想要預測未來日期的租用次數。 此資訊可協助您準備好庫存、員工和設備。

在此系列課程的第一部分中，您將會設定必要條件。 在第二部分和第三部分中，您將在 Jupyter 筆記本中開發一些 Python 指令碼來準備您的資料，並將機器學習模型定型。 接著在第三部分中，您將使用 T-SQL 預存程式在 SQL Server 內執行這些 Python 指令碼。

在本文中，您將學會如何：

> [!div class="checklist"]
> * 將範例資料庫匯入 SQL Server 

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)，您將了解如何將資料從 SQL Server 載入到 Python 資料框架，並以 Python 準備資料。

在[第三部分](python-ski-rental-linear-regression-train-model.md)中，您將了解如何在 Python 中定型線性迴歸模型。

在[第四部分](python-ski-rental-linear-regression-deploy-model.md)中，您將了解如何將模型儲存至 SQL Server，然後以您在第二部分和第三部分開發的 Python 指令碼建立預存程序。 預存程序將會在 SQL Server 中執行，以根據新資料進行預測。

## <a name="prerequisites"></a>Prerequisites

* SQL Server 機器學習服務 - 如需如何安裝機器學習服務的相關資訊，請參閱 [Windows 安裝指南](../install/sql-machine-learning-services-windows-install.md)或 [Linux 安裝指南](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json)。

* Python IDE - 本教學課程使用 [Azure Data Studio](../../azure-data-studio/what-is.md) 中的 Python 筆記本。 如需詳細資訊，請參閱[如何在 Azure Data Studio 中使用筆記本](../../azure-data-studio/sql-notebooks.md)。 

    您也可以使用自己的 Python IDE，例如 Jupyter 筆記本或 [Visual Studio Code](https://code.visualstudio.com/docs)，搭配 [Python 延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-python.python)和 [mssql 延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)使用。 

* [revoscalepy](../python/ref-py-revoscalepy.md) 套件 - **revoscalepy** 套件包含在 SQL Server 機器學習服務中。 若要在用戶端電腦上使用套件，請參閱[針對 Python 開發設定資料科學用戶端](../python/setup-python-client-tools-sql.md)，以取得在本機安裝此套件的選項。

    如果您在 Azure Data Studio 中使用 Python 筆記本，請遵循下列步驟使用 **revoscalepy**：

    1. 開啟 Azure Data Studio
    1. 從 [檔案]  功能表選取 [喜好設定]  ，再選取 [設定] 
    1. 展開 [延伸模組]  ，並選取 [筆記本設定] 
    1. 在 [Python 路徑]  底下，輸入您安裝程式庫的路徑 (例如，`C:\path-to-python-for-mls`)
    1. 確定已勾選 [使用現有的 Python] 
    1. 重新啟動 Azure Data Studio

    如果您使用的是不同的 Python IDE，請按照您 IDE 的類似步驟。

* SQL 查詢工具 - 本教學課程假設您使用 [Azure Data Studio](../../azure-data-studio/what-is.md)。 您也可以使用 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS)。

* 其他 Python 套件 - 本教學課程系列中範例所使用的 Python 套件您可能已安裝或尚未安裝。 請視需要使用下列 **pip** 命令安裝這些套件。

    ```console
    pip install pandas
    pip install sklearn
    pip install pickle
    ```

## <a name="restore-the-sample-database"></a>還原範例資料庫

本教學課程中使用的範例資料集已儲存到 **.bak** 資料庫備份檔案中，供您下載和使用。

1. 下載 [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak) 檔案。

1. 請遵循在 Azure Data Studio 中[從備份檔案還原資料庫](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)中的指示，使用下列詳細資料：

   * 從您下載的 **TutorialDB** 檔案匯入
   * 將目標資料庫命名為 "TutorialDB"

1. 您可以藉由查詢 **dbo. rental_data** 資料表，確認資料集在還原資料庫之後是否存在：

    ```sql
    USE TutorialDB;
    SELECT * FROM [dbo].[rental_data];
    ```

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第一部分中，您已完成下列步驟：

* 安裝了必要條件
* 將範例資料庫匯入 SQL Server

若要準備 TutorialDB 資料庫中的資料，請遵循本教學課程系列的第二部分：

> [!div class="nextstepaction"]
> [Python 教學課程：準備資料以定型線性迴歸模型](python-ski-rental-linear-regression-prepare-data.md)