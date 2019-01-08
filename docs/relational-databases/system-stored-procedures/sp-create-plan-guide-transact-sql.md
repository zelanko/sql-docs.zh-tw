---
title: sp_create_plan_guide & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide
- sp_create_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_plan_guide
ms.assetid: 5a8c8040-4f96-4c74-93ab-15bdefd132f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6900c60b788c30cadd404cc2d687cf7993aa119c
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202564"
---
# <a name="spcreateplanguide-transact-sql"></a>sp_create_plan_guide (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  建立將查詢提示或實際查詢計畫關聯於資料庫中查詢的計畫指南。 如需有關計畫指南的詳細資訊，請參閱 [計畫指南](../../relational-databases/performance/plan-guides.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_create_plan_guide [ @name = ] N'plan_guide_name'  
    , [ @stmt = ] N'statement_text'  
    , [ @type = ] N'{ OBJECT | SQL | TEMPLATE }'  
    , [ @module_or_batch = ]  
      {   
                    N'[ schema_name. ] object_name'  
        | N'batch_text'  
        | NULL  
      }  
    , [ @params = ] { N'@parameter_name data_type [ ,...n ]' | NULL }   
    , [ @hints = ] { N'OPTION ( query_hint [ ,...n ] )'   
                 | N'XML_showplan'  
                 | NULL }  
