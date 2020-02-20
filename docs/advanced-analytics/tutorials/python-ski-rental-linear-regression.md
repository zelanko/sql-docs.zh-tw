---
title: Python 教學課程：滑雪工具租用
description: 在這個四部分教學課程系列的第三部分中，您將會以 Python 建置線性迴歸模型，以在 SQL Server 機器學習服務中預測滑雪工具租用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fe8a0c9af06d39ce183677adb86f30d9fc197d67
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75681740"
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

* SQL 查詢工具 - 本教學課程假設您使用 [Azure Data Studio](../../azure-data-studio/what-is.md)。 您也可以使用 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS)。

* 其他 Python 套件 - 此教學課程系列中的範例會使用下列 Python 套件，這些套件預設可能不會安裝：

  * pandas
  * pyodbc
  * sklearn

  若要安裝這些套件：
  1. 在 Azure Data Studio 中，選取 [管理套件]  。
  2. 在 [管理套件]  窗格中，選取 [新增]  索引標籤。
  3. 針對每個下列套件，輸入套件名稱，按一下 [搜尋]  ，然後按一下 [安裝]  。

  或者，您可以開啟 [命令提示字元]  ，變更至您用於 Azure Data Studio 之 Python 版本的安裝路徑 (例如 `cd %LocalAppData%\Programs\Python\Python37-32`)，然後針對每個套件執行 `pip install`。

## <a name="restore-the-sample-database"></a>還原範例資料庫

此教學課程中使用的範例資料庫已儲存為 **.bak** 資料庫備份檔案，以供您下載並使用。

1. 下載 [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak) 檔案。

1. 請遵循在 Azure Data Studio 中[從備份檔案還原資料庫](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)中的指示，使用下列詳細資料：

   * 從您下載的 **TutorialDB** 檔案匯入
   * 將目標資料庫命名為 "TutorialDB"

1. 您可以藉由查詢 **dbo.rental_data** 資料表，確認已還原的資料庫是否存在：

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```

執行下列 SQL 命令來啟用外部指令碼：

  ```sql
  sp_configure 'external scripts enabled', 1;
  RECONFIGURE WITH override;
  ```

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第一部分中，您已完成下列步驟：

* 安裝了必要條件
* 將範例資料庫匯入 SQL Server

若要準備 TutorialDB 資料庫中的資料，請遵循本教學課程系列的第二部分：

> [!div class="nextstepaction"]
> [Python 教學課程：準備資料以定型線性迴歸模型](python-ski-rental-linear-regression-prepare-data.md)