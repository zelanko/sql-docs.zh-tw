---
title: sp_adddistpublisher (TRANSACT-SQL) |Microsoft 文件
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
- sp_adddistpublisher
- sp_adddistpublisher_TSQL
helpviewer_keywords:
- sp_adddistpublisher
ms.assetid: 04e15011-a902-4074-b38c-3ec2fc73b838
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3ccd9c550df21ea904c4ff8d8c7a3941908e59a2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定發行者來使用指定的散發資料庫。 這個預存程序執行於任何資料庫中的散發者端。 請注意，預存程序[sp_adddistributor &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)和[sp_adddistributiondb &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)必須使用此預存之前執行程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_adddistpublisher [ @publisher= ] 'publisher'   
        , [ @distribution_db= ] 'distribution_db'   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @working_directory= ] 'working_directory' ]   
    [ , [ @trusted= ] 'trusted' ]   
    [ , [ @encrypted_password= ] encrypted_password ]   
    [ , [ @thirdparty_flag = ] thirdparty_flag ]  
    [ , [ @publisher_type = ] 'publisher_type' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher=**] **'***publisher***'**  
 這是發行者名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@distribution_db=**] **'***distribution_db***'**  
 這是散發資料庫的名稱。 *distributor_db*是**sysname**，沒有預設值。 複寫代理程式利用這個參數來連接發行者。  
  
 [  **@security_mode=**] *security_mode*  
 這是實作的安全性模式。 此參數只供複寫代理程式用來連接佇列更新訂閱的發行者，或連接非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *security_mode*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|散發者的複寫代理程式利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接到發行者。|  
|**1** (預設值)|散發者的複寫代理程式利用 Windows 驗證來連接到發行者。|  
  
 [  **@login=**] **'***登入***'**  
 這是登入。 如果這個參數，則需要*security_mode*是**0**。 *login* 是預設值為 NULL 的 **sysname**。 複寫代理程式利用這個參數來連接發行者。  
  
 [  **@password=**] **'***密碼***'**]  
 這是密碼。 *密碼*是**sysname**，預設值是 NULL。 複寫代理程式利用這個參數來連接發行者。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。  
  
 [  **@working_directory=**] **'***working_directory***'**  
 這是用來儲存發行集資料和結構描述檔案的工作目錄名稱。 *working_directory*是**nvarchar （255)**，預設值是 ReplData 資料夾，這個執行個體和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，例如，' C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData'。 這個名稱應該用 UNC 格式來指定。  
  
 [  **@trusted=**] **'***信任***'**  
 這個參數已被取代，而且僅供回溯相容性之用。 *受信任*是**nvarchar （5)**，並將它設為以外**false**會導致錯誤。  
  
 [  **@encrypted_password=**] *encrypted_password*  
 設定*encrypted_password*不再支援。 嘗試將這個**元**參數**1**會導致錯誤。  
  
 [  **@thirdparty_flag =**] *thirdparty_flag*  
 這是指發行者是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的情況。 *thirdparty_flag*是**元**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**0** (預設)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**1**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外的資料庫。|  
  
 [ **@publisher_type**=] **'***publisher_type***'**  
 指定當發行者不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時的發行者類型。 *publisher_type*是 sysname，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (預設值)|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。|  
|**ORACLE**|指定標準 Oracle 發行者。|  
|**ORACLE GATEWAY**|指定 Oracle Gateway 發行者。|  
  
 如需有關 Oracle 發行者和 Oracle Gateway 發行者之間的差異的詳細資訊，請參閱[設定 Oracle 發行者](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_adddistpublisher**供快照式複寫、 異動複寫和合併式複寫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_adddistpublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)  
  
  
