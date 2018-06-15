---
title: sys.database_principals (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a879dfcc6dd0feb57126574947b51f84261af915
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181934"
---
# <a name="sysdatabaseprincipals-transact-sql"></a>sys.database_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中每一個安全性主體，各傳回一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|主體的名稱，它在資料庫中是唯一的。|  
|**principal_id**|**int**|主體的識別碼，它在資料庫中是唯一的。|  
|**type**|**char(1)**|主體類型：<br /><br /> A = 應用程式角色<br /><br /> C = 對應至憑證的使用者<br /><br /> E = 外部使用者從 Azure Active Directory<br /><br /> G = Windows 群組<br /><br /> K = 對應至非對稱金鑰的使用者<br /><br /> R = 資料庫角色<br /><br /> S = SQL 使用者<br /><br /> U = Windows 使用者<br /><br /> X = 從 Azure Active Directory 群組或應用程式的外部群組|  
|**type_desc**|**nvarchar(60)**|主體類型的描述。<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|當 SQL 名稱未指定結構描述時所要使用的名稱。 非類型 S、U 或 A 的主體，則為 NULL。|  
|**create_date**|**datetime**|建立主體的時間。|  
|**modify_date**|**datetime**|上次修改主體的時間。|  
|**owning_principal_id**|**int**|擁有這個主體的主體識別碼。 必須由擁有資料庫角色以外，所有主體**dbo**。|  
|**sid**|**varbinary(85)**|主體的 SID (安全性識別碼)。  如果是 SYS 和 INFORMATION SCHEMAS，則為 NULL|  
|**is_fixed_role**|**bit**|如果是 1，此資料列代表下列其中一個固定資料庫角色的項目：db_owner、db_accessadmin、db_datareader、db_datawriter、db_ddladmin、db_securityadmin、db_backupoperator、db_denydatareader、db_denydatawriter。|  
|**authentication_type**|**int**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 代表驗證類型。 以下是可能的值和它們的描述。<br /><br /> 0： 沒有驗證<br />1： 執行個體驗證<br />2： 驗證資料庫<br />3: Windows 驗證|  
|**authentication_type_desc**|**nvarchar(60)**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 驗證類型的描述。 以下是可能的值和它們的描述。<br /><br /> NONE： 無驗證<br />執行個體： 執行個體驗證<br />資料庫： 資料庫驗證<br />WINDOWS: Windows 驗證|  
|**default_language_name**|**sysname**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 表示此主體的預設語言。|  
|**default_language_lcid**|**int**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 表示此主體的預設 LCID。|  
|**allow_encrypted_value_modifications**|**bit**|**適用對象**：[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 在大量複製作業時隱藏伺服器上的密碼編譯中繼資料檢查。 這可讓使用者使用加密永遠加密，資料表或資料庫之間無須解密資料的大量複製資料。 預設值為 OFF。 |      
  
## <a name="remarks"></a>備註  
 *PasswordLastSetTime*屬性值可用於所有支援的設定的 SQL Server，但其他屬性僅適用於 SQL Server 正在執行 Windows Server 2003 或更新版本，和 CHECK_POLICY 和 CHECK_ 上時會啟用到期日。 請參閱[密碼原則](../../relational-databases/security/password-policy.md)如需詳細資訊。  
  
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
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C： 列出資料庫主體的所有權限  
 下列查詢會列出已明確授與或拒絕資料庫主體的權限。  
  
> [!IMPORTANT]  
>  固定的資料庫角色的權限不會出現在`sys.database_permissions`。 因此，資料庫主體可能仍有其他未列於此處的權限。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D： 列出資料庫內的結構描述物件權限  
 下列查詢會聯結`sys.database_principals`和`sys.database_permissions`至`sys.objects`和`sys.schemas`清單權限授與或拒絕特定結構描述物件。  
  
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
 [自主的資料庫使用者-使資料庫可攜](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  


