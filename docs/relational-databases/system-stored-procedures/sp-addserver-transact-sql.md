---
title: sp_addserver (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addserver
- sp_addserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addserver
- renaming servers
- machine names [SQL Server]
- computer names
ms.assetid: 160a6b29-5e80-44ab-80ec-77d4280f627c
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4263ae95f80518504fca71cf5622b4d3c65c850b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spaddserver-transact-sql"></a>sp_addserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  定義的本機執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 當電腦裝載[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是重新命名，使用**sp_addserver**通知的執行個體[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]新電腦名稱。 此程序必須在電腦上裝載的所有 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體上執行。 執行個體名稱[!INCLUDE[ssDE](../../includes/ssde-md.md)]無法變更。 若要變更具名執行個體的執行個體名稱，請安裝具有所需名稱的新執行個體、從舊的執行個體卸離資料庫檔案、將資料庫附加到新的執行個體，和卸除舊的執行個體。 或者，您可以在用戶端電腦上建立用戶端別名名稱，將連接重新導向至不同的伺服器和執行個體名稱或 **伺服器：連接埠** 的組合，而不需要變更伺服器電腦上的執行個體名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addserver [ @server = ] 'server' ,  
     [ @local = ] 'local'   
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@server =** ] **'***server***'**  
 這是伺服器的名稱。 伺服器名稱必須是唯一，並且遵照 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 電腦名稱的規則 (但不能加空格)。 *server* 是 **sysname**，沒有預設值。  
  
 當多個執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已安裝的電腦上，執行個體就好像它是不同的伺服器上。 透過將指定的具名執行個體*伺服器*為*servername\instancename*。  
  
 [ **@local =** ] **'LOCAL'**  
 將正在加入的伺服器指定為本機伺服器。 **@local** 是**varchar （10)**，預設值是 NULL。 指定**@local**為**本機**定義**@server**做為名稱的本機伺服器和原因 @@SERVERNAME函式傳回值*伺服器*。  
  
 在安裝時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會將這個變數設為電腦名稱。 根據預設，電腦名稱是使用者的方式連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不用其他組態。  
  
 本機定義在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 重新啟動之後才會生效。 每個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體只能定義一部本機伺服器。  
  
 [ **@duplicate_ok =** ] **'duplicate_OK'**  
 指定是否允許重複的伺服器名稱。 **@duplicate_OK** 是**varchar(13)**，預設值是 NULL。 **@duplicate_OK** 只能有值**duplicate_OK**或 NULL。 如果**duplicate_OK**指定且已加入的伺服器名稱存在，不會引發錯誤。 如果沒有使用具名的參數， **@local**必須指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 若要設定或清除伺服器選項，請使用**sp_serveroption**。  
  
 **sp_addserver**不能用在使用者自訂交易內。  
  
 使用**sp_addserver**新增遠端伺服器已停止。 請改用 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 。  
  
## <a name="permissions"></a>Permissions  
  需要 setupadmin 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會變更[!INCLUDE[ssDE](../../includes/ssde-md.md)]裝載電腦的名稱的項目[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至`ACCOUNTS`。  
  
```  
sp_addserver 'ACCOUNTS', 'local';  
```  
  
## <a name="see-also"></a>另請參閱  
 [重新命名主控 SQL Server 獨立執行個體的電腦](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropserver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_helpserver & #40;TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
