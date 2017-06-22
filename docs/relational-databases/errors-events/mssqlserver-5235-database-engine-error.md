---
title: MSSQLSERVER_5235 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 5235 (Database Engine error)
ms.assetid: 1aa7e6a5-7ccb-43c8-a1fd-d50e92e0a798
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bb6ed08c7ffad0e723dea7ad4774439049de3d99
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver5235"></a>MSSQLSERVER_5235
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|5235|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC4_ERRORLOG_SUMMARY_PREMATURE_TERMINATION|  
|訊息文字|USER_NAME 執行的 [EMERGENCY] DBCC DBCC_COMMAND_DETAILS 因為錯誤狀態 ERROR_STATE 而異常結束。 經過時間: HOURS 小時 MINUTES 分 SECONDS 秒。|  
  
## <a name="explanation"></a>說明  
這是當執行命令時發生非預期終止錯誤時，DBCC 列印到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔的摘要訊息。 訊息中報告的錯誤狀態定義未預期終止的類型。  
  
下表列出並定義錯誤狀態：  
  
|錯誤狀態|定義|  
|---------------|--------------|  
|狀態 0|陳述式因為中繼資料嚴重損毀而結束。 此訊息將伴隨錯誤 8930 的一或多個執行個體一起出現。|  
|狀態 1|陳述式因為內部檢查失敗而結束。 此訊息將伴隨錯誤 8967 的一個或多個執行個體一起出現。|  
|狀態 2|核心儲存引擎系統資料表的基本系統資料表檢查失敗。 此訊息將伴隨錯誤 [7984](../../relational-databases/errors-events/mssqlserver-7984-database-engine-error.md)、7985、[7986](~/relational-databases/errors-events/mssqlserver-7986-database-engine-error.md)、[7987](~/relational-databases/errors-events/mssqlserver-7987-database-engine-error.md) 或 [7988](~/relational-databases/errors-events/mssqlserver-7988-database-engine-error.md) 的一或多個執行個體一起出現。|  
|狀態 3|DBCC 緊急模式修復失敗，因為重建交易記錄檔之後，無法啟動資料庫。 此訊息將伴隨錯誤 7909 一起出現。|  
|狀態 4|命令執行期間發生宣告失敗或存取違規。|  
|狀態 5|發生使 DBCC 命令意外終止的未知錯誤。|  
  
## <a name="user-action"></a>使用者動作  
下表提供適用於指定之錯誤狀態的使用者動作。  
  
|錯誤狀態|使用者動作|  
|---------------|---------------|  
|狀態 0|從備份還原。|  
|狀態 1|連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶服務及支援中心 (CSS)。|  
|狀態 2|從備份還原。|  
|狀態 3|從備份還原。|  
|狀態 4|連絡 CSS。|  
|狀態 5|重新執行命令。 如果問題仍然存在，請連絡 CSS。|  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-transact-sql.md)  
  

