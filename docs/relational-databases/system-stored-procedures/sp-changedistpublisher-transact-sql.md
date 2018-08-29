---
title: sp_changedistpublisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42d4f622da4696f5dd053ce03a3ade1a03e52273
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038621"
---
# <a name="spchangedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [  **@publisher=** ] **'***發行者***'**  
 這是發行者名稱。 *發行者*已**sysname**，沒有預設值。  
  
 [  **@property=** ] **'***屬性***'**  
 這是要變更之給定發行者的屬性。 *屬性*已**sysname**而且可以是下列值之一。  
  
 [ **@value=** ] **'***value***'**  
 這是指定屬性的值。 *值*已**nvarchar(255)**，預設值是 NULL。  
  
 [  **@storage_connection_string =**] **'***storage_connection_string***'**  
 需要 SQL Database 受控執行個體，應該符合 Azure SQL Database 的存放磁碟區的存取金鑰。 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 下表描述發行者的屬性及這些屬性的值。  
  
|屬性|值|描述|  
|--------------|------------|-----------------|  
|**使用中**|**true**|啟動發行者。|  
||**false**|停用發行者|  
|**distribution_db**||散發資料庫的名稱。|  
|**login**||登入名稱。|  
|**password**||提供之登入的增強式密碼。|  
|**security_mode**|**1**|當連接到發行者時，使用 Windows 驗證。 *無法變更為非*[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *發行者。*|  
||**0**|當連接到發行者時，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 *無法變更為非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *發行者。*|  
|**working_directory**||用來儲存發行集資料和結構描述檔案的工作目錄。|  
|NULL (預設值)||所有可用*屬性*列印選項。| 
|**storage_connection_string**| 存取金鑰 | 在資料庫是 Azure SQL Database 受控執行個體的工作目錄的存取金鑰。 
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changedistpublisher**用於所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_changedistpublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
