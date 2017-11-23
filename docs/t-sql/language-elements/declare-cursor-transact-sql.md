---
title: "宣告資料指標 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs: TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
caps.latest.revision: "51"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 0641f87c36d3dbed886dc7bb81aa1f179148a8cd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  定義 [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標的屬性，例如其捲動行為以及用來建立資料指標運作所在之結果集的查詢。 DECLARE CURSOR 可接受 ISO 標準語法，以及使用一組 [!INCLUDE[tsql](../../includes/tsql-md.md)] 延伸模組的語法。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ISO Syntax  
DECLARE cursor_name [ INSENSITIVE ] [ SCROLL ] CURSOR   
     FOR select_statement   
     [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]  
[;]  
Transact-SQL Extended Syntax  
DECLARE cursor_name CURSOR [ LOCAL | GLOBAL ]   
     [ FORWARD_ONLY | SCROLL ]   
     [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
     [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
     [ TYPE_WARNING ]   
     FOR select_statement   
     [ FOR UPDATE [ OF column_name [ ,...n ] ] ]  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *cursor_name*  
 名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]定義伺服器資料指標。 *cursor_name*必須符合識別碼的規則。  
  
 INSENSITIVE  
 定義一個資料指標，它會建立資料暫存複本供資料指標本身使用。 從這份暫存資料表中的所有要求資料指標會有所都解答**tempdb**; 因此，修改基底資料表不會反映在提取這個資料指標時，所傳回的資料，而且這個資料指標不允許修改。 使用 ISO 語法時若省略了 INSENSITIVE，則任何使用者對基礎資料表所做的已認可刪除及更新動作，都會反映在後續的提取中。  
  
 SCROLL  
 指定可使用所有提取選項 (FIRST、LAST、PRIOR、NEXT、RELATIVE、ABSOLUTE)。 如果 ISO DECLARE CURSOR 中並未指定 SCROLL，NEXT 就是唯一支援的提取選項。 若您也指定了 FAST_FORWARD 時，便不能指定 SCROLL。  
  
 *select_statement*  
 這是定義資料指標結果集的標準 SELECT 陳述式。 內不允許 FOR BROWSE 和 INTO 關鍵字*select_statement*的資料指標宣告。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]隱含地轉換成另一種類型的資料指標，如果中的子句*select_statement*與要求的資料指標類型的功能發生衝突。  
  
 READ ONLY  
 防止利用這個資料指標進行更新。 UPDATE 或 DELETE 陳述式中的 WHERE CURRENT OF 子句無法參考這個資料指標。 這個選項會覆寫要更新之資料指標的預設功能。  
  
 更新 [OF *column_name* [**，**...*n*]]  
 在資料指標內定義可更新的資料行。 如果的*column_name* [**，**..*.n*] 已指定，只允許修改列出的資料行。 如果指定 UPDATE 時沒有同時指定資料行清單，則可更新所有的資料行。  
  
 *cursor_name*  
 名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]定義伺服器資料指標。 *cursor_name*必須符合識別碼的規則。  
  
 LOCAL  
 指定已建立資料指標的批次、預存程序或觸發程序，其資料指標的範圍為本機範圍。 資料指標名稱只在這個範圍內有效。 批次、預存程序或觸發程序內的區域資料指標變數或是預存程序 OUTPUT 參數可以參考資料指標。 OUTPUT 參數用來將本機資料指標傳回呼叫的批次、預存程序或觸發程序，而可將參數指派到資料指標變數，以便在預存程序中止後參考資料指標。 當批次、預存程序或觸發程序結束時，除非在 OUTPUT 參數中傳回資料指標，否則，會隱含地取消配置資料指標。 如果在 OUTPUT 參數中傳回資料指標，當最後一個參考資料指標的變數取消配置或離開範圍時，便會取消配置資料指標。  
  
 GLOBAL  
 指定連接的資料指標範圍為全域。 連接所執行的任何預存程序或批次內都可以參考資料指標名稱。 只有在中斷連接時，才會隱含地取消配置資料指標。  
  
> [!NOTE]  
>  如果指定不 GLOBAL 或 LOCAL，預設值由設定**to local cursor<**資料庫選項。  
  
 FORWARD_ONLY  
 指定資料指標只能從第一個資料列捲到最後一個資料列。 FETCH NEXT 是唯一支援的提取選項。 如果指定不含 STATIC、KEYSET 或 DYNAMIC 等關鍵字的 FORWARD_ONLY 時，資料指標便會作為 DYNAMIC 資料指標操作。 當 FORWARD_ONLY 和 SCROLL 兩者都沒有指定時，除非指定了 STATIC、KEYSET 或 DYNAMIC 等關鍵字，否則，預設值是 FORWARD_ONLY。 STATIC、KEYSET 和 DYNAMIC 資料指標預設為 SCROLL。 與 ODBC 和 ADO 等資料庫 API 不同的是，STATIC、KEYSET 和 DYNAMIC 等 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料指標支援 FORWARD_ONLY。  
  
 STATIC  
 定義一個資料指標，它會建立資料暫存複本供資料指標本身使用。 從這份暫存資料表中的所有要求資料指標會有所都解答**tempdb**; 因此，修改基底資料表不會反映在提取這個資料指標時，所傳回的資料，而且這個資料指標不允許修改。  
  
 KEYSET  
 指定在開啟資料指標時，修正資料指標中之資料列的成員資格和順序。 唯一識別資料列的索引鍵集內建的資料表中**tempdb**稱為**索引鍵集**。  
  
