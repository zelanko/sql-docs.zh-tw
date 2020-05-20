---
title: sp_addserver （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8578cccba27f38999ef786e1fb48b46445ad682c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833649"
---
# <a name="sp_addserver-transact-sql"></a>sp_addserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]定義  本機執行個體的名稱。 當主控的電腦重新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名時，請使用**sp_addserver**來通知實例的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 新電腦名稱稱。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 此程序必須在電腦上裝載的所有  執行個體上執行。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 無法變更  的執行個體名稱。 若要變更具名執行個體的執行個體名稱，請安裝具有所需名稱的新執行個體、從舊的執行個體卸離資料庫檔案、將資料庫附加到新的執行個體，和卸除舊的執行個體。 或者，您可以在用戶端電腦上建立用戶端別名名稱，將連接重新導向至不同的伺服器和執行個體名稱或 **伺服器：連接埠** 的組合，而不需要變更伺服器電腦上的執行個體名稱。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>語法

```

sp_addserver [ @server = ] 'server' ,
     [ @local = ] 'local' 
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]
```

## <a name="arguments"></a>引數
`[ @server = ] 'server'`這是伺服器的名稱。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 伺服器名稱必須是唯一，並且遵照  Windows 電腦名稱的規則 (但不能加空格)。 *server* 是 **sysname**，沒有預設值。

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當您在一部電腦安裝多個  執行個體時，每一個執行個體的運作方式，就好像分別位於不同的伺服器上。 藉由將*伺服器*參考為*servername\instancename*，指定已命名的實例。

`[ @local = ] 'LOCAL'`指定要加入做為本機伺服器的伺服器。 ** \@ local**是**Varchar （10）**，預設值是 Null。 指定** \@ local**做**為 local 會**將** \@ server**定義為本機伺服器的名稱，並讓 @ @SERVERNAME 函數傳回*伺服器*的值。

 在安裝時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會將這個變數設為電腦名稱。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 依預設，電腦名稱是使用者在不用其他組態的情況下，連接  執行個體的方法。

 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 本機定義在  重新啟動之後才會生效。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]每個  執行個體只能定義一部本機伺服器。

`[ @duplicate_ok = ] 'duplicate_OK'`指定是否允許重複的伺服器名稱。 ** \@ duplicate_OK**是**Varchar （13）**，預設值是 Null。 ** \@ duplicate_OK**只能有**duplicate_OK**或 Null 值。 如果指定了**duplicate_OK** ，而且要新增的伺服器名稱已經存在，就不會產生錯誤。 如果未使用具名引數，則必須指定** \@ local** 。

## <a name="return-code-values"></a>傳回碼值
 0 (成功) 或 1 (失敗)

## <a name="remarks"></a>備註
 若要設定或清除伺服器選項，請使用**sp_serveroption**。

 **sp_addserver**不能在使用者自訂交易內使用。

 使用**sp_addserver**新增遠端伺服器已停止。 請改用 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 。

## <a name="permissions"></a>權限
 **** 需要 setupadmin 固定伺服器角色中的成員資格。

## <a name="examples"></a>範例
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 下列範例將裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦名稱的 `ACCOUNTS`項目變更為 。

```
sp_addserver 'ACCOUNTS', 'local';
```

## <a name="see-also"></a>另請參閱
 [重新命名裝載 SQL Server sp_addlinkedserver 之獨立實例的電腦](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) [&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) [sp_dropserver](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md) &#40;Transact-sql [&#41;sp_helpserver transact-sql](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md) &#40;[系統預存程式&#41;transact-sql &#40;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) [安全性預存](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)程式&#41;transact-sql &#40;


