---
title: MSSQLSERVER_3456 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3456 (Database Engine error)
ms.assetid: d11b2b2c-3ae4-4023-b82f-05b561bfacce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f13316bdd3147bb0ad63c8d4a2fb18f1fce74006
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033407"
---
# <a name="mssqlserver_3456"></a>MSSQLSERVER_3456
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3456|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|REC_REDOLSNMISMATCH|  
|訊息文字|無法重做資料庫 '%.*ls' (資料庫識別碼 %d) 中頁面 %S_PGID 上交易識別碼 %S_XID 的記錄 %S_LSN。 頁面: LSN = %S_LSN，類型 = %ld。 記錄: OpCode = %ld，內容 %ld，PrevPageLSN: %S_LSN。 請從資料庫的備份還原或修復資料庫。|  
  
## <a name="explanation"></a>說明  
 還原作業無法重做交易記錄。 這個錯誤已經將資料庫置於 SUSPECT 狀態。 主要檔案群組以及可能還有其他檔案群組都有疑問，而且可能已損毀。 資料庫在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動期間無法復原，因此無法使用。 需要使用者動作來解決問題。  
  
 請注意，如果這個錯誤發生於 **tempdb**， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會關閉。  
  
## <a name="user-action"></a>使用者動作  
 當嘗試啟動伺服器執行個體或復原資料庫時，存在於系統上的暫時性狀況會引發這個錯誤。 每當您嘗試啟動資料庫時所發生的永久性失敗也會造成這個錯誤。 如需原因的相關資訊，請檢查 Windows 事件記錄檔，尋找指示特定失敗的先前錯誤。  
  
 如需此 3456 錯誤發生原因的詳細資訊，請檢查 Windows 事件記錄檔，尋找指出特定失敗的先前錯誤。 適當的使用者動作取決於 Windows 事件記錄檔中的資訊指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤是由暫時性狀況或永久性失敗所造成。 如需為錯誤 3456 疑難排解之使用者動作的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB &#40;Transact-sql&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [完整資料庫還原 &#40;簡單復原模式&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