> [!NOTE]  
>  如果查詢所參考的資料表中至少有一個沒有唯一的索引鍵，則索引鍵集資料指標會轉換為靜態資料指標。  
  
 當資料指標擁有者捲動資料指標時，基底資料表中非索引鍵的變更，不論是資料指標擁有者所進行的變更，或其他使用者所認可的變更，都是可見的。 其他使用者的插入便不可見 (無法利用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標來插入)。 如果資料列遭到刪除，試圖提取這個資料列會傳回 @@FETCH_STATUS -2。 從資料指標之外更新索引鍵值，類似於先刪除舊資料列，再插入新資料列。 具有新值的資料列不可見的且嘗試提取有舊值的資料列會傳回 @@FETCH_STATUS -2。 如果更新是藉由指定 WHERE CURRENT OF 子句透過資料指標完成，便可看到新值。  
  
 DYNAMIC  
 定義在您捲動資料指標時，資料指標能夠反映結果集資料列的所有資料變更。 每次提取時，資料列的資料值、順序和成員資格都有可能改變。 動態資料指標不支援 ABSOLUTE 提取選項。  
  
 FAST_FORWARD  
 指定啟用了效能最佳化的 FORWARD_ONLY、READ_ONLY 資料指標。 如果同時也指定 SCROLL 或 FOR_UPDATE，便不能指定 FAST_FORWARD。  
  
> [!NOTE]  
>  FAST_FORWARD 和 FORWARD_ONLY 都可以在相同的 DECLARE CURSOR 陳述式中使用。  
  
 READ_ONLY  
 防止利用這個資料指標進行更新。 UPDATE 或 DELETE 陳述式中的 WHERE CURRENT OF 子句無法參考這個資料指標。 這個選項會覆寫要更新之資料指標的預設功能。  
  
 SCROLL_LOCKS  
 指定藉由資料指標進行的定位更新或刪除一定會成功。 當資料列讀入資料指標時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會鎖定這些資料列，以確保之後可對它們進行修改。 若您也指定了 FAST_FORWARD 或 STATIC 時，便不能指定 SCROLL_LOCKS。  
  
 OPTIMISTIC  
 指定如果將資料列讀入資料指標之後，又更新了這些資料列，則透過資料指標來進行的定位更新或刪除不會成功。 當資料列讀入資料指標時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會鎖定資料列。 它會改為使用的比較**時間戳記**資料行值或總和檢查碼值，如果資料表沒有**時間戳記**資料行，來判斷讀入資料指標之後，是否修改資料列。 如果修改了資料列，試圖執行的定位更新或刪除便會失敗。 若您也指定了 FAST_FORWARD 時，便不能指定 OPTIMISTIC。  
  
 TYPE_WARNING  
 指定當資料指標從要求的類型隱含地轉換成另一個類型時，便傳送一則警告訊息給用戶端。  
  
 *select_statement*  
 這是定義資料指標結果集的標準 SELECT 陳述式。 中不允許使用 COMPUTE、 COMPUTE BY、 FOR BROWSE 和 INTO 關鍵字*select_statement*的資料指標宣告。  
  
> [!NOTE]  
>  您可以使用查詢提示內的資料指標宣告。不過，如果您同時使用的 FOR UPDATE OF 子句，指定選項 (*query_hint*) FOR UPDATE OF 後面。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]隱含地轉換成另一種類型的資料指標，如果中的子句*select_statement*與要求的資料指標類型的功能發生衝突。 如需詳細資訊，請參閱＜隱含資料指標轉換＞。  
  
 更新 [OF *column_name* [**，**...*n*]]  
 在資料指標內定義可更新的資料行。 如果的*column_name* [**，**... *n* ] 提供，只允許修改列出的資料行。 若指定 UPDATE 時未加上資料行清單，除非指定 READ_ONLY 這個並行選項，否則所有資料行皆可更新。  
  
