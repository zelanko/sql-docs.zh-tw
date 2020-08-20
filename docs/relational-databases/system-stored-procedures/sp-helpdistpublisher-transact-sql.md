---
description: sp_helpdistpublisher (Transact-SQL)
title: sp_helpdistpublisher (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cb9bfd2bebe5220d992b92251c79df957f3d7077
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474075"
---
# <a name="sp_helpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  利用散發者來傳回發行者的屬性。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 這是傳回屬性的發行者。 *publisher* 是 **sysname**，預設值是 **%** 。  
  
`[ @check_user = ] check_user` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|發行者的名稱。|  
|**distribution_db**|**sysname**|指定之發行者的散發資料庫。|  
|**security_mode**|**int**|安全性模式只供複寫代理程式用來連接佇列更新訂閱的發行者，或連接非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證<br /><br /> **1** = Windows 驗證|  
|**登錄**|**sysname**|登入名稱只供複寫代理程式用來連接佇列更新訂閱的發行者，或連接非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。|  
|**password**|**Nvarchar (524) **|傳回的密碼 (以簡單加密形式)。 **系統管理員（sysadmin**）以外的使用者的密碼為 Null。|  
|**active**|**bit**|遠端發行者是否利用本機伺服器來作為散發者：<br /><br /> **0** = 否<br /><br /> **1** = 是|  
|**working_directory**|**nvarchar(255)**|工作目錄的名稱。|  
|**trusted**|**bit**|當發行者連接到散發者時，是否需要密碼。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 在和更新版本中，這一律會傳回**0**，表示需要密碼。|  
|**thirdparty_flag**|**bit**|發行集是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟用，或由協力廠商應用程式啟用：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、oracle 或 oracle Gateway 發行者。<br /><br /> **1** = 發行者已與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用協力廠商應用程式整合。|  
|**publisher_type**|**sysname**|發行者的類型；它可以是下列項目之一：<br /><br /> **MSSQLSERVER**<br /><br /> **甲骨文**<br /><br /> **ORACLE GATEWAY**|  
|**publisher_data_source**|**nvarchar(4000)**|發行者之 OLE DB 資料來源的名稱。|  
|**storage_connection_string**|**nvarchar(4000)**|Azure SQL Database 中的「散發者」或「發行者」時，工作目錄的儲存體存取金鑰。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helpdistpublisher** 用於所有類型的複寫中。  
  
 **sp_helpdistpublisher** 不會在非**系統管理員（sysadmin** ）登入的結果集中顯示發行者登入或密碼。  
  
## <a name="permissions"></a>權限  
 **系統管理員（sysadmin** ）固定伺服器角色的成員，可以使用本機伺服器作為散發者來執行任何發行者的**sp_helpdistpublisher** 。 在散發資料庫中， **db_owner** 固定資料庫角色或 **replmonitor** 角色的成員，可能會使用該散發資料庫來執行任何發行者的 **sp_helpdistpublisher** 。 指定 *發行者* 端之發行集的發行集存取清單中的使用者，可能會執行 **sp_helpdistpublisher**。 如果未指定 *publisher* ，則會傳回使用者有權存取之所有發行者的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
