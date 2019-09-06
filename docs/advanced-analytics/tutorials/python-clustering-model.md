---
title: 使用 k--表示叢集分類客戶
description: 在這四部分的教學課程系列中，您將使用具有 SQL Server Machine Learning 服務的 Python，在 SQL database 中使用 K 意指演算法來執行客戶的叢集。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 78a5999bc0c00a72edcc631877fdfed647024bc5
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70294363"
---
# <a name="tutorial-categorizing-customers-using-k-means-clustering-with-sql-server-machine-learning-services"></a>教學課程：使用 k 來分類客戶-表示使用 SQL Server Machine Learning 服務的叢集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這四部分的教學課程系列中，您將使用 Python 在[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)中開發和部署 K 表示叢集模型，以叢集化客戶資料。

在此系列的第一部分中，您將設定本教學課程的必要條件，然後將範例資料集還原至 SQL 資料庫。 稍後在此系列中，您將使用這項資料，以 SQL Server Machine Learning 服務來定型和部署 Python 中的叢集模型。

在此系列的第二部分和其中三個中，您將在 Azure Data Studio 筆記本中開發一些 Python 腳本，以分析和準備您的資料，並將機器學習模型定型。 然後，在第四部分中，您將使用預存程式在 SQL 資料庫內執行這些 Python 腳本。

叢集的說明是將資料組織成群組，而群組的成員在某些方面是相似的。 在此教學課程系列中，假設您擁有零售業務。 您將使用**K 意指**演算法，在產品購買和退貨的資料集中執行客戶的叢集。 藉由叢集化客戶，您可以將目標設為特定群組，以更有效率地專注行銷工作。
K-表示叢集是一個*不受監督學習*演算法，它會根據相似處尋找資料中的模式。

在本文中，您將了解如何：

> [!div class="checklist"]
> * 將範例資料庫還原至 SQL Server 實例

在[第二部分](python-clustering-model-prepare-data.md)中，您將瞭解如何準備 SQL 資料庫中的資料，以執行群集。

在[第三部分](python-clustering-model-build.md)中，您將瞭解如何在 Python 中建立和定型以 K 表示的群集模型。

在[第四部分](python-clustering-model-deploy.md)中，您將瞭解如何在 SQL 資料庫中建立預存程式，以便根據新的資料在 Python 中執行叢集。

## <a name="prerequisites"></a>必要條件

* 使用 Python 語言選項[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)-遵循《 [Windows 安裝指南》](../install/sql-machine-learning-services-windows-install.md)或《 [Linux 安裝指南》](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15)中的安裝指示。

* Python IDE-本教學課程使用[Azure Data Studio](../../azure-data-studio/what-is.md)中的 Python 筆記本。 如需詳細資訊，請參閱[如何在 Azure Data Studio 中使用筆記本](../../azure-data-studio/sql-notebooks.md)。 您也可以使用自己的 Python IDE，例如 Jupyter 筆記本或具有[python 擴充](https://marketplace.visualstudio.com/items?itemName=ms-python.python)功能和[mssql 擴充](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)功能的[Visual Studio Code](https://code.visualstudio.com/docs) 。

* [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)封裝- **revoscalepy**套件包含在 SQL Server Machine Learning 服務中。 若要在用戶端電腦上使用套件，請參閱針對[Python 開發設定資料科學用戶端](../python/setup-python-client-tools-sql.md)，以取得在本機安裝此套件的選項。

  如果您在 Azure Data Studio 中使用 Python 筆記本，請遵循下列額外步驟來使用**revoscalepy**：

  1. 開啟 Azure Data Studio
  1. 從 [**檔案**] 功能表，依序選取 [**喜好**設定] 和 [**設定**]
  1. 展開 [**擴充**功能]，然後選取 [**筆記本**設定]
  1. 在 [ **Python 路徑**] 下，輸入您安裝程式庫的路徑（例如`C:\path-to-python-for-mls`，）
  1. 請確定已核取 [**使用現有的 Python** ]
  1. 重新開機 Azure Data Studio

  如果您使用的是不同的 Python IDE，請遵循 IDE 的類似步驟。

* SQL 查詢工具-本教學課程假設您使用[Azure Data Studio](../../azure-data-studio/what-is.md)。 您也可以使用[SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) （SSMS）。

* 其他 Python 套件-本教學課程系列中的範例會使用您可能或尚未安裝的 Python 套件。 如有必要，請使用下列**pip**命令來安裝這些套件。

  ```console
  pip install matplotlib
  pip install scipy
  pip install sklearn
  ```

## <a name="restore-the-sample-database"></a>還原範例資料庫

本教學課程中使用的範例資料集已儲存到 **.bak**資料庫備份檔案中，供您下載和使用。 此資料集衍生自[交易處理效能委員會（TPC）](http://www.tpc.org/default.asp)所提供的[tpcx-bb](http://www.tpc.org/tpcx-bb/default.asp)資料集。

1. 下載[tpcxbb_1gb](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak)檔。

1. 請遵循從 Azure Data Studio 中[的備份檔案還原資料庫](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)中的指示，使用下列詳細資料：

   * 從您下載的**tpcxbb_1gb .bak**檔案匯入
   * 將目標資料庫命名為 "tpcxbb_1gb"

1. 藉由查詢**dbo. customer**資料表來還原資料庫之後，您可以確認資料集是否存在：

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```

## <a name="clean-up-resources"></a>清除資源

如果您不打算繼續進行本教學課程，請從 SQL Server 刪除 tpcxbb_1gb 資料庫。

## <a name="next-steps"></a>後續步驟

在本教學課程系列的第一部分中，您已完成下列步驟：

* 將範例資料庫還原至 SQL Server 實例

若要準備機器學習模型的資料，請遵循本教學課程系列的第二部分：

> [!div class="nextstepaction"]
> [教學課程：使用 SQL Server Machine Learning 服務準備資料以在 Python 中執行叢集](python-clustering-model-prepare-data.md)
