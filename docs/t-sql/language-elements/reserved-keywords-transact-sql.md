---
title: "保留的關鍵字 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- ODBC function calls
- keywords [SQL Server], reserved
- reserved words [SQL Server]
- keywords [SQL Server]
ms.assetid: ed8b3e27-6796-40f0-aef3-0cac5e0e2418
caps.latest.revision: "53"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 000b5c3177db29b173ee836df9c194c2af322d39
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="reserved-keywords-transact-sql"></a>保留關鍵字 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 利用保留的關鍵字來定義、操作和存取資料庫。 保留的關鍵字是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 用來剖析及了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式和批次之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語言文法的一部分。 雖然在語意上可以利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保留關鍵字做為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼中的識別碼及物件名稱，但您必須分隔這些識別碼。  
  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保留關鍵字。  
  
||||  
|-|-|-|  
|ADD|EXTERNAL|PROCEDURE|  
|ALL|FETCH|PUBLIC|  
|ALTER|FILE|RAISERROR|  
|與|FILLFACTOR|READ|  
|ANY|FOR|READTEXT|  
|AS|FOREIGN|RECONFIGURE|  
|ASC|FREETEXT|REFERENCES|  
|AUTHORIZATION|FREETEXTTABLE|複寫|  
|BACKUP|FROM|RESTORE|  
|BEGIN|FULL|RESTRICT|  
|BETWEEN|FUNCTION|RETURN|  
|BREAK|GOTO|REVERT|  
|BROWSE|GRANT|REVOKE|  
|BULK|GROUP|RIGHT|  
|BY|HAVING|ROLLBACK|  
|CASCADE|HOLDLOCK|ROWCOUNT|  
|CASE|IDENTITY|ROWGUIDCOL|  
|CHECK|IDENTITY_INSERT|RULE|  
|CHECKPOINT|IDENTITYCOL|SAVE|  
|CLOSE|IF|SCHEMA|  
|CLUSTERED|IN|SECURITYAUDIT|  
|COALESCE|INDEX|SELECT|  
|COLLATE|INNER|SEMANTICKEYPHRASETABLE|  
|COLUMN|INSERT|SEMANTICSIMILARITYDETAILSTABLE|  
|COMMIT|INTERSECT|SEMANTICSIMILARITYTABLE|  
|COMPUTE|INTO|SESSION_USER|  
|CONSTRAINT|IS|SET|  
|CONTAINS|JOIN|SETUSER|  
|CONTAINSTABLE|KEY|SHUTDOWN|  
|CONTINUE|KILL|SOME|  
|CONVERT|LEFT|STATISTICS|  
|CREATE|LIKE|SYSTEM_USER|  
|CROSS|LINENO|TABLE|  
|CURRENT|LOAD|TABLESAMPLE|  
|CURRENT_DATE|MERGE|TEXTSIZE|  
|CURRENT_TIME|NATIONAL|THEN|  
|CURRENT_TIMESTAMP|NOCHECK|TO|  
|CURRENT_USER|NONCLUSTERED|頂端|  
|CURSOR|NOT|TRAN|  
|DATABASE|NULL|TRANSACTION|  
|DBCC|NULLIF|TRIGGER|  
|DEALLOCATE|OF|TRUNCATE|  
|DECLARE|OFF|TRY_CONVERT|  
|DEFAULT|OFFSETS|TSEQUAL|  
|DELETE|ON|UNION|  
|DENY|OPEN|UNIQUE|  
|DESC|OPENDATASOURCE|UNPIVOT|  
|DISK|OPENQUERY|UPDATE|  
|DISTINCT|OPENROWSET|UPDATETEXT|  
|DISTRIBUTED|OPENXML|USE|  
|DOUBLE|OPTION|使用者|  
|DROP|OR|VALUES|  
|DUMP|ORDER|VARYING|  
|ELSE|OUTER|VIEW|  
|END|OVER|WAITFOR|  
|ERRLVL|PERCENT|WHEN|  
|ESCAPE|PIVOT|WHERE|  
|EXCEPT|PLAN|WHILE|  
|EXEC|PRECISION|取代所有提及的|  
|執行 CREATE 陳述式之前，請先執行|PRIMARY|WITHIN GROUP|  
|EXISTS|PRINT|WRITETEXT|  
|EXIT|PROC||  
  
 另外，ISO 標準也定義了一份保留關鍵字的清單。 請避免在物件名稱和識別碼上使用 ISO 保留關鍵字。 下表所顯示的 ODBC 保留關鍵字清單與 ISO 保留關鍵字清單相同。  
  
