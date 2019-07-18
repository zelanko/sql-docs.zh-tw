---
title: MSSQLSERVER_3314 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3314 (Database Engine error)
ms.assetid: f3a5ca6a-b502-4cab-b3b1-4bc753763fa9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8d82911f013c9284a55bd55f00654a98633df0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914165"
---
# <a name="mssqlserver3314"></a>MSSQLSERVER_3314
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|3314|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|ERR_LOG_RID2|  
|訊息文字|恢復資料庫 '%.*ls' 已記錄的作業時，記錄識別碼 %S_LSN 發生錯誤。 一般而言，之前是將該錯誤記錄為 Windows 事件記錄檔服務的錯誤。 請從備份中還原資料庫或檔案，或修復資料庫。|  
  
## <a name="explanation"></a>說明  
 這是恢復復原的積存錯誤。 這個錯誤已經將資料庫置於 SUSPECT 狀態。 主要檔案群組以及可能還有其他檔案群組都有疑問，而且可能已損毀。 資料庫在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動期間無法復原，因此無法使用。 需要使用者動作來解決問題。  
  
 請注意，如果這個錯誤發生於 **tempdb**， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會關閉。  
  
## <a name="user-action"></a>使用者動作  
 當嘗試啟動伺服器執行個體或復原資料庫時，存在於系統上的暫時性狀況會引發這個錯誤。 每當您嘗試啟動資料庫時所發生的永久性失敗也會造成這個錯誤。 如需原因的相關資訊，請檢查 Windows 事件記錄檔，尋找指示特定失敗的先前錯誤。  
  
 如需有關此 3314 錯誤發生原因的詳細資訊，請檢查 Windows 事件記錄檔，尋找指出特定失敗的先前錯誤。 適當的使用者動作取決於 Windows 事件記錄檔中的資訊指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤是由暫時性狀況或永久性失敗所造成。 如需有關疑難排解錯誤 3314 之使用者動作的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [完整資料庫還原 &#40;簡單復原模式&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
