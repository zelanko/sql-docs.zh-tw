---
title: sp_addscriptexec (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: e8ae792ba7f8422e841abbbe2f80b096497df993
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022455"
---
# <a name="spaddscriptexec-transact-sql"></a>sp_addscriptexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @scriptfile = ] 'scriptfile'` 是 SQL 指令碼檔案的完整路徑。 *scriptfile*已**nvarchar(4000)** ，沒有預設值。  
  
`[ @skiperror = ] 'skiperror'` 表示指令碼處理期間發生錯誤時的散發代理程式 」 或 「 合併代理程式是否應該停止。 *SkipError*已**元**，預設值是 0。  
  
 **0** = 代理程式將會停止。  
  
 **1** = 代理程式會繼續指令碼，並忽略錯誤。  
  
`[ @publisher = ] 'publisher'` 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應從發佈時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addscriptexec**使用異動複寫與合併式複寫中。  
  
 **sp_addscriptexec**不適用於快照式複寫。  
  
 若要使用**sp_addscriptexec**，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶必須具有讀取和寫入權限的任何指令碼的位置的快照集位置] 及 [讀取權限會儲存。  
  
 [Sqlcmd 公用程式](../../tools/sqlcmd-utility.md)用來執行在訂閱者，指令碼，並連接到訂閱資料庫時，散發代理程式或合併代理程式所使用的安全性內容中執行指令碼。 在舊版上執行代理程式時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則[osql 公用程式](../../tools/osql-utility.md)而非[sqlcmd](../../tools/sqlcmd-utility.md)。  
  
 **sp_addscriptexec**可用於將指令碼套用至訂閱者，並使用[sqlcmd](../../tools/sqlcmd-utility.md)来套用到訂閱者的指令碼的內容。 不過，由於訂閱者組態可能會不同，因此，在公佈到發行者之前測試的指令碼仍可能在訂閱者中造成錯誤。 *skiperror*讓您能夠有散發代理程式或合併代理程式忽略錯誤並繼續。 使用[sqlcmd](../../tools/sqlcmd-utility.md)測試之前執行的指令碼**sp_addscriptexec**。  
  
> [!NOTE]  
>  略過的錯誤會繼續記錄到代理程式記錄中，以便參考。  
  
 使用**sp_addscriptexec**公佈以 FTP 傳遞快照集才支援的發行集的指令碼檔案[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addscriptexec**。  
  
## <a name="see-also"></a>另請參閱  
 [同步處理期間執行指令碼&#40;複寫 TRANSACT-SQL 程式設計&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [同步處理資料](../../relational-databases/replication/synchronize-data.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
