---
title: sys.databases database_principals （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_principals
- database_principals_TSQL
- sys.database_principals
- sys.database_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_principals catalog view
ms.assetid: 8cb239e9-eb8c-4109-9cec-0d35de95fa0e
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2ba34b8ceab3b90e45417728de2c3c697da459ac
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982707"
---
# <a name="sysdatabase_principals-transact-sql"></a>sys.database_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中每一個安全性主體，各傳回一個資料列。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|主體的名稱，它在資料庫中是唯一的。|  
|**principal_id**|**int**|主體的識別碼，它在資料庫中是唯一的。|  
|**型別**|**char(1)**|主體類型：<br /><br /> A = 應用程式角色<br /><br /> C = 對應至憑證的使用者<br /><br /> E = 來自 Azure Active Directory 的外部使用者<br /><br /> G = Windows 群組<br /><br /> K = 對應至非對稱金鑰的使用者<br /><br /> R = 資料庫角色<br /><br /> S = SQL 使用者<br /><br /> U = Windows 使用者<br /><br /> X = 來自 Azure Active Directory 群組或應用程式的外部群組|  
|**type_desc**|**nvarchar(60)**|主體類型的描述。<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|當 SQL 名稱未指定結構描述時所要使用的名稱。 非類型 S、U 或 A 的主體，則為 NULL。|  
|**create_date**|**datetime**|建立主體的時間。|  
|**modify_date**|**datetime**|上次修改主體的時間。|  
|**owning_principal_id**|**int**|擁有這個主體的主體識別碼。 資料庫角色以外的所有主體都必須由**dbo**所擁有。|  
|**sid**|**varbinary(85)**|主體的 SID (安全性識別碼)。  如果是 SYS 和 INFORMATION SCHEMAS，則為 NULL|  
|**is_fixed_role**|**bit**|如果是 1，此資料列代表下列其中一個固定資料庫角色的項目：db_owner、db_accessadmin、db_datareader、db_datawriter、db_ddladmin、db_securityadmin、db_backupoperator、db_denydatareader、db_denydatawriter。|  
|**authentication_type**|**int**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 代表驗證類型。 以下是可能的值及其描述。<br /><br /> 0：無驗證<br />1：實例驗證<br />2：資料庫驗證<br />3： Windows 驗證|  
|**authentication_type_desc**|**nvarchar(60)**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 驗證類型的描述。 以下是可能的值及其描述。<br /><br /> 無：無驗證<br />實例：實例驗證<br />資料庫：資料庫驗證<br />WINDOWS： Windows 驗證|  
|**default_language_name**|**sysname**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 表示此主體的預設語言。|  
|**default_language_lcid**|**int**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 表示此主體的預設 LCID。|  
|**allow_encrypted_value_modifications**|**bit**|**適用於**：[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 及更新版本、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 在大量複製作業時隱藏伺服器上的密碼編譯中繼資料檢查。 這可讓使用者在不解密資料的情況下，使用 Always Encrypted 在資料表或資料庫之間大量複製已加密的資料。 預設值為 OFF。 |      
  
## <a name="remarks"></a>Remarks  
 *PasswordLastSetTime*屬性可用於 SQL Server 的所有支援設定，但只有當 SQL Server 在 Windows Server 2003 或更新版本上執行，而且 CHECK_POLICY 和 CHECK_EXPIRATION 都已啟用時，才可以使用其他屬性。 如需詳細資訊，請參閱[密碼原則](../../relational-databases/security/password-policy.md)。  
  
## <a name="permissions"></a>Permissions  
 任何使用者都可以查看他們自己的使用者名稱、系統使用者和固定資料庫角色。 若要查看其他使用者，則需要 ALTER ANY USER 或該使用者的權限。 若要查看使用者定義角色，則需要 ALTER ANY ROLE 或該角色的成員資格。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C：列出資料庫主體的擁有權限  
 下列查詢會列出已明確授與或拒絕資料庫主體的權限。  
  
> [!IMPORTANT]  
>  固定資料庫角色的許可權不會出現在 `sys.database_permissions`中。 因此，資料庫主體可能仍有其他未列於此處的權限。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D：列出資料庫內架構物件的許可權  
 下列查詢會將 `sys.database_principals` 和 `sys.database_permissions` 聯結至 `sys.objects` 和 `sys.schemas`，以列出授與或拒絕特定架構物件的許可權。  
  
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
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 自主[資料庫使用者-使資料庫可](../../relational-databases/security/contained-database-users-making-your-database-portable.md)攜   
 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  


