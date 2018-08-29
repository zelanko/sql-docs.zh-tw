---
title: sys.objects & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.objects_TSQL
- objects
- sys.objects
- objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.objects catalog view
- table-valued parameters, sys.objects catalog view
- user-defined table types [SQL Server]
- table types [SQL Server]
ms.assetid: f8d6163a-2474-410c-a794-997639f31b3b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f94f5802e53c40dab74730a95f09686cd1f61481
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079787"
---
# <a name="sysobjects-transact-sql"></a>sys.objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  包含每個資料庫，包括原生編譯純量使用者定義的函式內建立的使用者定義的結構描述範圍物件的資料列。  
  
 如需詳細資訊，請參閱[記憶體內部 OLTP 的純量使用者定義函數](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
> [!NOTE]  
>  sys.objects 不顯示 DDL 觸發程序，因為它們不是以結構描述為範圍。 在中找到所有觸發程序，DML 和 DDL 在內[sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)。 sys.triggers 支援各種觸發程序種類的混合名稱範圍規則。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|物件名稱。|  
|object_id|**int**|物件識別碼。 在資料庫中，這是唯一的。|  
|principal_id|**int**|如果個別擁有者不是結構描述擁有者，這便是個別擁有者的識別碼。 依預設，結構描述包含的物件就是結構描述擁有者所擁有的物件。 不過，您也可以利用 ALTER AUTHORIZATION 陳述式來變更擁有權，指定替代的擁有者。<br /><br /> 如果沒有替代的個別擁有者，這便是 NULL。<br /><br /> 如果物件類型是下列其中一項，便是 NULL：<br /><br /> C = CHECK 條件約束<br /><br /> D = DEFAULT (條件約束或獨立式)<br /><br /> F = FOREIGN KEY 條件約束<br /><br /> PK = PRIMARY KEY 條件約束<br /><br /> R = 規則 (舊式、獨立式)<br /><br /> TA = 組件 (CLR 整合) 觸發程序<br /><br /> TR = SQL 觸發程序<br /><br /> UQ = UNIQUE 條件約束|  
|schema_id|**int**|物件所在的結構描述識別碼。<br /><br /> 結構描述範圍的系統物件永遠包含在 sys 或 INFORMATION_SCHEMA 結構描述中。|  
|parent_object_id|**int**|這個物件所屬的物件識別碼。<br /><br /> 0 = 不是子物件。|  
|型別|**char(2)**|物件類型：<br /><br /> AF = 彙總函式 (CLR)<br /><br /> C = CHECK 條件約束<br /><br /> D = DEFAULT (條件約束或獨立式)<br /><br /> F = FOREIGN KEY 條件約束<br /><br /> FN = SQL 純量函數<br /><br /> FS = 組件 (CLR) 純量函數<br /><br /> FT = 組件 (CLR) 資料表值函式<br /><br /> IF = SQL 嵌入資料表值函式<br /><br /> IT = 內部資料表<br /><br /> P = SQL 預存程序<br /><br /> PC = 組件 (CLR) 預存程序<br /><br /> PG = 計畫指南<br /><br /> PK = PRIMARY KEY 條件約束<br /><br /> R = 規則 (舊式、獨立式)<br /><br /> RF = 複寫篩選程序<br /><br /> S = 系統基底資料表<br /><br /> SN = 同義字<br /><br /> SO = 序列物件<br /><br /> U = 資料表 (使用者定義)<br /><br /> V = 檢視<br /><br /> <br /><br /> **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> <br /><br /> SQ = 服務佇列<br /><br /> TA = 組件 (CLR) DML 觸發程序<br /><br /> TF = SQL 資料表值函式<br /><br /> TR = SQL DML 觸發程序<br /><br /> TT = 資料表類型<br /><br /> UQ = UNIQUE 條件約束<br /><br /> X = 擴充預存程序<br /><br /> <br /><br /> **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]， [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。<br /><br /> <br /><br /> GET = 外部資料表|  
|type_desc|**nvarchar(60)**|物件類型的描述：<br /><br /> AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_STORED_PROCEDURE<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> CLR_TRIGGER<br /><br /> DEFAULT_CONSTRAINT<br /><br /> EXTENDED_STORED_PROCEDURE<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> INTERNAL_TABLE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> RULE<br /><br /> SEQUENCE_OBJECT<br /><br /> <br /><br /> **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> <br /><br /> SERVICE_QUEUE<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> SQL_STORED_PROCEDURE<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> SYNONYM<br /><br /> SYSTEM_TABLE<br /><br /> TABLE_TYPE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> USER_TABLE<br /><br /> VIEW|  
|create_date|**datetime**|物件的建立日期。|  
|modify_date|**datetime**|上次利用 ALTER 陳述式來修改物件的日期。 如果物件是資料表或檢視，當建立或變更資料表或檢視的叢集索引時，也會變更 modify_date。|  
|is_ms_shipped|**bit**|物件是內部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件所建立的。|  
|is_published|**bit**|已發行物件。|  
|is_schema_published|**bit**|僅發行物件的結構描述。|  
  
## <a name="remarks"></a>備註  
 您可以套用[OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)， [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md)，並[OBJECTPROPERTY](../../t-sql/functions/objectproperty-transact-sql.md)（） 內建函數，在 sys.objects 所顯示的物件。  
  
 此檢視包含相同的結構描述，並呼叫的版本[sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)，它會顯示系統物件。 沒有名為另一個檢視[sys.all_objects](../../relational-databases/system-catalog-views/sys-all-objects-transact-sql.md)它會顯示系統和使用者物件。 這三個目錄檢視都有相同的結構。  
  
 在這一版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，擴充索引 (例如 XML 索引或空間索引) 會視為 sys.objects 中的內部資料表 (type = IT 且 type_desc = INTERNAL_TABLE)。 如果是擴充索引：  
  
-   name 是索引資料表的內部名稱。  
  
-   parent_object_id 是基底資料表的 object_id。  
  
-   is_ms_shipped、is_published 和 is_schema_published 資料行設定為 0。  

**相關的有用系統檢視表**  
可以檢視的物件子集，藉由使用系統檢視表的特定類型的物件，例如：  
- [sys.tables](sys-tables-transact-sql.md)  
- [sys.views](sys-views-transact-sql.md)  
- [sys.procedures](sys-procedures-transact-sql.md)  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-all-the-objects-that-have-been-modified-in-the-last-n-days"></a>A. 傳回在過去 N 天中修改過的所有物件  
 在您執行下列查詢之前，請使用有效的值取代 `<database_name>` 及 `<n_days>`。  
  
```sql  
USE <database_name>;  
GO  
SELECT name AS object_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE modify_date > GETDATE() - <n_days>  
ORDER BY modify_date;  
GO  
```  
  
### <a name="b-returning-the-parameters-for-a-specified-stored-procedure-or-function"></a>B. 傳回指定之預存程序或函數的參數  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.object_name>`。  
  
```sql  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,o.name AS object_name  
    ,o.type_desc  
    ,p.parameter_id  
    ,p.name AS parameter_name  
    ,TYPE_NAME(p.user_type_id) AS parameter_type  
    ,p.max_length  
    ,p.precision  
    ,p.scale  
    ,p.is_output  
FROM sys.objects AS o  
INNER JOIN sys.parameters AS p ON o.object_id = p.object_id  
WHERE o.object_id = OBJECT_ID('<schema_name.object_name>')  
ORDER BY schema_name, object_name, p.parameter_id;  
GO  
```  
  
### <a name="c-returning-all-the-user-defined-functions-in-a-database"></a>C. 傳回資料庫中的所有使用者定義函數  
 在您執行下列查詢之前，請使用有效的資料庫名稱取代 `<database_name>`。  
  
```sql  
USE <database_name>;  
GO  
SELECT name AS function_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE type_desc LIKE '%FUNCTION%';  
GO  
```  
  
### <a name="d-returning-the-owner-of-each-object-in-a-schema"></a>D. 傳回結構描述中每個物件的擁有者。  
 在您執行下列查詢之前，請使用有效的名稱取代所有 `<database_name>` 及 `<schema_name>`。  
  
```sql  
USE <database_name>;  
GO  
SELECT 'OBJECT' AS entity_type  
    ,USER_NAME(OBJECTPROPERTY(object_id, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.objects WHERE SCHEMA_NAME(schema_id) = '<schema_name>'  
UNION   
SELECT 'TYPE' AS entity_type  
    ,USER_NAME(TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.types WHERE SCHEMA_NAME(schema_id) = '<schema_name>'   
UNION  
SELECT 'XML SCHEMA COLLECTION' AS entity_type   
    ,COALESCE(USER_NAME(xsc.principal_id),USER_NAME(s.principal_id)) AS owner_name  
    ,xsc.name   
FROM sys.xml_schema_collections AS xsc JOIN sys.schemas AS s  
    ON s.schema_id = xsc.schema_id  
WHERE s.name = '<schema_name>';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.all_objects &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-all-objects-transact-sql.md)   
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.internal_tables &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md)  
  
  
