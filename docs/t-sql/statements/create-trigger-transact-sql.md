---
title: "建立觸發程序 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE TRIGGER
- TRIGGER
- CREATE_TRIGGER_TSQL
- TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- CREATE TRIGGER statement
- multiple triggers
- deferred name resolution, DML triggers
- DML triggers, creating
- nested triggers
- server-scoped triggers
- DDL triggers, creating
- triggers [SQL Server], creating
- database-scoped triggers [SQL Server]
ms.assetid: edeced03-decd-44c3-8c74-2c02f801d3e7
caps.latest.revision: 140
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 56011e892d5fbc5862f3d7c279bc297c3d0ac04c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-trigger-transact-sql"></a>CREATE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  建立 DML、DDL 或登入觸發程序。 觸發程序是一種在資料庫伺服器發生事件時，會自動執行的特殊預存程序。 當使用者試圖透過資料操作語言 (DML) 事件來修改資料時，便會執行 DML 觸發程序。 DML 事件包括資料表或檢視的 INSERT、UPDATE 或 DELETE 陳述式。 無論資料表的資料列有無受到影響，這些觸發程序皆會在引發有效的事件時引發。 如需詳細資訊，請參閱 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)。  
  
 DDL 觸發程序會根據各種資料定義語言 (DDL) 事件的不同而執行。 這些事件主要是對應到 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE、ALTER 和 DROP 陳述式，以及執行類似 DDL 作業的特定系統預存程序。 登入觸發程序會引發來回應使用者工作階段建立時所引發的 LOGON 事件。 觸發程序可以直接從建立[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式或方法中建立的組件從[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]通用語言執行平台 (CLR) 和上傳到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許針對任何特定陳述式建立多個觸發程序。  
  
> [!IMPORTANT]  
>  觸發程序內的惡意程式碼可能在擴大的權限下執行。 如需如何降低這個威脅的詳細資訊，請參閱[管理觸發程序安全性](../../relational-databases/triggers/manage-trigger-security.md)。  
  
> [!NOTE]  
>  在本主題討論.NET Framework CLR 整合 SQL Server。 CLR 整合不適用於 Azure SQL Database。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
[ WITH APPEND ]  
[ NOT FOR REPLICATION ]   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME <method specifier [ ; ] > }  
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
```  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a 
-- table (DML Trigger on memory-optimized tables)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
AS { sql_statement  [ ; ] [ ,...n ] }  
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE or UPDATE statement (DDL Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { ALL SERVER | DATABASE }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type | event_group } [ ,...n ]  
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Trigger on a LOGON event (Logon Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON    
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
## <a name="syntax"></a>語法  
  
```  
-- Windows Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
  AS { sql_statement  [ ; ] [ ,...n ] [ ; ] > }  
  
<dml_trigger_option> ::=   
        [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Windows Azure SQL Database Syntax  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE, or UPDATE STATISTICS statement (DDL Trigger)   
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type | event_group } [ ,...n ]   
AS { sql_statement  [ ; ] [ ,...n ]  [ ; ] }  
  
<ddl_trigger_option> ::=   
    [ EXECUTE AS Clause ]  
