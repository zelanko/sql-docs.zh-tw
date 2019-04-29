---
title: MSSQLSERVER_5235 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5235 (Database Engine error)
ms.assetid: 1aa7e6a5-7ccb-43c8-a1fd-d50e92e0a798
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6cbfac91613c2374e42da5b33e75ed5cade2bcf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913755"
---
# <a name="mssqlserver5235"></a>MSSQLSERVER_5235
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|5235|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC4_ERRORLOG_SUMMARY_PREMATURE_TERMINATION|  
|訊息文字|USER_NAME 執行的 [EMERGENCY] DBCC DBCC_COMMAND_DETAILS 因為錯誤狀態 ERROR_STATE 而異常結束。 經過時間：HOURS 小時 MINUTES 分 SECONDS 秒。|  
  
## <a name="explanation"></a>說明  
 這是當執行命令時發生非預期終止錯誤時，DBCC 列印到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔的摘要訊息。 訊息中報告的錯誤狀態定義未預期終止的類型。  
  
 下表列出並定義錯誤狀態：  
  
|錯誤狀態|定義|  
|-----------------|----------------|  
|狀態 0|陳述式因為中繼資料嚴重損毀而結束。 此訊息將伴隨錯誤 8930 的一或多個執行個體一起出現。|  
|狀態 1|陳述式因為內部檢查失敗而結束。 此訊息將伴隨錯誤 8967 的一個或多個執行個體一起出現。|  
|狀態 2|核心儲存引擎系統資料表的基本系統資料表檢查失敗。 此訊息將伴隨錯誤 [7984](mssqlserver-7984-database-engine-error.md)、7985、[7986](mssqlserver-7986-database-engine-error.md)、[7987](mssqlserver-7987-database-engine-error.md) 或 [7988](mssqlserver-7988-database-engine-error.md) 的一或多個執行個體一起出現。|  
|狀態 3|DBCC 緊急模式修復失敗，因為重建交易記錄檔之後，無法啟動資料庫。 此訊息將伴隨錯誤 7909 一起出現。|  
|狀態 4|命令執行期間發生宣告失敗或存取違規。|  
|狀態 5|發生使 DBCC 命令意外終止的未知錯誤。|  
  
## <a name="user-action"></a>使用者動作  
 下表提供適用於指定之錯誤狀態的使用者動作。  
  
|錯誤狀態|使用者動作|  
|-----------------|-----------------|  
|狀態 0|從備份還原。|  
|狀態 1|連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶服務及支援中心 (CSS)。|  
|狀態 2|從備份還原。|  
|狀態 3|從備份還原。|  
|狀態 4|連絡 CSS。|  
|狀態 5|重新執行命令。 如果問題仍然存在，請連絡 CSS。|  
  
## <a name="see-also"></a>另請參閱  
 [DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)  
  
  
