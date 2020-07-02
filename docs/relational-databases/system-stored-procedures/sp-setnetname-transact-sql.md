---
title: sp_setnetname （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setnetname
- sp_setnetname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setnetname
ms.assetid: f416ba81-3835-4588-b0a3-2fe75589490e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 140765eacad1d035f9e8640330701711a358991b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719204"
---
# <a name="sp_setnetname-transact-sql"></a>sp_setnetname (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  將**sys.databases**中的網路名稱設定為遠端實例的實際網路電腦名稱稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這個程序可用來啟用對於網路名稱含有無效 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼之電腦的遠端預存程序呼叫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_setnetname  
@server = 'server',   
     @netname = 'network_name'  
```  
  
## <a name="arguments"></a>引數  
 ** @server = '** *server* **'**  
 這是使用者編寫的遠端預存程序呼叫語法所參考的遠端伺服器名稱。 在**sys.databases**中，只有一個資料列必須已經存在，才能使用此*伺服器*。 *server* 是 **sysname**，沒有預設值。  
  
 ** @netname = '** *network_name* **'**  
 這是遠端預存程序呼叫的目標電腦網路名稱。 *network_name*是**sysname**，沒有預設值。  
  
 這個名稱必須符合 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 電腦名稱，且這個名稱可以包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼不允許使用的字元。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 如果電腦名稱包含無效的識別碼，有些對 Windows 電腦的遠端預存程序呼叫可能會發生問題。  
  
 由於連結伺服器和遠端伺服器在相同命名空間中，因此，它們的名稱不能相同。 不過，您可以藉由指派不同的名稱，以及使用**sp_setnetname**將其中一個的網路名稱設定為基礎伺服器的網路名稱，為指定的伺服器定義連結伺服器和遠端伺服器。  
  
```  
--Assume sqlserv2 is actual name of SQL Server   
--database server  
EXEC sp_addlinkedserver 'sqlserv2';  
GO  
EXEC sp_addserver 'rpcserv2';  
GO  
EXEC sp_setnetname 'rpcserv2', 'sqlserv2';  
```  
  
> [!NOTE]  
>  不支援使用**sp_setnetname**將連結的伺服器指向本機伺服器。 這個方式所參考的伺服器無法參與分散式交易。  
  
## <a name="permissions"></a>權限  
 需要**sysadmin**和**setupadmin**固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上，用來發出遠端預存程序呼叫的一般管理順序。  
  
```  
USE master;  
GO  
EXEC sp_addserver 'Win_1';  
EXEC sp_setnetname 'Win_1','Win-1';  
EXEC Win_1.master.dbo.sp_who;  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
