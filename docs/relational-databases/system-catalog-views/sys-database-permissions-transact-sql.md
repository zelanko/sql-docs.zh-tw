---
title: sys.databases database_permissions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_permissions
- sys.database_permissions_TSQL
- database_permissions_TSQL
- sys.database_permissions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_permissions catalog view
ms.assetid: c1e261f8-6cb0-4759-b5f1-5ec233602655
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a87be6fe0a68172a99ade4704ae4111cabbe95f1
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982731"
---
# <a name="sysdatabase_permissions-transact-sql"></a>sys.database_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對資料庫中每個權限或資料行例外狀況權限，各傳回一個資料列。 針對資料行，與對應物件層級權限不同的每個權限，各有一個資料列。 如果資料行許可權與對應的物件使用權限相同，就不會有任何資料列，而且所套用的許可權會是物件。  
  
> [!IMPORTANT]  
>  資料行層級權限會覆寫同一實體的物件層級權限。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|識別權限所在的類別。<br /><br /> 0 = 資料庫<br />1 = 物件或資料行<br />3 = 結構描述<br />4 = 資料庫主體<br />5 = 元件-**適用于**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。<br />6 = 類型<br />10 = XML 架構集合- <br />                      **適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本。<br />15 = 訊息類型-**適用**于： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。<br />16 = 服務合約-**適用**于： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。<br />17 = 服務-**適用于**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。<br />18 = 遠端服務系結-**適用于**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。<br />19 = Route-**適用于**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。<br />23 = 全文檢索目錄-**適用**于： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。<br />24 = 對稱金鑰-**適用**于： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。<br />25 = 憑證-**適用于**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。<br />26 = 非對稱金鑰-**適用于**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本。|  
|**class_desc**|**nvarchar(60)**|權限所在類別的描述。<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN<br /><br /> SCHEMA<br /><br /> DATABASE_PRINCIPAL<br /><br /> ASSEMBLY<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> MESSAGE_TYPE<br /><br /> SERVICE_CONTRACT<br /><br /> SERVICE<br /><br /> REMOTE_SERVICE_BINDING<br /><br /> ROUTE<br /><br /> FULLTEXT_CATALOG<br /><br /> SYMMETRIC_KEYS<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC_KEY|  
|**major_id**|**int**|權限所在項目的識別碼，它是根據類別加以解譯。 一般來說， **major_id**只是適用于類別所代表之識別碼的類型。 <br /><br /> 0 = 資料庫本身 <br /><br /> > 0 = 使用者物件的物件識別碼 <br /><br /> \<0 = 系統物件的物件識別碼 |  
|**minor_id**|**int**|權限所在項目的次要識別碼，它是根據類別加以解譯。 **Minor_id**通常是零，因為物件的類別沒有可用的子類別。 否則，它是資料表的資料行識別碼。|  
|**grantee_principal_id**|**int**|獲授與權限的資料庫主體識別碼。|  
|**grantor_principal_id**|**int**|這些權限之同意授權者的資料庫主體識別碼。|  
|**型別**|**char （4）**|資料庫權限類型。 如需權限類型的清單，請參閱下表。|  
|**permission_name**|**nvarchar(128)**|權限名稱。|  
|**state**|**char(1)**|權限狀態：<br /><br /> D = 拒絕<br /><br /> R = 撤銷<br /><br /> G = 授與<br /><br /> W = 以授與選項授與|  
|**state_desc**|**nvarchar(60)**|權限狀態的描述：<br /><br /> DENY<br /><br /> REVOKE<br /><br /> GRANT<br /><br /> GRANT_WITH_GRANT_OPTION|  

## <a name="database-permissions"></a>資料庫權限   
可以是下列類型的許可權。
  
