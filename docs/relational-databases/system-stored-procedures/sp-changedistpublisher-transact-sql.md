---
title: "sp_changedistpublisher (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords: sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c462e73fd9a99d8645d752aaac86b5207e7c0722
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
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
```  
  
## <a name="arguments"></a>引數  
 [  **@publisher=** ] **'***發行者***'**  
 這是發行者名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@property=** ] **'***屬性***'**  
 這是要變更之給定發行者的屬性。 *屬性*是**sysname**而且可以是下列值之一。  
  
 [ **@value=** ] **'***value***'**  
 這是指定屬性的值。 *值*是**nvarchar （255)**，預設值是 NULL。  
  
 下表描述發行者的屬性及這些屬性的值。  
  
|屬性|值|Description|  
|--------------|------------|-----------------|  
|**使用中**|**true**|啟動發行者。|  
||**false**|停用發行者|  
|**distribution_db**||散發資料庫的名稱。|  
|**登入**||登入名稱。|  
|**密碼**||提供之登入的增強式密碼。|  
|**security_mode**|**1**|當連接到發行者時，使用 Windows 驗證。 *無法變更非*[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *發行者。*|  
||**0**|當連接到發行者時，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 *無法變更非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *發行者。*|  
|**working_directory**||用來儲存發行集資料和結構描述檔案的工作目錄。|  
|NULL (預設值)||所有可用*屬性*列印選項。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changedistpublisher**用於所有複寫類型。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_changedistpublisher**。  
  
## <a name="see-also"></a>請參閱＜  
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