```  
  
## <a name="arguments"></a>引數  
 [\@名稱 =] N'*plan_guide_name*'  
 計畫指南的名稱。 計畫指南名稱僅限於目前的資料庫。 *plan_guide_name*必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)且開頭不能是數字符號 （#）。 最大長度*plan_guide_name*為 124 個字元。  
  
 [ \@stmt =] N'*sp_create_plan_guide*'  
 這是建立計畫指南所針對的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查詢最佳化工具會辨識符合的查詢*sp_create_plan_guide*， *plan_guide_name*才會生效。 建立計畫指南才會成功， *sp_create_plan_guide*必須出現在所指定的內容\@型別\@module_or_batch，和\@params 參數。  
  
 *sp_create_plan_guide*可讓查詢最佳化工具，以符合與批次中所提供的對應陳述式或模組所識別的方法中必須提供\@module_or_batch 和\@params。 如需詳細資訊，請參閱＜備註＞一節。 大小*sp_create_plan_guide*只受到可用記憶體的伺服器。  
  
 [\@類型 =] N'{物件 |SQL |範本}'  
 是在其中的實體型別*sp_create_plan_guide*隨即出現。 這會指定用於比對的內容*sp_create_plan_guide*要*plan_guide_name*。  
  
 OBJECT  
 指出*sp_create_plan_guide*的內容中會出現[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序、 純量函數、 多重陳述式資料表值函式或[!INCLUDE[tsql](../../includes/tsql-md.md)]目前資料庫中的 DML 觸發程序。  
  
 SQL  
 指出*sp_create_plan_guide*獨立陳述式或批次提交至的內容中會出現[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]透過任何機制。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式提交 common language runtime (CLR) 物件或擴充預存程序，或利用 EXEC N'*sql_string*'、 以批次在伺服器上處理的因此，應該被視為\@類型**=**  'SQL'。 如果有指定 SQL，查詢提示 PARAMETERIZATION {FORCED |中不能指定簡單}\@提示參數。  
  
 TEMPLATE  
 表示計畫指南套用到任何查詢，參數化為中表示的格式*sp_create_plan_guide*。 如果有指定 TEMPLATE，只有 PARAMETERIZATION {FORCED |在您可以指定簡單} 查詢提示\@提示參數。 如需有關 TEMPLATE 計畫指南的詳細資訊，請參閱 <<c0> [ 所使用的計畫指南指定查詢參數化行為](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)。  
  
 [\@module_or_batch =] {N'[ *schema_name*。 ] *object_name*' |N'*batch_text*' |NULL}  
 指定要在其中的物件名稱*sp_create_plan_guide*出現時，或在其中的批次文字*sp_create_plan_guide*隨即出現。 批次文字不能包含 USE*資料庫*陳述式。  
  
 用於計畫指南，以符合應用程式所提交的批次*batch_tex*t 必須提供相同的格式，為字元，如提交給[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 不會執行內部轉換來簡化這個比對作業。 如需詳細資訊，請參閱＜備註＞一節。  
  
 [*schema_name*。]*object_name*指定的名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序、 純量函數、 多重陳述式資料表值函式，或[!INCLUDE[tsql](../../includes/tsql-md.md)]DML 觸發程序，其中包含*sp_create_plan_guide*. 如果*schema_name*未指定，則*schema_name*會使用目前使用者的結構描述。 如果指定了 NULL 並\@類型 = 'SQL'，值\@module_or_batch 設定的值為\@陳述式。如果\@類型 = '範本 **'**， \@module_or_batch 必須為 NULL。  
  
 [ \@params =] {N'*\@parameter_name data_type* [，*.....n* ]' |NULL}  
 指定之所有參數的內嵌在定義*sp_create_plan_guide*。 \@參數適用於只有下列其中一項為 true 時：  
  
-   \@類型 = 'SQL' 或 'TEMPLATE'。 如果 'TEMPLATE'， \@params 不得為 NULL。  
  
-   *sp_create_plan_guide*使用 sp_executesql 和值，來提交\@指定 params 參數，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]內部進行提交之後將它參數化的陳述式。 來自資料庫 API (包括 ODBC、OLE DB 及 ADO.NET) 參數化查詢的提交對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而言，視同對 sp_executesql 或對 API 伺服器資料指標常式的呼叫；因此，也可以由 SQL 或 TEMPLATE 計畫指南進行比對。  
  
 *\@parameter_name data_type*必須完全相同的格式中提交給[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]利用 sp_executesql 或參數化之後內部提交。 如需詳細資訊，請參閱＜備註＞一節。 如果批次不包含參數，就必須指定 NULL。 大小\@params 只受到可用的伺服器記憶體。  
  
 [\@提示 =] {N'OPTION (*query_hint* [，*.....n* ])' |N'*XML_showplan*' |NULL}  
 N'OPTION (*query_hint* [，*.....n* ])  
 指定要附加至符合查詢的 OPTION 子句\@stmt。\@提示語法上必須與 SELECT 陳述式中的 OPTION 子句相同且可以包含任何有效順序的查詢提示。  
  
 N'*XML_showplan*'  
 要套用為提示之 XML 格式的查詢計畫。  
  
 建議將 XML 執行程序表指派給變數；否則，您必須在單引號前加上另一個單引號，以免除執行程序表中的所有單引號。 請參閱範例 E。  
  
 NULL  
 表示在查詢之 OPTION 子句中指定的任何現有提示沒有套用到查詢中。 如需詳細資訊，請參閱 < [OPTION 子句&#40;TRANSACT-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)。  
  
## <a name="remarks"></a>備註  
 sp_create_plan_guide 的引數必須依照顯示順序提供。 當您提供 **sp_create_plan_guide**的參數值時，必須明確指定所有的參數名稱，或是完全不指定。 例如，如果**\@名稱 =** 指定 **\@stmt =** ， **\@類型 =**，依此類推，也必須指定。 同樣地，如果**\@名稱 =** 省略，而且只提供參數值，也必須省略其餘參數名稱，並提供它們的值。 引數名稱僅供描述用途，以協助您了解語法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會驗證指定的參數名稱是否與使用該名稱之位置中的參數名稱相符。  
  
 您可以針對相同的查詢和批次或模組，建立一個以上的 OBJECT 或 SQL 計畫指南。 但是，在任何指定的時間內，只能啟用一個計畫指南。  
  
 無法建立物件的類型的計畫指南\@module_or_batch 值參考預存程序、 函式或指定了 WITH ENCRYPTION 子句或是暫時的 DML 觸發程序。  
  
 試圖卸除或修改計畫指南所參考的函數、預存程序或 DML 觸發程序，不論是已啟用或已停用，都會造成錯誤。 嘗試卸除定義了觸發程序且被計畫指南參考的資料表也會造成錯誤。  
  
> [!NOTE]
>  並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都可使用計劃指南。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。 在任何版本中都可以看到計畫指南。 您也可以將包含計畫指南的資料庫附加到任何版本中。 當您將資料庫還原或附加至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的升級版本時，計畫指南仍維持不變。 您應該在執行伺服器升級後確認每個資料庫中計畫指南的符合度。  
  
## <a name="plan-guide-matching-requirements"></a>計畫指南比對需求  
 是否有指定的計畫指南\@類型 = 'SQL' 或\@類型 = 'TEMPLATE'，若要順利比對的值，查詢*batch_text*並 *\@parameter_name data_type*[，*.....n* ] 必須在其應用程式所提交的對應項目完全相同的格式提供。 這表示您提供的批次文字必須和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 編譯器所收到的完全相同。 若要擷取實際的批次和參數文字，您可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 使用 SQL Server Profiler 建立及測試計畫指南](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)。  
  
 當\@類型 = 'SQL' 和\@module_or_batch 設定為 NULL，值\@module_or_batch 設定的值為\@陳述式。這表示的值*sp_create_plan_guide*中完全相同的格式，必須提供-字元，如提交給[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 不會執行內部轉換來簡化這個比對作業。  
  
 時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的值相符*sp_create_plan_guide*要*batch_text*並 *\@parameter_name data_type* [，*......n* ]，或者如果\@類型 = **'** 物件 '，內之對應查詢的文字*object_name*，則不考量下列字串元素：  
  
-   字串內部的空白字元 (定位字元、空格字元、歸位字元或換行字元)。  
  
-   註解 (**--** 或是**/ \* \* /**)。  
  
-   行尾的分號。  
  
 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可比對*sp_create_plan_guide*字串`N'SELECT * FROM T WHERE a = 10'`下列*batch_text*:  
  
 `N'SELECT *`  
  
 `FROM T`  
  
 `WHERE a=10'`  
  
 不過，相同的字串則不會對應至此*batch_text*:  
  
 `N'SELECT * FROM T WHERE b = 10'`  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會忽略第一項查詢內的歸位字元、換行字元和空白字元。 在第二項查詢中，順序 `WHERE b = 10` 的解譯與 `WHERE a = 10` 不同。 比對作業會區分大小寫以及區分腔調字 (即使資料庫定序不區分大小寫亦然)，關鍵字例外，它不區分大小寫。 比對作業不區分縮寫格式的關鍵字。 例如，關鍵字 `EXECUTE`、`EXEC` 和 `execute` 被視為相同。  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>計畫指南對於計畫快取的影響  
 針對某個模組建立計畫指南時，就會從計畫快取中移除該模組的查詢計畫。 針對某個批次建立 OBJECT 或 SQL 類型的計畫指南時，就會移除具有相同雜湊值之批次的查詢計畫。 建立 TEMPLATE 類型的計畫指南時，就會從該資料庫內部的計畫快取中移除所有單一陳述式批次。  
  
