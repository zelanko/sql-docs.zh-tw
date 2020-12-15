---
description: sys.server_permissions (Transact-SQL)
title: sys.server_permissions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/20/2019
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_permissions_TSQL
- sys.server_permissions
- server_permissions
- server_permissions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_permissions catalog view
ms.assetid: 7d78bf17-6c64-4166-bd0b-9e9e20992136
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc833da8d53eadd88152e603777b4799ac30938f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464659"
---
# <a name="sysserver_permissions-transact-sql"></a>sys.server_permissions (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  針對每個伺服器層級權限，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|識別權限所在項目的類別。<br /><br /> 100 = 伺服器<br /><br /> 101 = 伺服器-主體<br /><br /> 105 = 端點|  
|**class_desc**|**nvarchar(60)**|權限所在類別的描述。 下列其中一個值：<br /><br /> **伺服器**<br /><br /> **SERVER_PRINCIPAL**<br /><br /> **端點**|  
|**major_id**|**int**|權限所在安全性實體的識別碼，它是根據類別加以解譯。 對大部份的項目來說，這只是套用至類別代表的識別碼。 下面是非標準的解譯：<br /><br /> 100 = 一律為0|  
|**minor_id**|**int**|權限所在項目的次要識別碼，它是根據類別加以解譯。|  
|**grantee_principal_id**|**int**|獲授與權限的伺服器主體識別碼。|  
|**grantor_principal_id**|**int**|這些權限之同意授權者的伺服器主體識別碼。|  
|**type**|**char (4)**|伺服器權限類型。 如需權限類型的清單，請參閱下表。|  
|**permission_name**|**nvarchar(128)**|權限名稱。|  
|**state**|**char(1)**|權限狀態：<br /><br /> D = 拒絕<br /><br /> R = 撤銷<br /><br /> G = 授與<br /><br /> W = 以授與選項授與|  
|**state_desc**|**nvarchar(60)**|權限狀態的描述：<br /><br /> 拒絕<br /><br /> REVOKE<br /><br /> GRANT<br /><br /> GRANT_WITH_GRANT_OPTION|  
  
|權限類型|權限名稱|適用於安全性實體|  
|---------------------|---------------------|--------------------------|  
|AAES|ALTER ANY EVENT SESSION|SERVER|
|ADBO|ADMINISTER BULK OPERATIONS|SERVER|  
|AL|ALTER|ENDPOINT、LOGIN|  
|ALAA|ALTER ANY SERVER AUDIT|SERVER|
|ALAG|ALTER ANY AVAILABILITY GROUP|SERVER|
|ALCD|ALTER ANY CREDENTIAL|SERVER|  
|ALCO|ALTER ANY CONNECTION|SERVER|  
|ALDB|ALTER ANY DATABASE|SERVER|  
|ALES|ALTER ANY EVENT NOTIFICATION|SERVER|  
|ALHE|ALTER ANY ENDPOINT|SERVER|  
|ALLG|ALTER ANY LOGIN|SERVER|  
|ALLS|ALTER ANY LINKED SERVER|SERVER|  
|ALRS|ALTER RESOURCES|SERVER|
|ALSR|ALTER ANY SERVER ROLE|SERVER|  
|ALSS|ALTER SERVER STATE|SERVER|  
|ALST|ALTER SETTINGS|SERVER|  
|ALTR|ALTER TRACE|SERVER|  
|AUTH|AUTHENTICATE SERVER|SERVER|
|CADB|CONNECT ANY DATABASE|SERVER|  
|CL|CONTROL|ENDPOINT、LOGIN|  
|CL|CONTROL SERVER|SERVER|  
|CO|CONNECT|端點|  
|COSQ|CONNECT SQL|SERVER|
|CRAC|CREATE AVAILABILITY GROUP|SERVER|  
|CRDB|CREATE ANY DATABASE|SERVER|  
|CRDE|CREATE DDL EVENT NOTIFICATION|SERVER|  
|CRHE|CREATE ENDPOINT|SERVER|
|CRSR|CREATE SERVER ROLE|SERVER|  
|CRTE|CREATE TRACE EVENT NOTIFICATION|SERVER|
|IAL|IMPERSONATE ANY LOGIN|SERVER|  
|IM|IMPERSONATE|LOGIN|  
|SHDN|SHUTDOWN|SERVER|
|SUS|SELECT ALL USER SECURABLES|SERVER|
|TO|TAKE OWNERSHIP|端點|  
|VW|VIEW DEFINITION|ENDPOINT、LOGIN|  
|VWAD|VIEW ANY DEFINITION|SERVER|  
|VWDB|VIEW ANY DATABASE|SERVER|  
|VWSS|VIEW SERVER STATE|SERVER|  
|XA|EXTERNAL ACCESS|SERVER|
|XU|UNSAFE ASSEMBLY|SERVER|
  
## <a name="permissions"></a>權限  
 任何使用者都可以查看他們自己的權限。 若要查看其他登入的權限，則需要 VIEW DEFINITION、ALTER ANY LOGIN 或登入的任何權限。 若要查看使用者定義伺服器角色，則需要 ALTER ANY SERVER ROLE 或該角色的成員資格。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
 下列查詢會列出已明確授與或拒絕伺服器主體的權限。  
  
> [!IMPORTANT]  
> 固定伺服器角色的權限並未出現在 sys.server_permissions 中。 因此，伺服器主體可能仍有其他未列於此處的權限。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pe.state_desc, pe.permission_name   
FROM sys.server_principals AS pr   
JOIN sys.server_permissions AS pe   
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [安全性實體](../../relational-databases/security/securables.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [權限階層 &#40;Database Engine&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