|權限類型|權限名稱|適用於安全性實體|  
|---------------------|---------------------|--------------------------|  
|AADS |ALTER ANY DATABASE EVENT SESSION |DATABASE |  
|AAMK |ALTER ANY MASK |DATABASE |  
|AEDS |ALTER ANY EXTERNAL DATA SOURCE |DATABASE |  
|AEFF |ALTER ANY EXTERNAL FILE FORMAT |DATABASE |  
|AL|ALTER|APPLICATION ROLE、ASSEMBLY、ASYMMETRIC KEY、CERTIFICATE、CONTRACT、DATABASE、FULLTEXT CATALOG、MESSAGE TYPE、OBJECT、REMOTE SERVICE BINDING、ROLE、ROUTE、SCHEMA、SERVICE、SYMMETRIC KEY、USER、XML SCHEMA COLLECTION|  
|ALAK|ALTER ANY ASYMMETRIC KEY|DATABASE|  
|ALAR|ALTER ANY APPLICATION ROLE|DATABASE|  
|ALAS|ALTER ANY ASSEMBLY|DATABASE|  
|ALCF|ALTER ANY CERTIFICATE|DATABASE|  
|ALDS|ALTER ANY DATASPACE|DATABASE|  
|ALED|ALTER ANY DATABASE EVENT NOTIFICATION|DATABASE|  
|ALFT|ALTER ANY FULLTEXT CATALOG|DATABASE|  
|ALMT|ALTER ANY MESSAGE TYPE|DATABASE|  
|ALRL|ALTER ANY ROLE|DATABASE|  
|ALRT|ALTER ANY ROUTE|DATABASE|  
|ALSB|ALTER ANY REMOTE SERVICE BINDING|DATABASE|  
|ALSC|ALTER ANY CONTRACT|DATABASE|  
|ALSK|ALTER ANY SYMMETRIC KEY|DATABASE|  
|ALSM|ALTER ANY SCHEMA|DATABASE|  
|ALSV|ALTER ANY SERVICE|DATABASE|  
|ALTG|ALTER ANY DATABASE DDL TRIGGER|DATABASE|  
|ALUS|ALTER ANY USER|DATABASE|  
|AUTH|AUTHENTICATE|DATABASE|  
|BADB|BACKUP DATABASE|DATABASE|  
|BALO|BACKUP LOG|DATABASE|  
|CL|CONTROL|APPLICATION ROLE、ASSEMBLY、ASYMMETRIC KEY、CERTIFICATE、CONTRACT、DATABASE、FULLTEXT CATALOG、MESSAGE TYPE、OBJECT、REMOTE SERVICE BINDING、ROLE、ROUTE、SCHEMA、SERVICE、SYMMETRIC KEY、TYPE、USER、XML SCHEMA COLLECTION|  
|CO|CONNECT|DATABASE|  
|CORP|CONNECT REPLICATION|DATABASE|  
|CP|CHECKPOINT|DATABASE|  
|CRAG|CREATE AGGREGATE|DATABASE|  
|CRAK|CREATE ASYMMETRIC KEY|DATABASE|  
|CRAS|CREATE ASSEMBLY|DATABASE|  
|CRCF|CREATE CERTIFICATE|DATABASE|  
|CRDB|CREATE DATABASE|DATABASE|  
|CRDF|CREATE DEFAULT|DATABASE|  
|CRED|CREATE DATABASE DDL EVENT NOTIFICATION|DATABASE|  
|CRFN|CREATE FUNCTION|DATABASE|  
|CRFT|CREATE FULLTEXT CATALOG|DATABASE|  
|CRMT|CREATE MESSAGE TYPE|DATABASE|  
|CRPR|CREATE PROCEDURE|DATABASE|  
|CRQU|CREATE QUEUE|DATABASE|  
|CRRL|CREATE ROLE|DATABASE|  
|CRRT|CREATE ROUTE|DATABASE|  
|CRRU|CREATE RULE|DATABASE|  
|CRSB|CREATE REMOTE SERVICE BINDING|DATABASE|  
|CRSC|CREATE CONTRACT|DATABASE|  
|CRSK|CREATE SYMMETRIC KEY|DATABASE|  
|CRSM|CREATE SCHEMA|DATABASE|  
|CRSN|CREATE SYNONYM|DATABASE|  
|CRSO|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> CREATE SEQUENCE|DATABASE|  
|CRSV|CREATE SERVICE|DATABASE|  
|CRTB|CREATE TABLE|DATABASE|  
|CRTY|CREATE TYPE|DATABASE|  
|CRVW|CREATE VIEW|DATABASE|  
|CRXS|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本。<br /><br /> CREATE XML SCHEMA COLLECTION|DATABASE|  
|DABO |ADMINISTER DATABASE BULK OPERATIONS | DATABASE |
|DL|DELETE|DATABASE、OBJECT、SCHEMA|  
|EAES |EXECUTE ANY EXTERNAL SCRIPT |DATABASE |
|EX|EXECUTE|ASSEMBLY、DATABASE、OBJECT、SCHEMA、TYPE、XML SCHEMA COLLECTION|  
|IM|IMPERSONATE|USER|  
|IN|Insert|DATABASE、OBJECT、SCHEMA|  
|RC|RECEIVE|OBJECT|  
|RF|REFERENCES|ASSEMBLY、ASYMMETRIC KEY、CERTIFICATE、CONTRACT、DATABASE、FULLTEXT CATALOG、MESSAGE TYPE、OBJECT、SCHEMA、SYMMETRIC KEY、TYPE、XML SCHEMA COLLECTION|  
|SL|SELECT|DATABASE、OBJECT、SCHEMA|  
|SN|SEND|SERVICE|  
|SPLN|SHOWPLAN|DATABASE|  
|SUQN|SUBSCRIBE QUERY NOTIFICATIONS|DATABASE|  
|TO|TAKE OWNERSHIP|ASSEMBLY、ASYMMETRIC KEY、CERTIFICATE、CONTRACT、DATABASE、FULLTEXT CATALOG、MESSAGE TYPE、OBJECT、REMOTE SERVICE BINDING、ROLE、ROUTE、SCHEMA、SERVICE、SYMMETRIC KEY、TYPE、XML SCHEMA COLLECTION|  
|UP|UPDATE|DATABASE、OBJECT、SCHEMA|  
|VW|VIEW DEFINITION|APPLICATION ROLE、ASSEMBLY、ASYMMETRIC KEY、CERTIFICATE、CONTRACT、DATABASE、FULLTEXT CATALOG、MESSAGE TYPE、OBJECT、REMOTE SERVICE BINDING、ROLE、ROUTE、SCHEMA、SERVICE、SYMMETRIC KEY、TYPE、USER、XML SCHEMA COLLECTION|  
|VWCK |VIEW ANY COLUMN ENCRYPTION KEY DEFINITION|DATABASE |  
|VWCM |VIEW ANY COLUMN MASTER KEY DEFINITION|DATABASE |  
|VWCT|VIEW CHANGE TRACKING|TABLE、SCHEMA|  
|VWDS|VIEW DATABASE STATE|DATABASE|  
  
## <a name="permissions"></a>Permissions  
 任何使用者都可以查看他們自己的權限。 若要查看其他使用者的權限，則需要 VIEW DEFINITION、ALTER ANY USER 或使用者的任何權限。 若要查看使用者定義角色，則需要 ALTER ANY ROLE 或該角色的成員資格 (例如 Public)。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-the-permissions-of-database-principals"></a>A：列出資料庫主體的所有權限  
 下列查詢會列出已明確授與或拒絕資料庫主體的權限。  
  
> [!IMPORTANT]  
>  固定資料庫角色的權限並未出現在 sys.database_permissions 中。 因此，資料庫主體可能仍有其他未列於此處的權限。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="b-listing-permissions-on-schema-objects-within-a-database"></a>B：列出資料庫內結構描述物件的權限  
 下列查詢會聯結 sys.database_principals 與 sys.database_permissions 以及 sys.objects 與 sys.schemas，藉此列出已授與或拒絕特定結構描述物件的權限。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
    
  
## <a name="see-also"></a>另請參閱  
 [安全性實體](../../relational-databases/security/securables.md)   
 [權限階層 &#40;Database Engine&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  


