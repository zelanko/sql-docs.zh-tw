---
title: SQL Server Python 和 R 教學課程的航班示範資料集
Description: 建立包含來自 R 和 Python 之航空公司資料集的資料庫。 此資料集用於練習, 示範如何將 R 語言或 Python 程式碼包裝在 SQL Server 預存程式中。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b7f28dd4b3e7e6990e037dbd9afe164d8d0e4bec
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714809"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 和 R 教學課程的航班抵達示範資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在此練習中, 請建立 SQL Server 資料庫, 以儲存來自 R 或 Python 內建航空公司示範資料集的匯入資料。 R 和 Python 散發套件提供對等的資料, 您可以使用 Management Studio 將其匯入至 SQL Server 資料庫。

若要完成此練習, 您應該具有[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或可執行 t-SQL 查詢的其他工具。

使用此資料集的教學課程和快速入門包括下列各項:

+  [使用 revoscalepy 建立 Python 模型](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>建立資料庫

1. 啟動 SQL Server Management Studio, 連接到具有 R 或 Python 整合的資料庫引擎實例。  

2. 在物件總管中, 以滑鼠右鍵按一下 [**資料庫**], 然後建立名為**flightdata.csv**的新資料庫。

3. 以滑鼠右鍵按一下**flightdata.csv**,按一下 [工作], 然後按一下 [匯**入**一般檔案]。

4. 開啟 R 或 Python 散發套件中提供的 AirlineDemoData, 視您安裝的語言而定。

   針對 R, 請在 C:\Program Files\Microsoft SQL Server\MSSQL14. 尋找**airlinedemosmall.xdf。** MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   針對 Python, 請在 C:\Program Files\Microsoft SQL Server\MSSQL14. 尋找**airlinedemosmall.xdf。** MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data
  
當您選取檔案時, [資料表名稱] 和 [架構] 會填入預設值。

  ![匯入一般檔案嚮導顯示航空公司示範預設值](media/import-airlinedemosmall.png)

按一下其餘的頁面 (接受預設值) 以匯入資料。


## <a name="query-the-data"></a>查詢資料

執行查詢以確認資料已上傳, 做為驗證步驟。

1. 在物件總管的 [資料庫] 底下, 以滑鼠右鍵按一下 [ **flightdata.csv** ] 資料庫, 然後開始新的查詢。

2. 執行一些簡單的查詢:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>後續步驟

在下列課程中, 您將建立以這項資料為基礎的線性回歸模型。

+ [使用 revoscalepy 建立 Python 模型](use-python-revoscalepy-to-create-model.md)
