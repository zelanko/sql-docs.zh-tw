---
title: "sp_addscriptexec (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords: sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13f3104f91c785252f573e653d3344a03091dd13
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
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
 [  **@publication=** ] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@scriptfile=** ] **'***scriptfile***'**  
 這是 SQL 指令碼檔案的完整路徑。 *scriptfile*是**nvarchar （4000)**，沒有預設值。  
  
 [  **@skiperror=** ] **'***skiperror***'**  
 表示在指令碼處理期間發生錯誤時，是否應該停止散發代理程式或合併代理程式。 *SkipError*是**元**，預設值是 0。  
  
 **0** = 代理程式將會停止。  
  
 **1** = 代理程式會繼續指令碼，而且會忽略錯誤。  
  
 [  **@publisher=** ] **'***發行者***'**  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應從發行時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addscriptexec**異動複寫和合併式複寫中使用。  
  
 **sp_addscriptexec**不適用於快照式複寫。  
  
 若要使用**sp_addscriptexec**、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶必須具有讀取和寫入權限的快照集位置與讀取權限的任何指令碼的位置會儲存。  
  
 [Sqlcmd 公用程式](../../tools/sqlcmd-utility.md)用來執行指令碼，在訂閱者，並連接到訂閱資料庫時，散發代理程式或合併代理程式所使用的安全性內容中執行指令碼。 代理程式的舊版本上執行時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [osql 公用程式](../../tools/osql-utility.md)而非[sqlcmd](../../tools/sqlcmd-utility.md)。  
  
 **sp_addscriptexec**適用於將指令碼套用至訂閱者，並使用[sqlcmd](../../tools/sqlcmd-utility.md)来套用到訂閱者的指令碼內容。 不過，由於訂閱者組態可能會不同，因此，在公佈到發行者之前測試的指令碼仍可能在訂閱者中造成錯誤。 *skiperror*可讓您將散發代理程式或合併代理程式忽略錯誤並繼續。 使用[sqlcmd](../../tools/sqlcmd-utility.md)測試指令碼，再執行**sp_addscriptexec**。  
  
> [!NOTE]  
>  略過的錯誤會繼續記錄到代理程式記錄中，以便參考。  
  
 使用**sp_addscriptexec**公佈快照集傳遞只支援使用 FTP 的發行集的指令碼檔案[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 「 訂閱者 」。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addscriptexec**。  
  
## <a name="see-also"></a>請參閱＜  
 [在同步處理 &#40; 期間執行指令碼複寫 TRANSACT-SQL 程式設計 &#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [同步處理資料](../../relational-databases/replication/synchronize-data.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
