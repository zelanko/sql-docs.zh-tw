---
title: "提供來源查詢 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 190c39de92d8fc1b559f43c90c95e446ccc87272
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>提供來源查詢 (SQL Server 匯入和匯出精靈)
如果您指定您想要提供查詢以選取要複製的資料，則 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [提供來源查詢] 。 在此頁面上，您可以撰寫和測試 SQL 查詢，以選取要從資料來源複製到目的地的資料。 您也可以貼上文字的已儲存的查詢，或從檔案載入的查詢文字。

## <a name="screen-shot-of-the-source-query-page"></a>[來源查詢] 頁面的螢幕擷取畫面  
下列螢幕擷取畫面顯示精靈的 [提供來源查詢]  頁面。
 
使用者會在這個簡單的範例中，輸入查詢`SELECT * FROM Sales.Customer`複製所有資料列和所有資料行從**Sales.Customer**來源資料庫中的資料表。
-   `SELECT *`表示複製所有資料行。
-   如果沒有`WHERE`子句表示複製所有資料列。
  
 ![來源查詢 頁面的匯入和匯出精靈](../../integration-services/import-export-data/media/source-query.png "來源查詢 頁面的匯入和匯出精靈")  

## <a name="provide-the-query-and-check-its-syntax"></a>提供查詢並檢查其語法
**SQL 陳述式**  
 輸入要從來源資料庫中擷取特定資料列和資料行的 SELECT 查詢。 您也可以貼上文字的已儲存的查詢，或從檔案載入查詢，依序按一下**瀏覽**。 
  
 例如，下列查詢會擷取**SalesPersonID**， **SalesQuota**，和**SalesYTD**從 AdventureWorks 範例資料庫的銷售人員的佣金百分比已超過 1.5%。  
  
```sql
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  

如需 SELECT 查詢的詳細範例，請參閱 [SELECT 範例 &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md) 或在線上搜尋。  

如果您的資料來源是 Excel，請參閱本主題後文的 [提供 Excel 的來源查詢](#excelQueries) ，了解如何在查詢中指定 Excel 工作表和範圍。
  
 **剖析**  
 檢查您在 [SQL 陳述式]  文字方塊中輸入的 SQL 陳述式語法。  
  
> [!NOTE]
> 如果檢查陳述式語法所需的時間超過逾時值 30 秒，剖析就會停止並引發錯誤。 在剖析成功之前，您將無法移過精靈的這個頁面。 避免逾時的方案為建立以您想使用之查詢為基礎的資料庫檢視，然後從精靈查詢此檢視，而非直接輸入查詢文字。  
  
 **瀏覽**  
 選取已儲存的檔案，其中包含使用 SQL 查詢的文字**開啟** 對話方塊。 選取檔案就會將該檔案的文字複製到 [SQL 陳述式]  文字方塊中。  
 
## <a name="excelQueries"></a> 提供 Excel 的來源查詢
### <a name="specify-excel-objects-in-queries"></a>在查詢中指定的 Excel 物件
有三種您可以查詢的 Excel 物件。
-   **工作表。** 若要查詢工作表，請在工作表名稱結尾加上 $ 字元，並以分隔符號括住字串，例如 **[Sheet1$]**。

    ```
    SELECT * FROM [Sheet1$]
    ```

-   **命名範圍。** 若要查詢命名範圍，請只使用範圍名稱，例如 **MyDataRange**。
    
    ```
    SELECT * FROM MyDataRange
    ```

-   **未命名範圍。** 若要指定尚未命名的儲存格範圍，請在工作表名稱結尾加上 $ 字元、指定範圍，再以分隔符號括住字串，例如 **[Sheet1$A1:B4]**。

    ```
    SELECT * FROM [Sheet1$A1:B4]
    ```

### <a name="prepare-the-excel-source-data"></a>準備 Excel 來源資料
無論是指定工作表或範圍為來源資料表，驅動程式會讀取「連續的」  資料格區塊，從工作表或範圍左上角的第一個非空白資料格開始。 結果就是來源資料中不能有空白的資料列。 例如，資料行標頭和資料列之間不能有空白的資料列。 如果工作表頂端在資料上方有某個標題後面有空白的資料列，您就無法查詢工作表。 在 Excel 中，您必須將名稱指派給資料範圍，並查詢命名範圍而不是工作表。

## <a name="whats-next"></a>下一步  
 在撰寫並測試選取要複製資料的 SQL 查詢之後，下一個頁面會取決於您資料的目的地。  
  
-   下一個頁面上的大部分目的地為 [選取來源資料表和檢視] 。 在此頁面上，您檢閱所提供的查詢，並選擇性地選擇資料行以複製和預覽範例資料。 如需詳細資訊，請參閱 [選取來源資料表和檢視表](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。  
  
-   如果您的目的地為一般檔案，則下一個頁面為 [設定一般檔案目的地] 。 在此頁面上，您可以指定目的地一般檔案的格式化選項。 (在您設定一般檔案之後，下一個頁面是 [選取來源資料表和檢視表])。如需詳細資訊，請參閱[設定一般檔案目的地](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  



