---
title: 教學課程的航班示範資料
Description: 從 R 和 Python 建立包含航空公司資料集的資料庫。 此資料集會用於 SQL Server 機器學習服務的 R 和 Python 教學課程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9bb8d26acb21ff38725c6e993c0b6080a35410f1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74908909"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 和 R 的航班抵達示範資料教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在此練習中，請建立 SQL Server 資料庫，以儲存來自 R 或 Python 內建航空公司示範資料集的匯入資料。 R 和 Python 發佈提供對等的資料，您可以使用 Management Studio 將其匯入 SQL Server 資料庫。

若要完成此練習，您應該具備 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) 或可執行 T-SQL 查詢的其他工具。

使用此資料集的教學課程和快速入門包括下列內容：

+  [使用 revoscalepy 建立 Python 模型](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>建立資料庫

1. 啟動 SQL Server Management Studio，連線到具有 R 或 Python 整合的資料庫引擎執行個體。  

2. 在 [物件總管] 中，以滑鼠右鍵按一下 [資料庫]  ，然後建立名為 **flightdata** 的新資料庫。

3. 以滑鼠右鍵按一下 [flightdata]  ，按一下 [工作]  ，然後按一下 [匯入一般檔案]  。

4. 開啟 R 或 Python 發佈中提供的 AirlineDemoData.csv 檔案，視您安裝的語言而定。

   對於 R，請在 C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData 尋找 **AirlineDemoSmall.csv**
   
   對於 Python，請在 C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data 尋找 **AirlineDemoSmall.csv**
  
當您選取檔案時，[資料表名稱] 和 [結構描述] 會填入預設值。

  ![顯示航空公司示範預設值的匯入一般檔案精靈](media/import-airlinedemosmall.png)

點擊其餘頁面，接受預設值，以匯入資料。


## <a name="query-the-data"></a>查詢資料

執行查詢以確認資料已上傳，作為驗證步驟。

1. 在 [物件總管] 的 [資料庫] 下，以滑鼠右鍵按一下 [flightdata]  資料庫，然後開始新的查詢。

2. 執行一些簡單的查詢：

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>後續步驟

在以下課程中，您將根據此資料建立線性迴歸模型。

+ [使用 revoscalepy 建立 Python 模型](use-python-revoscalepy-to-create-model.md)
