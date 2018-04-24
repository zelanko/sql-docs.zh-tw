---
title: SQL 資料隱碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Injection
ms.assetid: eb507065-ac58-4f18-8601-e5b7f44213ab
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6fc38f900f84abba5f1e5efab47772703f246317
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-injection"></a>SQL 資料隱碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  SQL 插入式攻擊是指將惡意程式碼插入字串中，然後將這些字串傳遞至 SQL Server 的執行個體進行剖析和執行。 建構 SQL 陳述式的任何程序都應該經過檢閱，以確認有無插入弱點，因為 SQL Server 會執行收到的所有語法有效查詢。 即使是參數化資料也可能被技術純熟又執意操作的攻擊者操縱。  
  
## <a name="how-sql-injection-works"></a>SQL 插入如何運作  
 SQL 資料隱碼的主要形式是將程式碼直接插入與 SQL 命令串連並執行的使用者輸入變數。 不直接的攻擊會將惡意程式碼插入用於資料表中儲存目的之字串，或插入做為中繼資料。 當儲存的字串在以後串連成動態 SQL 指令時，就會執行惡意程式碼。  
  
 資料隱碼處理的運作方式是不當地終止文字字串並附加新命令。 因為插入的命令在執行之前可能附加有其他字串，所以不懷好意的人會使用註解標記 "--" 終止插入的字串。 在執行時，後續文字便會被忽略。  
  
 下列指令碼顯示簡單的 SQL 資料隱碼。 此指令碼以使用者輸入的字串將硬式編碼的字串串連在一起，來建立 SQL 查詢：  
  
```  
var Shipcity;  
ShipCity = Request.form ("ShipCity");  
var sql = "select * from OrdersTable where ShipCity = '" + ShipCity + "'";  
```  
  
 系統會提示使用者輸入城市的名稱。 如果該使用者輸入 `Redmond`，則指令碼組合的查詢會如下所示：  
  
```  
SELECT * FROM OrdersTable WHERE ShipCity = 'Redmond'  
```  
  
 不過，假設使用者輸入下列命令：  
  
```  
Redmond'; drop table OrdersTable--  
```  
  
 在此情況下，指令碼會組合下列查詢：  
  
```  
SELECT * FROM OrdersTable WHERE ShipCity = 'Redmond';drop table OrdersTable--'  
```  
  
 分號 (;) 表示結束一項查詢而開始另一項查詢。 而雙連字號 (--) 表示目前這一行的剩餘部分是註解，而且應該被忽略。 如果修改的程式碼語法正確，伺服器就會執行它。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理此陳述式時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會先選取 `OrdersTable` 中的所有記錄，其中 `ShipCity` 是 `Redmond`。 然後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會卸除 `OrdersTable`。  
  
 只要插入的 SQL 程式碼語法正確，就無法以程式設計方式偵測竄改。 因此，您必須驗證所有使用者輸入，並且仔細檢視在您使用的伺服器中執行建構之 SQL 命令的程式碼。 這個主題的下列各節描述編碼的最佳作法。  
  
## <a name="validate-all-input"></a>驗證所有輸入  
 透過測試類型、長度、格式和範圍，始終驗證使用者輸入。 當您針對惡意輸入實作一些預防措施時，請考慮您的應用程式的架構和部署狀況。 請記住，設計用在安全環境中執行的程式也可以複製至不安全的環境。 下列建議應視為最佳作法：  
  
-   對您的應用程式所接收之資料的大小、類型或內容不作任何假設。 例如，您應該做下列評估：  
  
    -   如果錯誤或惡意的使用者在您的應用程式需要郵政編碼的地方，輸入 10 MB 的 MPEG 檔案，則應用程式會如何行為？  
  
    -   如果在文字欄位中內嵌了 `DROP TABLE` 陳述式，則應用程式會執行什麼動作？  
  
-   測試輸入的大小和資料類型，並強制執行適當的限制。 這有助於防止蓄意的緩衝區滿溢。  
  
-   測試字串變數的內容，僅接受預期的值。 拒絕包含二進位資料、逸出序列和註解字元的項目。 這可有助於阻止指令碼資料隱碼，並可防止部分緩衝區滿溢嘗試。  
  
-   使用 XML 文件時，在輸入資料時即驗證所有資料的結構描述。  
  
-   絕不直接在使用者輸入中建立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   使用預存程序來驗證使用者輸入。  
  
-   在多層環境中，所有資料應在進入受信任區域之前進行驗證。 應拒絕未通過驗證處理的資料，且將錯誤傳回至上一層。  
  
