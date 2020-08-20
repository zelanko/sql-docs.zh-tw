---
description: sp_addscriptexec (Transact-SQL)
title: sp_addscriptexec (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords:
- sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a133709a8fbaaabd58a9ad00d7298bf34317b0cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486315"
---
# <a name="sp_addscriptexec-transact-sql"></a>sp_addscriptexec (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將 SQL 指令碼 (.sql 檔) 公佈到發行集的所有訂閱者。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addscriptexec [ @publication = ] publication  
    [ , [ @scriptfile = ] 'scriptfile' ]  
    [ , [ @skiperror = ] 'skiperror' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @scriptfile = ] 'scriptfile'` 這是 SQL 腳本檔案的完整路徑。 *scriptfile* 是 **Nvarchar (4000) **，沒有預設值。  
  
`[ @skiperror = ] 'skiperror'` 指出當腳本處理期間發生錯誤時，散發代理程式或合併代理程式是否應該停止。 *Skiperror 您使* 是 **bit**，預設值是0。  
  
 **0** = 代理程式將會停止。  
  
 **1** = 代理程式會繼續執行腳本，並忽略錯誤。  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  從發行者發行時，不應使用「*發行者*」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addscriptexec** 用於異動複寫和合併式複寫中。  
  
 **sp_addscriptexec** 不會用於快照式複寫。  
  
 若要使用 **sp_addscriptexec**， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶必須具有快照集位置的讀取和寫入權限，以及任何腳本儲存位置的讀取權限。  
  
 [Sqlcmd 公用程式](../../tools/sqlcmd-utility.md)是用來在「訂閱者」端執行腳本，而腳本則是在連接到訂閱資料庫時，在散發代理程式或合併代理程式所使用的安全性內容中執行。 當代理程式在舊版上執行時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，會使用 [osql 公用程式](../../tools/osql-utility.md) ，而非 [sqlcmd](../../tools/sqlcmd-utility.md)。  
  
 **sp_addscriptexec** 適用于將腳本套用至訂閱者，並使用 [sqlcmd](../../tools/sqlcmd-utility.md) 將腳本的內容套用至「訂閱者」。 不過，由於訂閱者組態可能會不同，因此，在公佈到發行者之前測試的指令碼仍可能在訂閱者中造成錯誤。 *skiperror 您使* 可讓散發代理程式或合併代理程式忽略錯誤，並繼續進行。 在執行**sp_addscriptexec**之前，請先使用[sqlcmd](../../tools/sqlcmd-utility.md)測試腳本。  
  
> [!NOTE]  
>  略過的錯誤會繼續記錄到代理程式記錄中，以便參考。  
  
 針對使用 FTP 進行快照集傳遞的發行集，使用 **sp_addscriptexec** 張貼腳本檔只支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_addscriptexec**。  
  
## <a name="see-also"></a>另請參閱  
 [在同步處理期間執行腳本 &#40;複寫 Transact-sql 程式設計&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [同步處理資料](../../relational-databases/replication/synchronize-data.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