## <a name="permissions"></a>Permissions  
 若要建立類型為 OBJECT 的計畫指南，需要所參考物件的 ALTER 權限。 若要建立類型為 SQL 或 TEMPLATE 的計畫指南，需要目前資料庫的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-plan-guide-of-type-object-for-a-query-in-a-stored-procedure"></a>A. 為預存程序中的查詢建立類型為 OBJECT 的計畫指南  
 下列範例會建立與應用程式型預存程序的內容中執行的查詢相符的計畫指南，並將 `OPTIMIZE FOR` 提示套用至這項查詢。  
  
 以下是預存程序：  
  
```  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t   
        ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country_region;  
END  
GO  
```  
  
 以下是預存程序中查詢所建立的計畫指南：  
  
```  
EXEC sp_create_plan_guide   
    @name =  N'Guide1',  
    @stmt = N'SELECT *  
              FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.Customer AS c   
                 ON h.CustomerID = c.CustomerID  
              INNER JOIN Sales.SalesTerritory AS t   
                 ON c.TerritoryID = t.TerritoryID  
              WHERE t.CountryRegionCode = @Country_region',  
    @type = N'OBJECT',  
    @module_or_batch = N'Sales.GetSalesOrderByCountry',  
    @params = NULL,  
    @hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
### <a name="b-creating-a-plan-guide-of-type-sql-for-a-stand-alone-query"></a>B. 為獨立的查詢建立類型為 SQL 的計畫指南  
 下列範例會建立計畫指南來與使用 sp_executesql 系統預存程序的應用程式所提交批次中的查詢比對。  
  
 批次如下：  
  
```  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 若要防止這項查詢產生平行執行計畫，請建立下列計畫指南：  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT TOP 1 *   
              FROM Sales.SalesOrderHeader   
              ORDER BY OrderDate DESC',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (MAXDOP 1)';  
