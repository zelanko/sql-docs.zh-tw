---
title: Python 教學課程:Ski 租用 (線性回歸)
description: 在本教學課程中, 您將在 SQL Server Machine Learning 服務中使用 Python 和線性回歸, 以預測 ski 租用的數目。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 718487ba55b2b8db8f16b59df5785cf78ff501f1
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242506"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Python 教學課程:在 SQL Server Machine Learning 服務中使用線性回歸來預測 ski 出租
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這四部分的教學課程系列中, 您將在[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)中使用 Python 和線性回歸, 以預測 ski 租用的數目。 本教學課程使用[Azure Data Studio 中的 python 筆記本](../../azure-data-studio/sql-notebooks.md), 但您也可以使用自己的 python 整合式開發環境 (IDE)。

假設您擁有 ski 出租企業, 而且想要預測未來日期的租用次數。 此資訊可協助您讓您的股票、員工和設施準備就緒。

在此系列的第一個部分中, 您將會設定必要條件。 在第二個和第三部分中, 您將在 Jupyter 筆記本中開發一些 Python 腳本來準備您的資料, 並將機器學習模型定型。 然後, 在第三部分中, 您將使用 T-sql 預存程式在 SQL Server 內執行這些 Python 腳本。

在本文中，您將了解如何：

> [!div class="checklist"]
> * 將範例資料庫匯入 SQL Server 

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)中, 您將瞭解如何將資料從 SQL Server 載入 python 資料框架, 並以 python 準備資料。

在[第三部分](python-ski-rental-linear-regression-train-model.md)中, 您將瞭解如何在 Python 中訓練線性回歸模型。

在[第四部分](python-ski-rental-linear-regression-deploy-model.md)中, 您將瞭解如何將模型儲存至 SQL Server, 然後從您在第二部和第三部分所開發的 Python 腳本中建立預存程式。 預存程式將會在 SQL Server 中執行, 以根據新的資料進行預測。

## <a name="prerequisites"></a>必要條件

* SQL Server Machine Learning 服務-如需如何安裝 Machine Learning 服務的詳細說明, 請參閱[Windows 安裝指南](../install/sql-machine-learning-services-windows-install.md)或《 [Linux 安裝指南》](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json)。

* Python IDE-本教學課程使用[Azure Data Studio](../../azure-data-studio/what-is.md)中的 Python 筆記本。 如需詳細資訊, 請參閱[如何在 Azure Data Studio 中使用筆記本](../../azure-data-studio/sql-notebooks.md)。 

    您也可以使用自己的 Python IDE, 例如 Jupyter 筆記本或具有[python 擴充](https://marketplace.visualstudio.com/items?itemName=ms-python.python)功能和[mssql 擴充](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)功能的[Visual Studio Code](https://code.visualstudio.com/docs) 。 

* [revoscalepy](../python/ref-py-revoscalepy.md)封裝- **revoscalepy**套件包含在 SQL Server Machine Learning 服務中。 若要在用戶端電腦上使用套件, 請參閱針對[Python 開發設定資料科學用戶端](../python/setup-python-client-tools-sql.md), 以取得在本機安裝此套件的選項。

    如果您在 Azure Data Studio 中使用 Python 筆記本, 請遵循下列額外步驟來使用**revoscalepy**:

    1. 開啟 Azure Data Studio
    1. 從 [檔案] 功能表, 依序選取 [**喜好**設定] 和 [**設定**]
    1. 展開 [**擴充**功能], 然後選取 [**筆記本**設定]
    1. 在 [ **Python 路徑**] 下, 輸入您安裝程式庫的路徑 (例如`C:\path-to-python-for-mls`,)
    1. 請確定已核取 [**使用現有的 Python** ]
    1. 重新開機 Azure Data Studio

    如果您使用的是不同的 Python IDE, 請遵循 IDE 的類似步驟。

* SQL 查詢工具-本教學課程假設您使用[Azure Data Studio](../../azure-data-studio/what-is.md)。 您也可以使用[SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS)。

* 其他 Python 套件-本教學課程系列中的範例會使用您可能或尚未安裝的 Python 套件。 如有必要, 請使用下列**pip**命令來安裝這些套件。

    ```console
    pip install pandas
    pip install sklearn
    pip install pickle
    ```

## <a name="restore-the-sample-database"></a>還原範例資料庫

本教學課程中使用的範例資料集已儲存到 **.bak**資料庫備份檔案中, 供您下載和使用。

1. 下載[TutorialDB](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak)檔。

1. 請遵循從 Azure Data Studio 中[的備份檔案還原資料庫](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)中的指示, 使用下列詳細資料:

   * 從您下載的**TutorialDB .bak**檔案匯入
   * 將目標資料庫命名為 "TutorialDB"

1. 藉由查詢**rental_data**資料表來還原資料庫之後, 您可以確認資料集存在:

    ```sql
    USE TutorialDB;
    SELECT * FROM [dbo].[rental_data];
    ```

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第一部分中, 您已完成下列步驟:

* 已安裝必要條件
* 將範例資料庫匯入 SQL Server

若要準備 TutorialDB 資料庫中的資料, 請遵循本教學課程系列的第二部分:

> [!div class="nextstepaction"]
> [Python 教學課程:準備資料以定型線性回歸模型](python-ski-rental-linear-regression-prepare-data.md)