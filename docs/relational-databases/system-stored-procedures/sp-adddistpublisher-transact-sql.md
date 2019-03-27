---
title: sp_adddistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistpublisher
- sp_adddistpublisher_TSQL
helpviewer_keywords:
- sp_adddistpublisher
ms.assetid: 04e15011-a902-4074-b38c-3ec2fc73b838
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c01d00362dc55deb1fa9da8df49beebdaf82b170
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492770"
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  設定發行者來使用指定的散發資料庫。 這個預存程序執行於任何資料庫中的散發者端。 請注意，預存程序[sp_adddistributor &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)並[sp_adddistributiondb &#40;-&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)必須執行才能使用此預存程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_adddistpublisher [ @publisher= ] 'publisher'   
        , [ @distribution_db= ] 'distribution_db'   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @working_directory= ] 'working_directory' ]   
    [ , [ @storage_connection_string= ] 'storage_connection_string']
    [ , [ @trusted= ] 'trusted' ]   
    [ , [ @encrypted_password= ] encrypted_password ]   
    [ , [ @thirdparty_flag = ] thirdparty_flag ]  
    [ , [ @publisher_type = ] 'publisher_type' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 這是發行者名稱。 *發行者*已**sysname**，沒有預設值。  
  
`[ @distribution_db = ] 'distribution_db'` 是散發資料庫的名稱。 *distributor_db*已**sysname**，沒有預設值。 複寫代理程式利用這個參數來連接發行者。  
  
`[ @security_mode = ] security_mode` 是實作的安全性模式。 這個參數只由複寫代理程式用來連接到發行者之佇列更新訂閱，或與非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *security_mode*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|散發者的複寫代理程式利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接到發行者。|  
|**1** (預設值)|散發者的複寫代理程式利用 Windows 驗證來連接到發行者。|  
  
`[ @login = ] 'login'` 是登入。 如果此參數，則需要*security_mode*是**0**。 *login* 是預設值為 NULL 的 **sysname**。 複寫代理程式利用這個參數來連接發行者。  
  
`[ @password = ] 'password']` 這是密碼。 *密碼*已**sysname**，預設值是 NULL。 複寫代理程式利用這個參數來連接發行者。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。  
  
`[ @working_directory = ] 'working_directory'` 是用來儲存發行集的資料和結構描述檔案的工作目錄的名稱。 *working_directory*已**nvarchar(255)**，預設值是 ReplData 資料夾，這個執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，例如`C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData`。 這個名稱應該用 UNC 格式來指定。  

 針對 Azure SQL Database，使用`\\<storage_account>.file.core.windows.net\<share>`。

`[ @storage_connection_string = ] 'storage_connection_string'` 需要 SQL Database。 使用儲存體存取金鑰從 Azure 入口網站 > 設定。

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]

`[ @trusted = ] 'trusted'` 這個參數已被取代，並提供回溯相容性。 *受信任*是**nvarchar(5)**，並設定為任何內容，不過**false**會導致錯誤。  
  
`[ @encrypted_password = ] encrypted_password` 設定*encrypted_password*不受支援。 嘗試將這個**位元**參數來**1**會導致錯誤。  
  
`[ @thirdparty_flag = ] thirdparty_flag` 當 「 發行者 」 時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 *thirdparty_flag*已**元**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**1**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外的資料庫。|  
  
`[ @publisher_type = ] 'publisher_type'` 當發行者不是指定的發行者類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 *publisher_type*是 sysname，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (預設值)|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。|  
|**ORACLE**|指定標準 Oracle 發行者。|  
|**ORACLE GATEWAY**|指定 Oracle Gateway 發行者。|  
  
 如需有關 Oracle 發行者 」 與 「 Oracle Gateway 發行者之間的差異的詳細資訊，請參閱 <<c0> [ 設定 Oracle 發行者](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
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
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)  
  
  