## <a name="remarks"></a>備註  
 DECLARE CURSOR 定義 [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標的屬性，例如資料指標運作時的捲動行為以及用來建立結果集的查詢。 OPEN 陳述式可擴展結果集，而 FETCH 會從結果集中傳回一個資料列。 CLOSE 陳述式會釋放與資料指標相關聯的目前結果集。 DEALLOCATE 陳述式則會釋放資料指標所使用的資源。  
  
 DECLARE CURSOR 陳述式的第一種格式是使用 ISO 語法來宣告資料指標的行為。 DECLARE CURSOR 的第二種格式是使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 延伸模組，讓您使用與 ODBC 或 ADO 資料庫 API 資料指標功能中相同的資料指標類型來定義資料指標。  
  
 您不能混用這兩種格式。 如果您指定 SCROLL 或不區分大小寫的關鍵字，在 CURSOR 關鍵字之前，您無法使用任何關鍵字，介於資料指標和*select_statement*關鍵字。 如果您指定任何關鍵字，介於資料指標和*select_statement*關鍵字，則不得在 CURSOR 關鍵字之前指定 SCROLL 或 INSENSITIVE。  
  
 如果使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法的 DECLARE CURSOR 中未指定 READ_ONLY、OPTIMISTIC 或 SCROLL_LOCKS，則預設如下：  
  
-   若 SELECT 陳述式不支援更新 (權限不足、存取的遠端資料表不支援更新等等)，則資料指標為 READ_ONLY。  
  
-   STATIC 和 FAST_FORWARD 資料指標的預設值是 READ_ONLY。  
  
-   DYNAMIC 和 KEYSET 資料指標的預設值是 OPTIMISTIC。  
  
 只有其他的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可以參考資料指標名稱。 資料庫 API 函數無法參考這些名稱。 例如，在宣告資料指標後，OLE DB、ODBC 或 ADO 函數或方法都無法參考資料指標名稱。 資料指標資料列不能使用 API 的提取函數或方法提取；只有 [!INCLUDE[tsql](../../includes/tsql-md.md)] FETCH 陳述式可以提取這些資料列。  
  
 在宣告資料指標後，下列系統預存程序即可用來判斷資料指標的特性。  
  
|系統預存程序|Description|  
|------------------------------|-----------------|  
|**sp_cursor_list**|傳回目前連接可見的資料指標清單及其屬性。|  
|**sp_describe_cursor**|描述某個資料指標的屬性，例如，它是一個順向資料指標或捲動資料指標。|  
|**sp_describe_cursor_columns**|描述資料指標結果集中的資料行屬性。|  
|**sp_describe_cursor_tables**|描述資料指標所存取的基底資料表。|  
  
 可以使用變數過程*select_statement*宣告資料指標。 在資料指標宣告之後，資料指標變數值便不會改變。  
  
## <a name="permissions"></a>Permissions  
 若使用者對於資料指標中使用的檢視、資料表及資料行擁有 SELECT 權限，則預設擁有 DECLARE CURSOR 權限。
 
## <a name="limitations-and-restrictions"></a>限制事項

您無法使用具有叢集資料行存放區索引的資料表上的資料指標或觸發程序。 這項限制不適用於非叢集資料行存放區索引。您可以在具有非叢集資料行存放區索引的資料表上使用資料指標和觸發程序。 
  
## <a name="examples"></a>範例  
  
### <a name="a-using-simple-cursor-and-syntax"></a>A. 使用簡單資料指標和語法  

在開啟這個資料指標時所產生的結果集內，包含了資料表的所有資料列及所有資料行。 可以更新這個資料指標，而且所有更新和刪除都會在針對這個資料指標所做的提取中表示。 `FETCH NEXT` 是唯一可用的提取，因為尚未指定 `SCROLL` 選項。  

  
```  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>B. 使用巢狀資料指標產生報表輸出  
 下列範例顯示如何讓資料指標形成巢狀結構，以產生複雜報告。 內部資料指標宣告給每個供應商。  
  
```  
SET NOCOUNT ON;  
  
DECLARE @vendor_id int, @vendor_name nvarchar(50),  
    @message varchar(80), @product nvarchar(50);  
  
PRINT '-------- Vendor Products Report --------';  
  
DECLARE vendor_cursor CURSOR FOR   
SELECT VendorID, Name  
FROM Purchasing.Vendor  
WHERE PreferredVendorStatus = 1  
ORDER BY VendorID;  
  
OPEN vendor_cursor  
  
FETCH NEXT FROM vendor_cursor   
INTO @vendor_id, @vendor_name  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    PRINT ' '  
    SELECT @message = '----- Products From Vendor: ' +   
        @vendor_name  
  
    PRINT @message  
  
    -- Declare an inner cursor based     
    -- on vendor_id from the outer cursor.  
  
    DECLARE product_cursor CURSOR FOR   
    SELECT v.Name  
    FROM Purchasing.ProductVendor pv, Production.Product v  
    WHERE pv.ProductID = v.ProductID AND  
    pv.VendorID = @vendor_id  -- Variable value from the outer cursor  
  
    OPEN product_cursor  
    FETCH NEXT FROM product_cursor INTO @product  
  
    IF @@FETCH_STATUS <> 0   
        PRINT '         <<None>>'       
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
  
        SELECT @message = '         ' + @product  
        PRINT @message  
        FETCH NEXT FROM product_cursor INTO @product  
        END  
  
    CLOSE product_cursor  
    DEALLOCATE product_cursor  
        -- Get the next vendor.  
    FETCH NEXT FROM vendor_cursor   
    INTO @vendor_id, @vendor_name  
END   
CLOSE vendor_cursor;  
DEALLOCATE vendor_cursor;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)   
 [關閉 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [資料指標 &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [解除配置 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [擷取 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