```  
  
## <a name="arguments"></a>引數
或 ALTER  
 **適用於**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1)。 
  
 只有當它已經存在，有條件地改變觸發程序。 
  
 *schema_name*  
 這是 DML 觸發程序所屬的結構描述名稱。 DML 觸發程序只會針對其據以建立的資料表或檢視表的結構描述。 *schema_name*不能指定 DDL 或登入觸發程序。  
  
 *trigger_name*  
 這是觸發程序的名稱。 A *trigger_name*必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)，不同之處在於*trigger_name*不能以 # 開頭或 # #。  
  
 *資料表* | *檢視*  
 這是執行 DML 觸發程序的資料表或檢視，有時稱為觸發程序資料表或觸發程序檢視。 您可以選擇性地指定資料表或檢視的完整名稱。 只有 INSTEAD OF 觸發程序可以參考檢視。 在本機或全域暫存資料表上，不能定義 DML 觸發程序。  
  
 DATABASE  
 將 DDL 觸發程序的範圍套用在目前資料庫上。 如果指定，每當引發觸發程序*event_type*或*event_group*在目前資料庫中發生。  
  
 ALL SERVER  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 將 DDL 或登入觸發程序的範圍套用在目前伺服器上。 如果指定，每當引發觸發程序*event_type*或*event_group*目前伺服器中任何位置發生。  
  
 WITH ENCRYPTION  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 模糊化 CREATE TRIGGER 陳述式的文字。 使用 WITH ENCRYPTION 可防止在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫中發行這個觸發程序。 CLR 觸發程序不能指定 WITH ENCRYPTION。  
  
 EXECUTE AS  
 指定用來執行這個觸發程序的安全性內容。 可讓您控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體要利用哪個使用者帳戶來驗證觸發程序所參考之任何資料庫物件的權限。  
  
 這個選項是必要的記憶體最佳化資料表上的觸發程序。  
  
 如需詳細資訊，請參閱[EXECUTE AS 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
 NATIVE_COMPILATION  
 表示觸發程序原生編譯。  
  
 這個選項是必要的記憶體最佳化資料表上的觸發程序。  
  
 SCHEMABINDING  
 可確保觸發程序所參考的資料表無法卸除或改變。  
  
 這個選項需要在記憶體最佳化資料表上的觸發程序，並不支援傳統的資料表上的觸發程序。  
  
 FOR | AFTER  
 AFTER 指定只在觸發的 SQL 陳述式指定的所有作業都執行成功時，才引發 DML 觸發程序。 所有參考的重疊顯示動作和條件約束檢查也都必須成功之後，才會引發這個觸發程序。  
  
 當指定的關鍵字只有 FOR 時，預設值便是 AFTER。  
  
 檢視不能定義 AFTER 觸發程序。  
  
 INSTEAD OF  
 指定執行 DML 觸發程序*而不是*觸發的 SQL 陳述式，因此，會覆寫觸發陳述式的動作。 DDL 或登入觸發程序不能指定 INSTEAD OF。  
  
 您最多只能在資料表或檢視上，定義每個 INSERT、UPDATE 或 DELETE 陳述式各一個 INSTEAD OF 觸發程序。 不過，您可以定義檢視的檢視，讓每份檢視都有它自己的 INSTEAD OF 觸發程序。  
  
 使用 WITH CHECK OPTION 的可更新檢視上不可使用 INSTEAD OF 觸發程序。 當 INSTEAD OF 觸發程序加入所指定之可更新檢視 WITH CHECK OPTION 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會產生錯誤。 使用者必須在定義 INSTEAD OF 觸發程序之前，利用 ALTER VIEW 來移除這個選項。  
  
 { [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }  
 指定當試圖針對這份資料表或檢視來執行時，會啟動 DML 觸發程序的資料修改陳述式。 至少必須指定一個選項。 您可以在觸發程序定義中，依照任何順序來指定這些選項的任何組合。  
  
 對於 INSTEAD OF 觸發程序而言，含有指定了重疊顯示動作 ON DELETE 的參考關聯性之資料表不能使用 DELETE 選項。 同樣地，含有指定了串聯動作 ON UPDATE 的參考關聯性之資料表也不能使用 UPDATE 選項。  
  
 WITH APPEND  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。  
  
 指定應該加入現有類型的其他觸發程序。 當使用 INSTEAD OF 觸發程序時，或明確指示 AFTER 觸發程序時，便不能使用 WITH APPEND。 只有在為了與舊版相容而指定 FOR，且不含 INSTEAD OF 或 AFTER 時，才能使用 WITH APPEND。 如果指定了 EXTERNAL NAME (也就是說，觸發程序是一個 CLR 觸發程序)，便不能指定 WITH APPEND。  
  
 *event_type*  
 這是在執行之後會引發 DDL 觸發程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語言事件名稱。 有效的事件，DDL 觸發程序會列在[DDL 事件](../../relational-databases/triggers/ddl-events.md)。  
  
 *event_group*  
 這是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語言事件之預設定義群組的名稱。 執行任何之後，DDL 觸發程序都會引發[!INCLUDE[tsql](../../includes/tsql-md.md)]語言事件屬於*event_group*。 有效的事件群組的 DDL 觸發程序所述[DDL 事件群組](../../relational-databases/triggers/ddl-event-groups.md)。  
  
 CREATE TRIGGER 執行完成之後*event_group*也可以當做巨集來將事件類型加入它涵蓋 sys.trigger_events 目錄檢視。  
  
 NOT FOR REPLICATION  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指出當複寫代理程式修改觸發程序所涉及的資料表時，不應執行觸發程序。  
  
 *q*  
 這是觸發程序條件和動作。 觸發程序準則指定一些其他條件來決定所嘗試的 DML、DDL 或登入事件是否引起執行觸發程序動作。  
  
 當嘗試作業時，[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式所指定的觸發程序動作便會生效。  
  
 觸發程序可以包括任意數目和任何種類的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，但有例外。 如需詳細資訊，請參閱＜備註＞。 觸發程序的設計，是為了根據資料修改或定義陳述式來檢查或變更資料；它不應將資料傳回給使用者。 [!INCLUDE[tsql](../../includes/tsql-md.md)]觸發程序中的陳述式通常包括[流程控制語言](~/t-sql/language-elements/control-of-flow.md)。  
  
 DML 觸發程序會使用 deleted 和 inserted 邏輯 (概念) 資料表。 它們的結構類似於定義觸發程序的資料表，也就是使用者動作試圖處理的資料表。 deleted 和 inserted 資料表用來保留使用者動作可能已變更之資料列的舊值或新值。 例如，若要擷取 `deleted` 資料表中的所有值，請使用：  
  
```  
SELECT * FROM deleted;  
```  
  
 如需詳細資訊，請參閱[使用 inserted 及 deleted 資料表](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)。  
  
 DDL 和登入觸發程序擷取觸發的事件資訊使用[EVENTDATA &#40;TRANSACT-SQL &#41;](../../t-sql/functions/eventdata-transact-sql.md)函式。 如需詳細資訊，請參閱[使用 EVENTDATA 函數](../../relational-databases/triggers/use-the-eventdata-function.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可讓更新的**文字**， **ntext**，或**映像**資料表或檢視表的資料行透過 INSTEAD OF 觸發程序。  
  
> [!IMPORTANT]  
>  **ntext**，**文字**，和**映像**的未來版本將移除的資料型別[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些資料類型，並規劃修改目前在使用這些資料類型的應用程式。 請改用 [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)、 [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)和 [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) 。 AFTER 和 INSTEAD OF 觸發程序支援**varchar （max)**， **nvarchar （max)**，和**varbinary （max)** inserted 及 deleted 資料表中的資料。  
  
 記憶體最佳化的資料表上的觸發程序的唯一*q*允許的最上層是 ATOMIC 區塊。 T-SQL ATOMIC 區塊內，允許受限於 T-SQL 原生程序內，允許使用。  
  
 \<called >**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 對於 CLR 觸發程序，指定繫結觸發程序的組件方法。 此方法不可使用任何引數，且必須傳回空值。 *class_name*必須是有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別項且必須是組件中的類別與組件可見性。 如果該類別的名稱符合命名空間規定，利用 '.' 來分隔命名空間的各個部分，您就必須用 [ ] 或 " " 分隔字元來分隔類別名稱。 這個類別不能是巢狀類別。  
  
> [!NOTE]  
>  依預設，會關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行 CLR 程式碼的能力。 您可以建立、 修改和卸除參考 managed 程式碼模組的資料庫物件的執行個體中，將無法執行這些參考，但[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非[clr enabled 選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)啟用利用[sp_設定](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
## <a name="remarks-dml-triggers"></a>註解 DML 觸發程序  
 DML 觸發程序常會用於執行商務規則與資料完整性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 利用 ALTER TABLE 及 CREATE TABLE 陳述式提供宣告式參考完整性 (DRI)。 不過，DRI 並不提供跨資料庫的參考完整性。 參考完整性是指資料表主索引鍵和外部索引鍵之間的關聯性規則。 若要強制執行參考完整性，請在 ALTER TABLE 和 CREATE TABLE 中，使用 PRIMARY KEY 和 FOREIGN KEY 條件約束。 如果觸發程序資料表有條件約束，便會在執行 INSTEAD OF 觸發程序之後，執行 AFTER 觸發程序之前，檢查這些條件約束。 如果違反條件約束，便會回復 INSTEAD OF 觸發程序動作，且不會引發 AFTER 觸發程序。  
  
 您可以利用 sp_settriggerorder 來指定資料表所要執行的第一個和最後一個 AFTER 觸發程序。 一份資料表的每個 INSERT、UPDATE 和 DELETE 作業，都只能指定頭尾各一個 AFTER 觸發程序。 如果同一份資料表有其他 AFTER 觸發程序，便會隨機執行它們。  
  
 如果 ALTER TRIGGER 陳述式變更第一個或最後一個觸發程序，便會卸除修改的觸發程序所設定的第一個或最後一個屬性，順序值必須利用 sp_settriggerorder 來重設。  
  
 只有在觸發的 SQL 陳述式已執行成功之後，才會執行 AFTER 觸發程序。 所謂執行成功，包括與已更新或刪除之物件關聯的所有參考串聯動作和條件約束檢查。 AFTER 觸發程序不會以遞迴方式在相同資料表上引發 INSTEAD OF 觸發程序。  
  
 如果資料表所定義的 INSTEAD OF 觸發程序是針對通常會再引發 INSTEAD OF 觸發程序的資料表來執行陳述式，這個觸發程序並不稱為遞迴運作。 相反地，此時會依照資料表沒有 INSTEAD OF 觸發程序的方式來處理陳述式，且會啟動條件約束作業的鏈結，執行 AFTER 觸發程序。 例如，如果觸發程序定義為資料表的 INSTEAD OF INSERT 觸發程序，且這個觸發程序會在相同的資料表上執行 INSERT 陳述式，INSTEAD OF 觸發程序所執行的 INSERT 陳述式便不會重新呼叫這個觸發程序。 觸發程序所執行的 INSERT 會啟動執行條件約束動作及引發定義給資料表之任何 AFTER INSERT 觸發程序的程序。  
  
 如果檢視所定義的 INSTEAD OF 觸發程序是針對通常會再引發 INSTEAD OF 觸發程序的檢視來執行陳述式，它並不稱為遞迴運作。 相反地，陳述式會解析成針對檢視下的基底資料表來進行的修改。 在這個情況下，檢視定義必須符合可更新之檢視的所有限制。 如需可更新檢視的定義，請參閱[修改資料透過檢視](../../relational-databases/views/modify-data-through-a-view.md)。  
  
 例如，如果觸發程序定義為檢視的 INSTEAD OF UPDATE 觸發程序，且這個觸發程序會執行參考相同檢視的 UPDATE 陳述式，INSTEAD OF 觸發程序所執行的 UPDATE 陳述式便不會重新呼叫這個觸發程序。 觸發程序所執行的 UPDATE 是依照檢視沒有 INSTEAD OF 觸發程序的方式，針對檢視來處理的。 UPDATE 所變更的資料行必須解析成單一基底資料表。 基礎基底資料表的每項修改都會啟動套用條件約束及引發定義給資料表之 AFTER 觸發程序的鏈結。  
  
### <a name="testing-for-update-or-insert-actions-to-specific-columns"></a>測試特定資料行的 UPDATE 或 INSERT 動作  
 您可以設計一個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 觸發程序來執行以特定資料行之 UPDATE 或 INSERT 修改為基礎的特定動作。 使用[update （)](../../t-sql/functions/update-trigger-functions-transact-sql.md)或[COLUMNS_UPDATED](../../t-sql/functions/columns-updated-transact-sql.md)針對此用途的觸發程序主體中。 UPDATE() 會測試單一資料行所嘗試的 UPDATE 或 INSERT。 COLUMNS_UPDATED 會測試多個資料行所執行的 UPDATE 或 INSERT 動作，且會傳回一個位元模式來指出插入或更新了哪些資料行。  
  
### <a name="trigger-limitations"></a>觸發程序限制  
 CREATE TRIGGER 必須是批次中的第一個陳述式，且只能套用至一份資料表。  
  
 觸發程序只會建立在目前資料庫中；不過，觸發程序可以參考在目前資料庫之外的物件。  
  
 如果指定觸發程序結構描述名稱來限定觸發程序，請依照相同方式來限定資料表名稱。  
  
 您可以在相同 CREATE TRIGGER 陳述式中，定義多個使用者動作 (如 INSERT 和 UPDATE) 的相同觸發程序動作。  
  
 您不能在外部索引鍵定義了 DELETE/UPDATE 動作串聯的資料表上，定義 INSTEAD OF DELETE/UPDATE 觸發程序。  
  
 您可以在觸發程序內指定任何 SET 陳述式。 在觸發程序的執行期間，所選取的 SET 選項會持續有效，之後，會還原為先前的設定。  
  
 當引發觸發程序時，如同預存程序一樣，結果會傳回發出呼叫的應用程式。 若要防止結果因為引發觸發程序而傳回應用程式，請勿併入會傳回結果的 SELECT 陳述式或是會在觸發程序中執行變數指派的陳述式。 包括將結果傳回給使用者的 SELECT 陳述式或執行變數指派的陳述式之觸發程序，需要特殊處理；這些傳回的結果必須寫入允許修改觸發程序資料表的每個應用程式中。 如果必須在觸發程序內發生變數指派，請在觸發程序開頭使用 SET NOCOUNT 陳述式，以防止傳回任何結果集。  
  
 雖然 TRUNCATE TABLE 陳述式實際上是 DELETE 陳述式，但是它並不會啟動觸發程序，因為此作業不會記錄個別的資料列刪除。 但是，只有具有執行 TRUNCATE TABLE 陳述式之權限的使用者才需要擔心這種方式會不小心阻止 DELETE 觸發程序。  
  
 WRITETEXT 陳述式，不論有沒有記錄，都不會啟動觸發程序。  
  
 DML 觸發程序中不可使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
||||  
|-|-|-|  
|ALTER DATABASE|CREATE DATABASE|DROP DATABASE|  
|RESTORE DATABASE|RESTORE LOG|RECONFIGURE|  
  
 除此之外，當 DML 觸發程序用於觸發動作的目標資料表或檢視表時，不可在 DML 觸發程序的主體內使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
||||  
|-|-|-|  
|CREATE INDEX (包括 CREATE SPATIAL INDEX 和 CREATE XML INDEX)|ALTER INDEX|DROP INDEX|  
|DBCC DBREINDEX|ALTER PARTITION FUNCTION|DROP TABLE|  
|用來執行下列動作的 ALTER TABLE：<br /><br /> 新增、修改或卸除資料行。<br /><br /> 切換資料分割。<br /><br /> 加入或卸除 PRIMARY KEY 或 UNIQUE 條件約束。|||  
  
> [!NOTE]  
>  由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援系統資料表的使用者自訂觸發程序，因此，我們建議您不要在系統資料表上建立使用者自訂觸發程序。  
  
## <a name="remarks-ddl-triggers"></a>註解 DDL 觸發程序  
 如同標準觸發程序，DDL 觸發程序也會執行預存程序來回應事件。 但它們不像標準觸發程序，並不會為了回應資料表或檢視的 UPDATE、INSERT 或 DELETE 陳述式而執行。 相反地，執行它們主要是為了回應資料定義語言 (DDL) 陳述式。 其中包括 CREATE、ALTER、DROP、GRANT、DENY、REVOKE 和 UPDATE STATISTICS 陳述式。 執行類似 DDL 作業的某些系統預存程序也可能引發 DDL 觸發程序。  
  
> [!IMPORTANT]  
>  請測試 DDL 觸發程序，以判斷它們對執行之系統預存程序的回應。 例如，CREATE TYPE 陳述式與 sp_addtype 及 sp_rename 預存程序都會引發在 CREATE_TYPE 事件上建立的 DDL 觸發程序。  
  
 如需有關 DDL 觸發程序的詳細資訊，請參閱[DDL 觸發程序](../../relational-databases/triggers/ddl-triggers.md)。  
  
 對於影響區域或全域暫存資料表與預存程序的事件，DDL 觸發程序不會為了回應它而引發。  
  
 DDL 觸發程序不像 DML 觸發程序，並不以結構描述為範圍。 因此，OBJECT_ID、OBJECT_NAME、OBJECTPROPERTY 和 OBJECTPROPERTYEX 等函數無法用來查詢有關 DDL 觸發程序的中繼資料。 請改用目錄檢視。 如需詳細資訊，請參閱[取得資訊有關 DDL 觸發程序](../../relational-databases/triggers/get-information-about-ddl-triggers.md)。  
  
> [!NOTE]  
>  伺服器範圍的 DDL 觸發程序會出現在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]物件總管 中**觸發程序**資料夾。 這個資料夾在 **[伺服器物件]** 資料夾之下。 資料庫範圍的 DDL 觸發程序會出現在**資料庫觸發程序**資料夾。 這個資料夾在對應資料庫的 **[可程式性]** 資料夾之下。  
  
## <a name="logon-triggers"></a>登入觸發程序  
 登入觸發程序會執行預存程序來回應 LOGON 事件。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體建立使用者工作階段時，就會引發這個事件。 登入觸發程序會在登入驗證階段結束之後，但在使用者工作階段實際建立之前引發。 因此，從觸發程序內產生且一般會顯示給使用者的所有訊息，例如錯誤訊息和來自 PRINT 陳述式的訊息，都會轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。 如需詳細資訊，請參閱[登入觸發程序](../../relational-databases/triggers/logon-triggers.md)。  
  
 如果驗證失敗，登入觸發程序就不會引發。  
  
 登入觸發程序不支援分散式交易。 若引發含有分散式交易的登入觸發程序，會傳回錯誤 3969。  
  
### <a name="disabling-a-logon-trigger"></a>停用登入觸發程序  
 登入觸發程序可以有效地防止所有使用者成功連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，包括 **sysadmin** 固定伺服器角色的成員。 當登入觸發程序防止連接時， **sysadmin** 固定伺服器角色的成員可以使用專用管理員連接或以最低組態模式 (-f) 啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，藉以進行連接。 如需詳細資訊，請參閱 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
## <a name="general-trigger-considerations"></a>一般觸發程序考量  
  
### <a name="returning-results"></a>傳回結果  
 SQL Server 的未來版本將移除從觸發程序傳回結果的功能。 傳回結果集的觸發程序可能會導致非專用的應用程式發生非預期的行為。 請在新的開發工作中避免從觸發程序傳回結果集，並計畫修改目前如此運作的應用程式。 若要避免觸發程序傳回結果集，將[disallow results from triggers 選項](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md)設為 1。  
  
 登入觸發程序不允許傳回結果集，而且您無法設定這項行為。 如果登入觸發程序產生結果集，此觸發程序將無法執行，而引發觸發程序的登入嘗試將被拒絕。  
  
### <a name="multiple-triggers"></a>多重觸發程序  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許每個 DML、DDL 或 LOGON 事件各建立多個觸發程序。 例如，如果針對已有 UPDATE 觸發程序的資料表來執行 CREATE TRIGGER FOR UPDATE，便會建立其他更新觸發程序。 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，每份資料表的每個 INSERT、UPDATE 或 DELETE 資料修改事件都只能有一個觸發程序。  
  
### <a name="recursive-triggers"></a>遞迴觸發程序  
 當利用 ALTER DATABASE 來啟用 RECURSIVE_TRIGGERS 設定時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也允許觸發程序的遞迴叫用。  
  
 遞迴觸發程序有可能產生下列遞迴類型：  
  
-   間接遞迴  
  
     當進行間接遞迴時，應用程式會更新 T1 資料表。 這會引發 TR1 觸發程序，更新 T2 資料表。 在這個狀況下，T2 觸發程序後來又會引發和更新 T1 資料表。  
  
-   直接遞迴  
  
     當進行直接遞迴時，應用程式會更新 T1 資料表。 這會引發 TR1 觸發程序，更新 T1 資料表。 由於更新了 T1 資料表，因此，又會引發 TR1 觸發程序，依此類推。  
  
 下列範例會使用間接和直接觸發程序遞迴。它假設 T1 資料表定義了 TR1 和 TR2 這兩個更新觸發程序。 TR1 觸發程序會遞迴更新 T1 資料表。 UPDATE 陳述式會執行每個 TR1 和 TR2 各一次。 另外，執行 TR1 會觸發執行 TR1 (遞迴) 和 TR2。 特定觸發程序的 inserted 和 deleted 資料表包含只對應於呼叫觸發程序之 UPDATE 陳述式的資料表。  
  
> [!NOTE]  
>  只有在利用 ALTER DATABASE 來啟用 RECURSIVE_TRIGGERS 設定時，才會發生上述行為。 定義給特定事件的多個觸發程序並沒有任何定義的執行順序。 每個觸發程序都應該是獨立自足的。  
  
 停用 RECURSIVE_TRIGGERS 設定只會防止直接遞迴。 如果也要停用間接遞迴，請利用 sp_configure，將 nested triggers 伺服器選項設為 0。  
  
 如果有任何觸發程序執行 ROLLBACK TRANSACTION，不論巢狀層級為何，都不會執行任何觸發程序。  
  
### <a name="nested-triggers"></a>巢狀觸發程序  
 觸發程序的巢狀結構，最多可達 32 層。 如果觸發程序變更了一份資料表，且這份資料表有另一個觸發程序，就會啟動第二個觸發程序，之後這個觸發程序可能會呼叫第三個觸發程序，依此類推。 如果鏈結中的任何觸發程序造成無限迴圈，就會超出巢狀層級，並取消觸發程序。 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 觸發程序參考 CLR 常式、類型或彙總來執行 Managed 程式碼時，在 32 層的巢狀限制中，這項參考算是一層。 從 Managed 程式碼內叫用的方法，不列入這項限制。  
  
 若要停用巢狀觸發程序，請將 sp_configure 的 nested triggers 選項設成 0 (關閉)。 預設組態接受巢狀觸發程序。 如果關閉了巢狀觸發程序，遞迴觸發程序也會停用，不論利用 ALTER DATABASE 設定的 RECURSIVE_TRIGGERS 設定為何，都是如此。  
  
 第一個 AFTER 觸發程序的巢狀方式置於 INSTEAD OF 觸發程序引發，即使**巢狀觸發程序**伺服器組態選項設定為 0。 不過，在此設定下，後續的 AFTER 觸發程序不會引發。 我們建議您檢閱您的應用程式，來判斷與您的商務規則，新行為是否符合應用程式的巢狀觸發程序時**巢狀觸發程序**伺服器組態選項設定為 0，然後進行適當的修改。  
  
### <a name="deferred-name-resolution"></a>延遲名稱解析  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序、觸發程序和批次參考在編譯階段並不存在的資料表。 這項功能稱為延遲名稱解析。  
  
## <a name="permissions"></a>Permissions  
 若要建立 DML 觸發程序，需要建立觸發程序的資料表或檢視的 ALTER 權限。  
  
 若要建立伺服器範圍 (ON ALL SERVER) 的 DDL 觸發程序或登入觸發程序，需要伺服器的 CONTROL SERVER 權限。 若要建立資料庫範圍 (ON DATABASE) 的 DDL 觸發程序，需要目前資料庫的 ALTER ANY DATABASE DDL TRIGGER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-a-dml-trigger-with-a-reminder-message"></a>A. 使用包含提示訊息的 DML 觸發程序  
 當任何人嘗試在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的 `Customer` 資料表中新增或變更資料時，以下 DML 觸發程序會向用戶端列印一則訊息。  
  
```  
CREATE TRIGGER reminder1  
ON Sales.Customer  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Customer Relations', 16, 10);  
GO  
```  
  
### <a name="b-using-a-dml-trigger-with-a-reminder-e-mail-message"></a>B. 使用包含提示電子郵件訊息的 DML 觸發程序  
 當 `MaryM` 資料表有了改變時，以下範例會向指定的人 (`Customer`) 傳送一則電子郵件訊息。  
  
```  
CREATE TRIGGER reminder2  
ON Sales.Customer  
AFTER INSERT, UPDATE, DELETE   
AS  
   EXEC msdb.dbo.sp_send_dbmail  
        @profile_name = 'AdventureWorks2012 Administrator',  
        @recipients = 'danw@Adventure-Works.com',  
        @body = 'Don''t forget to print a report for the sales force.',  
        @subject = 'Reminder';  