> [!NOTE]  
>  ISO 標準保留關鍵字清單有時限制性大於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，有時比較小。 例如，ISO 保留的關鍵字清單包含**INT**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並不需要將它視為保留關鍵字。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 保留關鍵字可用來作為資料庫或資料庫物件 (如資料表、資料行、檢視等) 的識別碼或名稱。 請使用附加引號的識別字或分隔的識別碼。 利用保留關鍵字作為變數和預存程序參數的名稱，並不會受到限制。  
  
## <a name="odbc-reserved-keywords"></a>ODBC 保留關鍵字  
 以下是 ODBC 函數呼叫所用的保留字。 這些字並不會限制最基礎的 SQL 文法；不過，為了確保與支援核心 SQL 文法的驅動程式相容，應用程式應該避免使用這些關鍵字。  
  
 這是目前的 ODBC 保留關鍵字清單。  
  
||||  
|-|-|-|  
|**絕對**|**EXEC**|**重疊**|  
|**動作**|**EXECUTE**|**填補**|  
|**與 ADA**|**EXISTS**|**部分**|  
|**新增**|**EXTERNAL**|**依照 PASCAL 命名法**|  
|**ALL**|**擷取**|**位置**|  
|**配置**|**FALSE**|**有效位數**|  
|**ALTER**|**FETCH**|**準備**|  
|**AND**|**第一個**|**保留**|  
|**ANY**|**浮點數**|**PRIMARY**|  
|**是**|**針對**|**之前**|  
|**AS**|**外部索引**|**權限**|  
|**ASC**|**FORTRAN**|**PROCEDURE**|  
|**判斷提示**|**找到**|**公用**|  
|**在**|**FROM**|**讀取**|  
|**AUTHORIZATION**|**FULL**|**實數**|  
|**AVG**|**取得**|**參考**|  
|**BEGIN**|**全域**|**相對**|  
|**BETWEEN**|**GO**|**限制**|  
|**位元**|**GOTO**|**REVOKE**|  
|**BIT_LENGTH**|**GRANT**|**RIGHT**|  
|**兩者**|**群組**|**復原**|  
|**由**|**具有**|**資料列**|  
|**重疊顯示**|**小時**|**SCHEMA**|  
|**重疊顯示**|**身分識別**|**捲軸**|  
|**CASE**|**即時運算**|**第二個**|  
|**轉型**|**IN**|**區段**|  
|**類別目錄**|**包含**|**SELECT**|  
|**CHAR**|**INDEX**|**工作階段**|  
|**CHAR_LENGTH**|**指標**|**SESSION_USER**|  
|**字元**|**一開始**|**設定**|  
|**CHARACTER_LENGTH**|**內部**|**大小**|  
|**核取**|**輸入**|**SMALLINT**|  
|**CLOSE**|**不區分大小寫**|**某些**|  
|**COALESCE**|**INSERT**|**SPACE**|  
|**自動分頁**|**INT**|**SQL**|  
|**定序**|**整數**|**SQLCA**|  
|**資料行**|**INTERSECT**|**SQLCODE**|  
|**認可**|**間隔**|**SQLERROR**|  
|**連接**|**到**|**SQLSTATE**|  
|**連線**|**IS**|**SQLWARNING**|  
|**條件約束**|**隔離**|**SUBSTRING**|  
|**條件約束**|**聯結**|**SUM**|  
|**CONTINUE**|**索引鍵**|**SYSTEM_USER**|  
|**轉換**|**LANGUAGE**|**TABLE**|  
|**對應**|**最後一個**|**暫存**|  
|**COUNT**|**開頭**|**然後**|  
|**建立**|**LEFT**|**時間**|  
|**跨**|**層級**|**時間戳記**|  
|**目前的**|**LIKE**|**TIMEZONE_HOUR**|  
|**CURRENT_DATE**|**本機**|**TIMEZONE_MINUTE**|  
|**CURRENT_TIME**|**LOWER**|**若要**|  
|**CURRENT_TIMESTAMP**|**MATCH**|**後端**|  
|**CURRENT_USER**|**MAX**|**交易**|  
|**資料指標**|**MIN**|**TRANSLATE**|  
|**日期**|**分鐘**|**轉譯**|  
|**DAY**|**模組**|**TRIM**|  
|**DEALLOCATE**|**MONTH**|**為 TRUE**|  
|**DEC**|**名稱**|**等位**|  
|**小數點**|**國家 （地區)**|**唯一**|  
|**宣告**|**自然**|**未知**|  
|**DEFAULT**|**NCHAR**|**UPDATE**|  
|**可以延後**|**下一步**|**UPPER**|  
|**延遲**|**否**|**使用方式**|  
|**DELETE**|**NONE**|**USER**|  
|**DESC**|**NOT**|**使用**|  
|**描述**|**NULL**|**VALUE**|  
|**描述元**|**NULLIF**|**值**|  
|**診斷**|**數值**|**VARCHAR**|  
|**中斷連線**|**OCTET_LENGTH**|**不同的**|  
|**相異**|**的**|**VIEW**|  
|**網域**|**ON**|**當**|  
|**DOUBLE**|**只有**|**每當**|  
|**卸除**|**OPEN**|**WHERE**|  
|**其他**|**選項**|**與**|  
|**END**|**OR**|**工作**|  
|**結束 EXEC**|**順序**|**寫入**|  
|**逸出**|**外部**|**YEAR**|  
|**除了**|**輸出**|**區域**|  
|**例外狀況**|||  
  
