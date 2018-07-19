---
title: sp_dropserver (TRANSACT-SQL) |Microsoft 文件
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
- sp_dropserver_TSQL
- sp_dropserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropserver
ms.assetid: 0fc83e35-0caa-49a3-a4b6-a1890d4f46ef
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 82f030a0f35a75bb1494035c9db8cd0ae0f002c0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38049336"
---
# <a name="spdropserver-transact-sql"></a>sp_dropserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體上的已知遠端和連結伺服器清單中移除伺服器。  
  
[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropserver [ @server = ] 'server'   
     [ , [ @droplogins = ] { 'droplogins' | NULL} ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@server =** ] **'***server***'**  
 這是要移除的伺服器。 *server* 是 **sysname**，沒有預設值。 *伺服器*必須存在。  
  
 [  **@droplogins =** ] **'droplogins'** |NULL  
 指出相關遠端和連結伺服器登入*伺服器*也必須移除如果**droplogins**指定。 **@droplogins** 已**char(10)**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 如果您執行**sp_dropserver**有相關聯的遠端和連結伺服器登入項目，或設定為複寫發行者的伺服器上傳回錯誤訊息。 當您移除伺服器時，請移除所有的遠端和連結伺服器登入伺服器，請使用**droplogins**引數。  
  
 **sp_dropserver**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 ALTER ANY LINKED SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體移除遠端伺服器 `ACCOUNTS` 和所有相關聯的遠端登入。  
  
```  
sp_dropserver 'ACCOUNTS', 'droplogins';  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addserver &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpremotelogin &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
