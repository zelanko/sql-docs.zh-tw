---
title: sp_addremotelogin (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ec988334611350fdf736b69100b27d79d5374342
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238818"
---
# <a name="spaddremotelogin-transact-sql"></a>sp_addremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在本機伺服器上加入新的遠端登入識別碼。 此舉可讓遠端伺服器連接及執行遠端程序呼叫。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]請改用連結伺服器和連結伺服器預存程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @remoteserver **=** ] **'***remoteserver***'**  
 這是遠端登入所套用的遠端伺服器名稱。 *remoteserver*是**sysname**，沒有預設值。 如果只*remoteserver*指定，則所有使用者都*remoteserver*會對應至本機伺服器上相同名稱的現有登入。 本機伺服器必須知道這部伺服器。 這是由使用 sp_addserver 加入。 當使用者*remoteserver*連線到本機伺服器執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接自己的登入相符的本機登入為執行遠端預存程序， *remoteserver*. *remoteserver*是起始遠端程序呼叫的伺服器。  
  
 [ @loginame **=** ] **'***登入***'**  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體上的使用者登入識別碼。 *login* 是預設值為 NULL 的 **sysname**。 *登入*必須已存在於本機執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*登入*指定，則所有使用者都*remoteserver*會對應至該特定本機登入。 當使用者*remoteserver*連接到本機執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接做為執行遠端預存程序，*登入*。  
  
 [ @remotename **=** ] **'***remote_name***'**  
 這是遠端伺服器上的使用者登入識別碼。 *remote_name*是**sysname**，預設值是 NULL。 *remote_name*必須存在於*remoteserver*。 如果*remote_name*指定時，特定使用者*remote_name*對應至*登入*本機伺服器上。 當*remote_name*上*remoteserver*會連接到本機執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以執行遠端預存程序，它會連接做為*登入*。 登入識別碼*remote_name*可以不同於遠端伺服器上的登入識別碼*登入*。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 若要執行分散式的查詢，請使用 sp_addlinkedsrvlogin。  
  
 sp_addremotelogin 不能在使用者自訂交易內。  
  
## <a name="permissions"></a>Permissions  
 只有系統管理員和安全性管理員固定伺服器角色的成員可以執行 sp_addremotelogin。  
  
## <a name="examples"></a>範例  
  
### <a name="a-mapping-one-to-one"></a>A. 一對一對應  
 下列範例是在遠端伺服器 `ACCOUNTS` 和本機伺服器具有相同的使用者登入時，將遠端名稱對應至本機名稱。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-mapping-many-to-one"></a>B. 多對一對應  
 下列範例會建立一個項目，將遠端伺服器 `ACCOUNTS` 上所有的使用者，對應至本機登入識別碼 `Albert`。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-using-explicit-one-to-one-mapping"></a>C. 使用明確的一對一對應  
 下列範例會將來自遠端伺服器 `Chris` 上遠端使用者 `ACCOUNTS` 的遠端登入，對應至本機使用者 `salesmgr`。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_addlinkedsrvlogin &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addserver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver & #40;TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