GO  
```  
  
### <a name="c-using-a-dml-after-trigger-to-enforce-a-business-rule-between-the-purchaseorderheader-and-vendor-tables"></a>C. 使用 DML AFTER 觸發程序在 PurchaseOrderHeader 與 Vendor 資料表之間執行商務規則  
 由於 CHECK 條件約束只能參考定義了資料行層級或資料表層級條件約束的資料行，任何跨資料表的條件約束 (這裡是商務規則) 都必須定義成觸發程序。  
  
 以下範例會在 AdventureWorks2012 資料庫中建立 DML 觸發程序。 這個觸發程序會檢查確認供應商最好信用等級 (不是 5) 當嘗試插入新的採購單`PurchaseOrderHeader`資料表。 為了取得供應商的信用等級，必須參考 `Vendor` 資料表。 如果信用等級太低，將會顯示訊息，且不會執行插入動作。  
  
```  
-- This trigger prevents a row from being inserted in the Purchasing.PurchaseOrderHeader 
-- table when the credit rating of the specified vendor is set to 5 (below average).  
  
CREATE TRIGGER Purchasing.LowCredit ON Purchasing.PurchaseOrderHeader  
AFTER INSERT  
AS  
IF EXISTS (SELECT *  
           FROM Purchasing.PurchaseOrderHeader AS p   
           JOIN inserted AS i   
           ON p.PurchaseOrderID = i.PurchaseOrderID   
           JOIN Purchasing.Vendor AS v   
           ON v.BusinessEntityID = p.VendorID  
           WHERE v.CreditRating = 5  
          )  
