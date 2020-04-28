---
title: sp_changedistpublisher （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 80eb30fc6b6b2cea9fc058780831af3915fd9007
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771358"
---
# <a name="sp_changedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  變更散發發行者的屬性。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @storage_connection_string = ] 'storage_connection_string']
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是發行者名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @property = ] 'property'`這是要針對給定發行者變更的屬性。 *屬性*是**sysname** ，而且可以是下列其中一個值。  
  
`[ @value = ] 'value'`這是指定之屬性的值。 *value*是**Nvarchar （255）**，預設值是 Null。  
  
`[ @storage_connection_string = ] 'storage_connection_string'`SQL Database 受控實例必須符合 Azure SQL Database 存放磁片區的存取金鑰。 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 下表描述發行者的屬性及這些屬性的值。  
  
|屬性|值|描述|  
|--------------|------------|-----------------|  
|**作用中**|**true**|啟動發行者。|  
||**false**|停用發行者|  
|**distribution_db**||散發資料庫的名稱。|  
|**login**||登入名稱。|  
|**password**||提供之登入的增強式密碼。|  
|**security_mode**|**1**|當連接到發行者時，使用 Windows 驗證。 *這無法針對非*[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *發行者*進行變更。|  
||**0**|當連接到發行者時，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 *這無法針對非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *發行者*進行變更。|  
|**working_directory**||用來儲存發行集資料和結構描述檔案的工作目錄。|  
|NULL (預設值)||所有可用的*屬性*選項都會列印出來。| 
|**storage_connection_string**| 存取金鑰 | 當資料庫 Azure SQL Database 受控執行個體時，工作目錄的存取金鑰。 
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changedistpublisher**用於所有類型的複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_changedistpublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [查看和修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
