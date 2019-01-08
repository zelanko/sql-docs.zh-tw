---
title: 如需 SQL Server Python 和 R 教學課程-SQL Server Machine Learning airline 飛行示範資料集
Description: Create a database containing the Airline dataset from R and Python. This dataset is used in exercises showing how to wrap R language or Python code in a SQL Server stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 10d2f013c103dee3de02335ca2acf82d4320b623
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596979"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>航空公司航班抵達示範資料的 SQL Server Python 和 R 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此練習中，建立 SQL Server 資料庫來儲存從 R 或 Python 內建航空公司示範資料集匯入的資料。 R 和 Python 散發套件會提供對等的資料，您可以匯入 SQL Server 資料庫，使用 Management Studio。

若要完成此練習中，您應該具備[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或其他工具，可執行 T-SQL 查詢。

教學課程和快速入門使用此資料集包含下列項目：

+  [建立使用 revoscalepy Python 模型](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>建立資料庫

1. 啟動 SQL Server Management Studio，連接到資料庫引擎執行個體具有 R 或 Python 整合。  

2. 在 [物件總管] 中，以滑鼠右鍵按一下**資料庫**並建立新的資料庫**flightdata**。

3. 以滑鼠右鍵按一下**flightdata**，按一下**工作**，按一下 **匯入一般檔案**。

4. 開啟 AirlineDemoData.csv 所提供的檔案中的 R 或 Python 發佈，在您安裝的語言而定。

   針對 R，尋求**AirlineDemoSmall.csv**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   對於 Python，尋求**AirlineDemoSmall.csv**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Lib\site packages\revoscalepy\data\sample_data
  
當您選取檔案時，預設值會填入資料表名稱和結構描述。

  ![匯入一般檔案精靈 顯示航空公司示範預設值](media/import-airlinedemosmall.png)

按一下 執行其餘的頁面，接受預設值，將資料匯入。


## <a name="query-the-data"></a>查詢資料

驗證步驟中，執行查詢，以確認資料已上傳。

1. 在 [物件總管] 的資料庫，以滑鼠右鍵按一下**flightdata**資料庫，然後開始新的查詢。

2. 執行一些簡單的查詢：

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>後續步驟

在下一課，您將建立線性迴歸模型，根據此資料。

+ [建立使用 revoscalepy Python 模型](use-python-revoscalepy-to-create-model.md)