BEGIN  
RAISERROR ('A vendor''s credit rating is too low to accept new  
purchase orders.', 16, 1);  
ROLLBACK TRANSACTION;  
RETURN   
END;  
GO  
  
-- This statement attempts to insert a row into the PurchaseOrderHeader table  
-- for a vendor that has a below average credit rating.  
-- The AFTER INSERT trigger is fired and the INSERT transaction is rolled back.  
  
INSERT INTO Purchasing.PurchaseOrderHeader (RevisionNumber, Status, EmployeeID,  
VendorID, ShipMethodID, OrderDate, ShipDate, SubTotal, TaxAmt, Freight)  
VALUES (  
2  
,3  
,261  
,1652  
,4  
,GETDATE()  
,GETDATE()  
,44594.55  
,3567.564  
,1114.8638 );  
GO  
  
```  
  
### <a name="d-using-a-database-scoped-ddl-trigger"></a>D. 使用僅限於資料庫的 DDL 觸發程序  
 以下範例利用 DDL 觸發程序避免卸除資料庫中的同義字。  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_SYNONYM  
AS   
   RAISERROR ('You must disable Trigger "safety" to drop synonyms!',10, 1)  
   ROLLBACK  
GO  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
### <a name="e-using-a-server-scoped-ddl-trigger"></a>E. 使用僅限於伺服器的 DDL 觸發程序  
 以下範例會在目前伺服器執行個體出現任何 CREATE DATABASE 事件時，利用 DDL 觸發程序來列印訊息，並利用 `EVENTDATA` 函數來擷取對應 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的文字。 在 DDL 觸發程序使用 EVENTDATA 的詳細範例，請參閱[使用 EVENTDATA 函數](../../relational-databases/triggers/use-the-eventdata-function.md)。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
```  
  
### <a name="f-using-a-logon-trigger"></a>F. 使用登入觸發程序  
 下列的登入觸發程序範例拒絕登入嘗試[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成員的身分*login_test*如果已經有三個執行以該登入的使用者工作階段的登入。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
  
```  
  
### <a name="g-viewing-the-events-that-cause-a-trigger-to-fire"></a>G. 檢視引發觸發程序的事件  
 以下範例會查詢 `sys.triggers` 及 `sys.trigger_events` 目錄檢視，判別引發 `safety` 觸發程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語言事件。 `safety` 是在前一個範例中建立。  
  
```  
SELECT TE.*  
FROM sys.trigger_events AS TE  
JOIN sys.triggers AS T ON T.object_id = TE.object_id  
WHERE T.parent_class = 0 AND T.name = 'safety';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [COLUMNS_UPDATED &#40;TRANSACT-SQL &#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [TRIGGER_NESTLEVEL &#40;TRANSACT-SQL &#41;](../../t-sql/functions/trigger-nestlevel-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_settriggerorder &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)   
 [更新 &#40; &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)   
 [取得關於 DML 觸發程序的詳細資訊](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [取得 DDL 觸發程序的相關資訊](../../relational-databases/triggers/get-information-about-ddl-triggers.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  