-   實作多層驗證。 您針對隨意惡意使用者所採取的預防措施可能對執意操作的攻擊者無效。 較好的作法是在使用者介面中及以後每次跨越信任界限時都進行驗證。   
    例如，用戶端應用程式的資料驗證可阻止簡單的指令碼資料隱碼。 然而，如果下一層假設其輸入已經過驗證，則能繞過用戶端的任何惡意使用者都可以不受限制地存取系統。  
  
-   絕不串連未經驗證的使用者輸入。 字串串連是指令碼資料隱碼的主要進入點。  
  
-   在可用以建構檔案名稱的欄位中，不接受下列字串：AUX、CLOCK$、COM1 到 COM8、CON、CONFIG$、LPT1 到 LPT8、NUL 和 PRN。  
  
 可能的話，請拒絕包含下列字元的輸入。  
  
|輸入字元|Transact-SQL 中的意義|  
|---------------------|------------------------------|  
|**;**|查詢分隔符號。|  
|**'**|字元資料字串分隔符號。|  
|**--**|字元資料字串分隔符號。<br />執行個體時提供 SQL Server 登入。|  
|**/\*** ... **\*/**|註解分隔符號。 伺服器不會評估 **/\*** 和 **\*/** 之間的文字。|  
|**xp_**|用在目錄擴充預存程序名稱的開頭，如 `xp_cmdshell`。|  
  
### <a name="use-type-safe-sql-parameters"></a>使用類型安全的 SQL 參數  
 **中的** Parameters [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 集合會提供類型檢查和長度驗證。 如果您使用 **Parameters** 集合，會將輸入視為常值，而不是可執行的程式碼。 使用 **Parameters** 集合的另一個優點是您可以強制執行類型和長度檢查。 超出範圍的值會觸發例外狀況。 下列程式碼片段會說明如何使用 **Parameters** 集合：  
  
```  
SqlDataAdapter myCommand = new SqlDataAdapter("AuthorLogin", conn);  
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter parm = myCommand.SelectCommand.Parameters.Add("@au_id",  
     SqlDbType.VarChar, 11);  
parm.Value = Login.Text;  
```  
  
 在此範例中，會將 `@au_id` 參數視為常值，而不是可執行的程式碼。 而且，還會檢查此值的類型和長度。 如果 `@au_id` 的值與指定的類型和長度條件約束不一致，則會發生例外狀況。  
  
### <a name="use-parameterized-input-with-stored-procedures"></a>與預存程序搭配使用參數化輸入  
 如果預存程序使用未篩選的輸入，則預存程序很可能會受到 SQL 資料隱碼的攻擊。 例如，下列程式碼易受攻擊：  
  
```  
SqlDataAdapter myCommand =   
new SqlDataAdapter("LoginStoredProcedure '" +   
                               Login.Text + "'", conn);  
```  
  
 如果使用預存程序，您應該使用參數做為其輸入。  
  
### <a name="use-the-parameters-collection-with-dynamic-sql"></a>與動態 SQL 搭配使用 Parameters 集合  
 如果無法使用預存程序，您仍然可以使用參數，如下列程式碼範例所示。  
  
```  
SqlDataAdapter myCommand = new SqlDataAdapter(  
"SELECT au_lname, au_fname FROM Authors WHERE au_id = @au_id", conn);  
SQLParameter parm = myCommand.SelectCommand.Parameters.Add("@au_id",   
                        SqlDbType.VarChar, 11);  
Parm.Value = Login.Text;  
```  
  
### <a name="filtering-input"></a>篩選輸入  
 篩選輸入可移除逸出字元，對於保護 SQL 資料隱碼也很有幫助。 不過，因為大量字元可能會產生問題，所以這不是可靠的防線。 下列範例會搜尋字元字串分隔符號。  
  
```  
private string SafeSqlLiteral(string inputSQL)  
{  
  return inputSQL.Replace("'", "''");  
}  
```  
  
### <a name="like-clauses"></a>LIKE 子句  
 請注意，如果您使用 `LIKE` 子句，萬用字元仍必定逸出：  
  
```  
s = s.Replace("[", "[[]");  
s = s.Replace("%", "[%]");  
s = s.Replace("_", "[_]");  
```  
  
## <a name="reviewing-code-for-sql-injection"></a>檢閱 SQL 資料隱碼的程式碼  
 您應該檢閱所有呼叫 `EXECUTE`、 `EXEC`或 `sp_executesql`的程式碼。 您可以使用類似以下的查詢，來幫助您識別包含這些陳述式的程序。 這個查詢會檢查 `EXECUTE` 或 `EXEC`這些字後面的 1、2、3 或 4 個空格。  
  
```  
SELECT object_Name(id) FROM syscomments  
WHERE UPPER(text) LIKE '%EXECUTE (%'  
OR UPPER(text) LIKE '%EXECUTE  (%'  
OR UPPER(text) LIKE '%EXECUTE   (%'  
OR UPPER(text) LIKE '%EXECUTE    (%'  
OR UPPER(text) LIKE '%EXEC (%'  
OR UPPER(text) LIKE '%EXEC  (%'  
OR UPPER(text) LIKE '%EXEC   (%'  
OR UPPER(text) LIKE '%EXEC    (%'  
OR UPPER(text) LIKE '%SP_EXECUTESQL%';  
```  
  
### <a name="wrapping-parameters-with-quotename-and-replace"></a>用 QUOTENAME() 和 REPLACE() 包裝參數  
 在每一個選取的預存程序中，驗證動態 Transact-SQL 使用的所有變數都已正確處理。 來自預存程序的輸入參數或從資料表中讀取的資料應該用 QUOTENAME() 或 REPLACE() 包裝。 請記住，傳遞到 QUOTENAME() 的 @variable 值屬於 sysname，其最大長度為 128 個字元。  
  
|@variable|建議的包裝函數|  
|---------------|-------------------------|  
|安全性實體的名稱|`QUOTENAME(@variable)`|  
|小於等於 128 個字元的字串|`QUOTENAME(@variable, '''')`|  
|小於 128 個字元的字串|`REPLACE(@variable,'''', '''''')`|  
  
 當您使用這項技術時，SET 陳述式可修改如下：  
  
```  
--Before:  
SET @temp = N'SELECT * FROM authors WHERE au_lname ='''   
 + @au_lname + N'''';  
  
--After:  
SET @temp = N'SELECT * FROM authors WHERE au_lname = '''   
 + REPLACE(@au_lname,'''','''''') + N'''';  
```  
  
### <a name="injection-enabled-by-data-truncation"></a>資料截斷啟用資料隱碼  
 任何指派給變數的動態 [!INCLUDE[tsql](../../includes/tsql-md.md)] 若大於該變數已配置的緩衝區，就會被截斷。 能夠非預期傳遞長字串給預存程序來強制執行陳述式截斷的攻擊者，就可以操作此結果。 例如，由下列指令碼建立的預存程序很容易因為截斷而啟用資料隱碼。  
  
```  
CREATE PROCEDURE sp_MySetPassword  
@loginname sysname,  
@old sysname,  
@new sysname  
AS  
-- Declare variable.  
-- Note that the buffer here is only 200 characters long.   
DECLARE @command varchar(200)  
-- Construct the dynamic Transact-SQL.  
-- In the following statement, we need a total of 154 characters   
-- to set the password of 'sa'.   
-- 26 for UPDATE statement, 16 for WHERE clause, 4 for 'sa', and 2 for  
-- quotation marks surrounded by QUOTENAME(@loginname):  
-- 200 – 26 – 16 – 4 – 2 = 154.  
-- But because @new is declared as a sysname, this variable can only hold  
-- 128 characters.   
-- We can overcome this by passing some single quotation marks in @new.  
SET @command= 'update Users set password='   
    + QUOTENAME(@new, '''') + ' where username='   
    + QUOTENAME(@loginname, '''') + ' AND password = '   
    + QUOTENAME(@old, '''')  
  
-- Execute the command.  
EXEC (@command)  
GO  
```  
  
 將 154 個字元傳遞至 128 個字元的緩衝區之後，攻擊者可以在不知道舊密碼的情況下，設定 sa 的新密碼。  
  
```  
EXEC sp_MySetPassword 'sa', 'dummy',   
'123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012'''''''''''''''''''''''''''''''''''''''''''''''''''   
```  
  
 基於這個原因，您應該對命令變數使用大型緩衝區，或直接在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式內執行動態 `EXECUTE` 。  
  
### <a name="truncation-when-quotenamevariable--and-replace-are-used"></a>使用 QUOTENAME(@variable, '''') 和 REPLACE() 時會截斷  
 如果超過已配置的空間，QUOTENAME() 和 REPLACE() 傳回的字串會自動被截斷。 下列範例所建立的預存程序會顯示可能發生的情況。  
  
```  
CREATE PROCEDURE sp_MySetPassword  
    @loginname sysname,  
    @old sysname,  
    @new sysname  
AS  
  
-- Declare variables.  
    DECLARE @login sysname  
    DECLARE @newpassword sysname  
    DECLARE @oldpassword sysname  
    DECLARE @command varchar(2000)  
  
-- In the following statements, the data stored in temp variables  
-- will be truncated because the buffer size of @login, @oldpassword,  
-- and @newpassword is only 128 characters, but QUOTENAME() can return  
-- up to 258 characters.  
    SET @login = QUOTENAME(@loginname, '''')  
    SET @oldpassword = QUOTENAME(@old, '''')  
    SET @newpassword = QUOTENAME(@new, '''')  
  
-- Construct the dynamic Transact-SQL.  
-- If @new contains 128 characters, then @newpassword will be '123... n  
-- where n is the 127th character.   
-- Because the string returned by QUOTENAME() will be truncated,   
-- it can be made to look like the following statement:  
-- UPDATE Users SET password ='1234. . .[127] WHERE username=' -- other stuff here  
    SET @command = 'UPDATE Users set password = ' + @newpassword   
     + ' where username =' + @login + ' AND password = ' + @oldpassword;  
  
-- Execute the command.  
EXEC (@command);  
GO  
```  
  
 因此，下列陳述式將所有使用者的密碼都設為先前程式碼傳遞的值  
  
```  
EXEC sp_MyProc '--', 'dummy', '12345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678'  
```  
  
 您可以在使用 REPLACE() 時超出已配置的緩衝區來強制執行字串截斷。 下列範例所建立的預存程序會顯示可能發生的情況。  
  
```  
CREATE PROCEDURE sp_MySetPassword  
    @loginname sysname,  
    @old sysname,  
    @new sysname  
AS  
  
-- Declare variables.  
    DECLARE @login sysname  
    DECLARE @newpassword sysname  
    DECLARE @oldpassword sysname  
    DECLARE @command varchar(2000)  
  
-- In the following statements, data will be truncated because   
-- the buffers allocated for @login, @oldpassword and @newpassword   
-- can hold only 128 characters, but QUOTENAME() can return   
-- up to 258 characters.   
    SET @login = REPLACE(@loginname, '''', '''''')  
    SET @oldpassword = REPLACE(@old, '''', '''''')  
    SET @newpassword = REPLACE(@new, '''', '''''')  
  
-- Construct the dynamic Transact-SQL.  
-- If @new contains 128 characters, @newpassword will be '123...n   
-- where n is the 127th character.   
-- Because the string returned by QUOTENAME() will be truncated, it  
-- can be made to look like the following statement:  
-- UPDATE Users SET password='1234…[127] WHERE username=' -- other stuff here   
    SET @command= 'update Users set password = ''' + @newpassword + ''' where username='''   
     + @login + ''' AND password = ''' + @oldpassword + '''';  
  
-- Execute the command.  
EXEC (@command);  
GO  
```  
  
 就像 QUOTENAME() 一樣，也可以藉由宣告大到適合所有情況的暫時變數來避免 REPLACE() 截斷字串。 可能的話，您應該直接在動態 [!INCLUDE[tsql](../../includes/tsql-md.md)]內呼叫 QUOTENAME() 或 REPLACE()。 否則，您可以計算必要的緩衝區大小如下。 若為 `@outbuffer = QUOTENAME(@input)`， `@outbuffer` 的大小應該為 `2*(len(@input)+1)`。 當您使用 `REPLACE()` 和雙引號時 (如上例所示)，大小為 `2*len(@input)` 的緩衝區已足夠。  
  
 下列計算可涵蓋所有情況：  
  
```  
WHILE LEN(@find_string) > 0, required buffer size =  
ROUND(LEN(@input)/LEN(@find_string),0) * LEN(@new_string)   
 + (LEN(@input) % LEN(@find_string))  
```  
  
### <a name="truncation-when-quotenamevariable--is-used"></a>使用 QUOTENAME(@variable, ']') 時會截斷  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性實體的名稱傳遞至使用 `QUOTENAME(@variable, ']')`格式的陳述式時，會發生截斷。 以下範例說明這點。  
  
```  
CREATE PROCEDURE sp_MyProc  
    @schemaname sysname,  
    @tablename sysname,  
AS  
  
-- Declare a variable as sysname. The variable will be 128 characters.  
-- But @objectname actually must allow for 2*258+1 characters.   
DECLARE @objectname sysname  
SET @objectname = QUOTENAME(@schemaname)+'.'+ QUOTENAME(@tablename)   
-- Do some operations.  
GO  
```  
  
 當您串連 sysname 類型的值時，應使用夠大的暫存變數來保留每個值最多 128 個的字元。 可能的話，請直接在動態 `QUOTENAME()` 內呼叫 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 否則，您可以計算必要的緩衝區大小，如上一節所述。  
  
## <a name="see-also"></a>另請參閱  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)   
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)   
 [sp_executesql &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)   
 [保護 SQL Server 的安全](../../relational-databases/security/securing-sql-server.md)  
  
  
