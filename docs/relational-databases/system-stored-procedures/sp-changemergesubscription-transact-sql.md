---
title: sp_changemergesubscription (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_changemergesubscription_TSQL
- sp_changemergesubscription
helpviewer_keywords:
- sp_changemergesubscription
ms.assetid: fd820f35-c189-4e2d-884d-b60c1c469f58
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eda4f52de6d6b072f8250a00dcff82623badb43c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spchangemergesubscription-transact-sql"></a>sp_changemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更合併發送訂閱的所選屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changemergesubscription [ [ @publication= ] 'publication' ]  
    [ , [ @subscriber= ] 'subscriber'  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 這是要變更的發行集名稱。 *發行集*是**sysname**，預設值是 NULL。 發行集必須已存在，且必須符合識別碼的規則。  
  
 [  **@subscriber=**] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 NULL。  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，預設值是 NULL。  
  
 [  **@property=**] **'***屬性***'**  
 這是給定發行集要變更的屬性。 *屬性*是**sysname**，而且可以是下列其中一個資料表中的值。  
  
 [  **@value=**] **'***值***'**  
 指定的新值*屬性*。 *值*是**nvarchar （255)**，而且可以是下列其中一個資料表中的值。  
  
|屬性|Value|Description|  
|--------------|-----------|-----------------|  
|**描述**||這個合併訂閱的描述。|  
|**priority**||這是訂閱優先權。 在偵測到衝突時，預設解析程式會利用優先權挑選贏的一方。|  
|**merge_job_login**||用來執行代理程式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的登入。|  
|**merge_job_password**||用來執行代理程式之 Windows 帳戶的密碼。|  
|**publisher_security_mode**|**1**|當連接到發行者時，使用 Windows 驗證。|  
||**0**|當連接到發行者時，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。|  
|**publisher_login**||發行者的登入名稱。|  
|**publisher_password**||提供之發行者登入的增強式密碼。|  
|**subscriber_security_mode**|**1**|當連接到發行者時，使用 Windows 驗證。|  
||**0**|當連接到訂閱者時，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。|  
|**subscriber_login**||訂閱者的登入名稱。|  
|**subscriber_password**||提供之訂閱者登入的增強式密碼。|  
|**sync_type**|**自動**|先將發行資料表的結構描述和初始資料傳送給訂閱者。|  
||**無**|訂閱者已有發行資料表的結構描述和初始資料；一律會傳送系統資料表和資料。|  
|**use_interactive_resolver**|**true**|可讓您以互動方式來解決接受互動式解決之所有發行項的衝突。|  
||**false**|衝突是利用預設解析程式或自訂解析程式加以自動解析。|  
|NULL (預設值)|NULL (預設值)||  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changemergesubscription**用於合併式複寫中。  
  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_changemergesubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addmergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
