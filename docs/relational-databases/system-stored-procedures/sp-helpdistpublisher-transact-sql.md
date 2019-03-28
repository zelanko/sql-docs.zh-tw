---
title: sp_helpdistpublisher & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords:
- sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54222842aa51e6904944a8b97507a3368e144612
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526470"
---
# <a name="sphelpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  利用散發者來傳回發行者的屬性。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 是其屬性會傳回 「 發行者 」。 *發行者*已**sysname**，預設值是**%**。  
  
`[ @check_user = ] check_user` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|發行者的名稱。|  
|**distribution_db**|**sysname**|指定之發行者的散發資料庫。|  
|**security_mode**|**int**|安全性模式只供複寫代理程式用來連接佇列更新訂閱的發行者，或連接非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證|  
|**login**|**sysname**|登入名稱只供複寫代理程式用來連接佇列更新訂閱的發行者，或連接非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。|  
|**password**|**nvarchar(524)**|傳回的密碼 (以簡單加密形式)。 密碼為 NULL 的使用者以外**sysadmin**。|  
|**active**|**bit**|遠端發行者是否利用本機伺服器來作為散發者：<br /><br /> **0** = 否<br /><br /> **1** = 是|  
|**working_directory**|**nvarchar(255)**|工作目錄的名稱。|  
|**trusted**|**bit**|當發行者連接到散發者時，是否需要密碼。 針對[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]及更新版本中，這一律會傳回**0**，這表示，不需要密碼。|  
|**thirdparty_flag**|**bit**|發行集是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟用，或由協力廠商應用程式啟用：<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，oracle 或 Oracle Gateway 發行者。<br /><br /> **1** = 已與整合發行者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用第三方應用程式。|  
|**publisher_type**|**sysname**|發行者的類型；它可以是下列項目之一：<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE GATEWAY**|  
|**publisher_data_source**|**nvarchar(4000)**|發行者之 OLE DB 資料來源的名稱。|  
|**storage_connection_string**|**nvarchar(4000)**|工作目錄的儲存體存取金鑰時散發者 」 或 「 Azure SQL Database 中的發行者。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdistpublisher**用於所有類型的複寫。  
  
 **sp_helpdistpublisher**將不會顯示發行者登入，或在結果中的密碼設為非**sysadmin**登入。  
  
## <a name="permissions"></a>Permissions  
 成員**sysadmin**固定的伺服器角色可能會執行**sp_helpdistpublisher**任何使用本機伺服器為散發者的發行者。 成員**db_owner**固定的資料庫角色或**replmonitor**散發資料庫中的角色可能會執行**sp_helpdistpublisher**使用的任何發行者散發資料庫。 使用者在發行集存取清單指定發行集*發行者*可能會執行**sp_helpdistpublisher**。 如果*發行者*未指定，資訊會傳回所有發行者的使用者具有存取權限。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