## <a name="future-keywords"></a>未來關鍵字  
 下列關鍵字可能保留給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實作新功能的未來版本。 請考慮避免使用這些字做為識別碼。  
  
||||  
|-|-|-|  
|ABSOLUTE|HOST|RELATIVE|  
|ACTION|HOUR|RELEASE|  
|ADMIN|IGNORE|RESULT|  
|AFTER|IMMEDIATE|RETURNS|  
|AGGREGATE|INDICATOR|ROLE|  
|ALIAS|INITIALIZE|ROLLUP|  
|ALLOCATE|INITIALLY|ROUTINE|  
|ARE|INOUT|ROW|  
|ARRAY|INPUT|ROWS|  
|ASENSITIVE|INT|SAVEPOINT|  
|ASSERTION|INTEGER|SCROLL|  
|ASYMMETRIC|INTERSECTION|SCOPE|  
|AT|INTERVAL|SEARCH|  
|ATOMIC|ISOLATION|SECOND|  
|BEFORE|ITERATE|SECTION|  
|BINARY|LANGUAGE|SENSITIVE|  
|BIT|LARGE|SEQUENCE|  
|BLOB|LAST|SESSION|  
|BOOLEAN|LATERAL|SETS|  
|BOTH|LEADING|SIMILAR|  
|BREADTH|LESS|SIZE |  
|CALL|LEVEL|SMALLINT|  
|CALLED|LIKE_REGEX|SPACE|  
|CARDINALITY|LIMIT|SPECIFIC|  
|CASCADED|LN|SPECIFICTYPE|  
|CAST|LOCAL|SQL|  
|CATALOG|LOCALTIME|SQLEXCEPTION|  
|CHAR|LOCALTIMESTAMP|SQLSTATE|  
|CHARACTER|LOCATOR|SQLWARNING|  
|CLASS|MAP|START|  
|CLOB|MATCH|STATE|  
|COLLATION|MEMBER|STATEMENT|  
|COLLECT|METHOD|STATIC|  
|COMPLETION|MINUTE|STDDEV_POP|  
|CONDITION|MOD|STDDEV_SAMP|  
|CONNECT|MODIFIES|STRUCTURE|  
|CONNECTION|MODIFY|SUBMULTISET|  
|CONSTRAINTS|MODULE|SUBSTRING_REGEX|  
|CONSTRUCTOR|MONTH|SYMMETRIC|  
|CORR|MULTISET|SYSTEM|  
|CORRESPONDING|NAMES|TEMPORARY|  
|COVAR_POP|NATURAL|TERMINATE|  
|COVAR_SAMP|NCHAR|THAN|  
|CUBE|NCLOB|TIME|  
|CUME_DIST|NEW|timestamp|  
|CURRENT_CATALOG|NEXT|TIMEZONE_HOUR|  
|CURRENT_DEFAULT_TRANSFORM_GROUP|否|TIMEZONE_MINUTE|  
|CURRENT_PATH|無|TRAILING|  
|CURRENT_ROLE|NORMALIZE|TRANSLATE_REGEX|  
|CURRENT_SCHEMA|NUMERIC|TRANSLATION|  
|CURRENT_TRANSFORM_GROUP_FOR_TYPE|OBJECT|TREAT|  
|CYCLE|OCCURRENCES_REGEX|TRUE|  
|DATA|OLD|UESCAPE|  
|DATE|ONLY|UNDER|  
|DAY|OPERATION|UNKNOWN|  
|DEC|ORDINALITY|UNNEST|  
|DECIMAL|OUT|USAGE|  
|DEFERRABLE|OVERLAY|USING|  
|DEFERRED|OUTPUT|Value|  
|DEPTH|PAD|VAR_POP|  
|DEREF|參數|VAR_SAMP|  
|DESCRIBE|PARAMETERS|VARCHAR|  
|DESCRIPTOR|PARTIAL|VARIABLE|  
|DESTROY|PARTITION|WHENEVER|  
|DESTRUCTOR|PATH|WIDTH_BUCKET|  
|DETERMINISTIC|POSTFIX|WITHOUT|  
|DICTIONARY|PREFIX|WINDOW|  
|DIAGNOSTICS|PREORDER|WITHIN|  
|DISCONNECT|PREPARE|WORK|  
|DOMAIN|PERCENT_RANK|WRITE|  
|DYNAMIC|PERCENTILE_CONT|XMLAGG|  
|EACH|PERCENTILE_DISC|XMLATTRIBUTES|  
|ELEMENT|POSITION_REGEX|XMLBINARY|  
|END-EXEC|PRESERVE|XMLCAST|  
|EQUALS|PRIOR|XMLCOMMENT|  
|EVERY|PRIVILEGES|XMLCONCAT|  
|EXCEPTION|RANGE|XMLDOCUMENT|  
|FALSE|READS|XMLELEMENT|  
|FILTER|REAL|XMLEXISTS|  
|FIRST|RECURSIVE|XMLFOREST|  
|FLOAT|REF|XMLITERATE|  
|FOUND|REFERENCING|XMLNAMESPACES|  
|FREE|REGR_AVGX|XMLPARSE|  
|FULLTEXTTABLE|REGR_AVGY|XMLPI|  
|FUSION|REGR_COUNT|XMLQUERY|  
|GENERAL|REGR_INTERCEPT|XMLSERIALIZE|  
|GET|REGR_R2|XMLTABLE|  
|GLOBAL|REGR_SLOPE|XMLTEXT|  
|GO|REGR_SXX|XMLVALIDATE|  
|GROUPING|REGR_SXY|YEAR|  
|HOLD|REGR_SYY|ZONE|  
  
## <a name="see-also"></a>請參閱＜  
 [SET QUOTED_IDENTIFIER &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
