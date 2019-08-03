---
title: sp_adddistpublisher (Transact-sql) |Microsoft Docs
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
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2190e31245cde19eca4c5a47f21ac48e12f57f53
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771393"
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  設定發行者來使用指定的散發資料庫。 這個預存程序執行於任何資料庫中的散發者端。 請注意, 在使用這個預存程式之前, 必須先執行[sp_adddistributor &#40; &#41; transact-sql](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)和[sp_adddistributiondb &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)的預存程式。  
  
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
`[ @publisher = ] 'publisher'`這是發行者名稱。 *publisher*是**sysname**, 沒有預設值。  
  
`[ @distribution_db = ] 'distribution_db'`這是散發資料庫的名稱。 *distributor_db*是**sysname**, 沒有預設值。 複寫代理程式利用這個參數來連接發行者。  
  
`[ @security_mode = ] security_mode`是實作為安全性模式。 此參數只供複寫代理程式用來連接佇列更新訂閱的發行者, 或使用非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *security_mode*是**int**, 而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|散發者的複寫代理程式利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接到發行者。|  
|**1** (預設值)|散發者的複寫代理程式利用 Windows 驗證來連接到發行者。|  
  
`[ @login = ] 'login'`這是登入。 如果*security_mode*為**0**, 則此為必要參數。 *login* 是預設值為 NULL 的 **sysname**。 複寫代理程式利用這個參數來連接發行者。  
  
`[ @password = ] 'password']`這是密碼。 *password*是**sysname**, 預設值是 Null。 複寫代理程式利用這個參數來連接發行者。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。  
  
`[ @working_directory = ] 'working_directory'`這是用來儲存發行集資料和架構檔案的工作目錄名稱。 *working_directory*是**Nvarchar (255)** , 預設為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]這個實例的 ReplData 資料夾, `C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData`例如。 這個名稱應該用 UNC 格式來指定。  

 針對 Azure SQL Database, 請`\\<storage_account>.file.core.windows.net\<share>`使用。

`[ @storage_connection_string = ] 'storage_connection_string'`SQL Database 需要。 使用 Azure 入口網站的 [儲存體] > [設定] 底下的 [存取金鑰]。

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]

`[ @trusted = ] 'trusted'`這個參數已被取代, 而且是為了回溯相容性而提供。 *trusted*是**Nvarchar (5)** , 並將它設定為**false**以外的任何專案, 將會導致錯誤。  
  
`[ @encrypted_password = ] encrypted_password`已不再支援設定*encrypted_password* 。 嘗試將此**位**參數設定為**1**將會導致錯誤。  
  
`[ @thirdparty_flag = ] thirdparty_flag`當發行者為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時。 *thirdparty_flag*是**bit**, 它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**1**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外的資料庫。|  
  
`[ @publisher_type = ] 'publisher_type'`指定發行者不[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是時的發行者類型。 *publisher_type*是 sysname, 它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (預設值)|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。|  
|**ORACLE**|指定標準 Oracle 發行者。|  
|**ORACLE 閘道**|指定 Oracle Gateway 發行者。|  
  
 如需有關「Oracle 發行者」與「Oracle 閘道發行者」之間差異的詳細資訊, 請參閱[設定 Oracle 發行者](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_adddistpublisher**是由快照式複寫、異動複寫和合併式複寫所使用。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有**系統管理員 (sysadmin** ) 固定伺服器角色的成員, 才能夠執行**sp_adddistpublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)  
  
  
