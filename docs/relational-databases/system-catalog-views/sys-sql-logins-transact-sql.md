---
title: sys.databases sql_logins （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_logins_TSQL
- sql_logins_TSQL
- sys.sql_logins
- sql_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_logins catalog view
ms.assetid: 0d9c5b09-86fe-40ff-baab-00b7c051402f
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c3dba46f4d0e2ecdebda13fe3fe9412219c2a755
ms.sourcegitcommit: f7af758b353b53ac3b596d79fd6e32ad7e1e61cf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/17/2020
ms.locfileid: "79448479"
---
# <a name="syssql_logins-transact-sql"></a>sys.sql_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  針對每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<繼承的資料行>**|--|繼承自**sys. server_principals**。|  
|**is_policy_checked**|**bit**|已經檢查密碼原則。|  
|**is_expiration_checked**|**bit**|已經檢查密碼逾期。|  
|**password_hash**|**Varbinary （256）**|SQL 登入密碼的雜湊。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，預存密碼資訊會使用加料式 (Salted) 密碼的 SHA-512 加以計算。|  
  
 如需此視圖所繼承之資料行的清單，請參閱[server_principals &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。 和`is_fixed_role`資料`owning_principal_id`行不會繼承自 sys. server_principals。
  
## <a name="remarks"></a>備註  
 若要同時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查看驗證登入與 Windows 驗證登入，請參閱[sys.databases &#40;transact-sql&#41;server_principals ](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。  
  
 啟用自主資料庫使用者時，可以不進行登入來進行連接。 若要識別這些帳戶，請參閱[database_principals &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入都可以查看他們自己的登入名稱和 sa 登入。 若要查看其他登入，則需要 ALTER ANY LOGIN 或該登入的權限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的安全性目錄檢視](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [密碼原則](../../relational-databases/security/password-policy.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