```  
  
### <a name="c-creating-a-plan-guide-of-type-template-for-the-parameterized-form-of-a-query"></a>C. 為參數化格式的查詢建立類型為 TEMPLATE 的計畫指南  
 下列範例會建立與參數化為特定格式的任何查詢相符的計畫指南，並導引 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以強制執行查詢的參數化作業。 下列兩項查詢在語法上相同，不同的只是兩者的常數值。  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 以下是參數化格式查詢的計畫指南：  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 在前一個範例中， `@stmt` 參數的值是參數化格式的查詢。 取得這個值以便於 sp_create_plan_guide 中使用的唯一可靠方法，是利用 [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) 系統預存程序。 下列指令碼可以用來取得參數化查詢，之後再建立參數化查詢的計畫指南。  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  傳送到 sp_get_query_template 之 `@stmt` 參數中的常數常值，可能會影響針對取代常值的參數所選擇的資料類型。 這會影響計畫指南的比對作業。 您可能需要建立一份以上的計畫指南，來處理不同的參數值範圍。  
  
### <a name="d-creating-a-plan-guide-on-a-query-submitted-by-using-an-api-cursor-request"></a>D. 建立藉由使用 API 資料指標要求來提交查詢的計畫指南  
 計畫指南可以比對從 API 伺服器資料指標常式提交的查詢。 這些常式包括 sp_cursorprepare、sp_cursorprepexec 和 sp_cursoropen。 使用 ADO、OLE DB 和 ODBC API 的應用程式經常會利用 API 伺服器資料指標與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 互動。 透過檢視 RPC:Starting Profiler 追蹤事件，您可以看見 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 追蹤中的 API 伺服器資料指標常式的叫用。  
  
 假設下列資料出現在您想以計畫指南調整之查詢的 RPC:Starting Profiler 追蹤事件中：  
  
```  
DECLARE @p1 int;  
SET @p1=-1;  
DECLARE @p2 int;  
SET @p2=0;  
DECLARE @p5 int;  
SET @p5=4104;  
DECLARE @p6 int;  
SET @p6=8193;  
DECLARE @p7 int;  
SET @p7=0;  
EXEC sp_cursorprepexec @p1 output,@p2 output,N'@P1 varchar(255),@P2 varchar(255)',N'SELECT * FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID WHERE h.OrderDate BETWEEN @P1 AND @P2',@p5 OUTPUT,@p6 OUTPUT,@p7 OUTPUT,'20040101','20050101'  
SELECT @p1, @p2, @p5, @p6, @p7;  
```  
  
 您注意到對 `SELECT` 的呼叫中 `sp_cursorprepexec` 查詢的計畫，是使用合併聯結，但您卻想要使用雜湊聯結。 將利用 `sp_cursorprepexec` 提交的查詢參數化，包括查詢字串和參數字串。 透過使用與對 `sp_cursorprepexec` 呼叫中完全相同的查詢和參數字串 (逐字元顯示)，您可以建立下列計畫指南來變更計畫的選擇。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'APICursorGuide',  
    @stmt = N'SELECT * FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.SalesOrderDetail AS d   
                ON h.SalesOrderID = d.SalesOrderID   
              WHERE h.OrderDate BETWEEN @P1 AND @P2',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = N'@P1 varchar(255),@P2 varchar(255)',  
    @hints = N'OPTION(HASH JOIN)';  
```  
  
 這個應用程式對這項查詢的後續執行，將受到這份計畫指南的影響，且會利用雜湊聯結來處理查詢。  
  
### <a name="e-creating-a-plan-guide-by-obtaining-the-xml-showplan-from-a-cached-plan"></a>E. 從快取計畫取得 XML 執行程序表，以建立計畫指南  
 下列範例會針對簡單的特定 SQL 陳述式建立計畫指南。 直接以 `@hints` 參數指定查詢的 XML 執行程序表，就可以在計畫指南中提供此陳述式所需的查詢計畫。 此範例會先執行 SQL 陳述式以便在計畫快取中產生計畫。 基於此範例的目的，假設產生的計畫為所需的計畫，而且不需要額外調整查詢。 查詢的 XML 執行程序表會透過查詢 `sys.dm_exec_query_stats`、 `sys.dm_exec_sql_text`和 `sys.dm_exec_text_query_plan` 動態管理檢視取得，而且會被指派給 `@xml_showplan` 變數。 然後，系統會將 `@xml_showplan` 變數傳遞到 `sp_create_plan_guide` 參數的 `@hints` 陳述式中。 或者，您可以使用 [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) 預存程序，從計畫快取的查詢計劃中建立計劃指南。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints =@xml_showplan;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [計畫指南](../../relational-databases/performance/plan-guides.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_cached_plans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)   
 [sp_get_query_template &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md)  
  
  
