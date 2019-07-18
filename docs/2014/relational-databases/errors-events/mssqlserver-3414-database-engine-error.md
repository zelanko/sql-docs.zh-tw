---
title: MSSQLSERVER_3414 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3414 (Database Engine error)
ms.assetid: f25852f9-b91c-4356-b817-78bec9ec8db4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 890179c3f5a6bc7d3d627ce9cf2c51fc5d2e96ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868273"
---
# <a name="mssqlserver3414"></a>MSSQLSERVER_3414
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|3414|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|REC_GIVEUP|  
|訊息文字|復原時發生錯誤，導致資料庫 '%.*ls' (資料庫識別碼 %d) 無法重新啟動。 請診斷並修正復原錯誤，或者從已知完好的備份還原。 如果不能更正或預期錯誤，請連絡技術支援部門。|  
  
## <a name="explanation"></a>說明  
 已復原指定的資料庫，但是因為復原期間發生錯誤而無法啟動。 這個錯誤已經將資料庫置於 SUSPECT 狀態。 主要檔案群組以及可能還有其他檔案群組都有疑問，而且可能已損毀。 資料庫在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動期間無法復原，因此無法使用。 需要使用者動作來解決問題。  
  
 請注意，如果這個錯誤發生於 **tempdb**， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會關閉。  
  
## <a name="user-action"></a>使用者動作  
 當嘗試啟動伺服器執行個體或復原資料庫時，存在於系統上的暫時性狀況會引發這個錯誤。 每當您嘗試啟動資料庫時所發生的永久性失敗也會造成這個錯誤。 如需原因的相關資訊，請檢查 Windows 事件記錄檔，尋找指示特定失敗的先前錯誤。  
  
 如需此 3314 錯誤發生原因的詳細資訊，請檢查 Windows 事件記錄檔，尋找指出特定失敗的先前錯誤。 適當的使用者動作取決於 Windows 事件記錄檔中的資訊指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤是由暫時性狀況或永久性失敗所造成。 如需疑難排解錯誤 3314 之使用者動作的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [完整資料庫還原 &#40;簡單復原模式&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
