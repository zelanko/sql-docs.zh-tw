---
title: MSSQL_REPL027056 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 46e29452e0cec80523e4c98195f2836a94b5733b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37219158"
---
# <a name="mssqlrepl027056"></a>MSSQL_REPL027056
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|27056|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|合併處理無法變更生成集記錄 '%1'。 執行疑難排解時，以詳細資訊記錄重新啟動同步處理，並指定要寫入的輸出檔案。|  
  
## <a name="explanation"></a>說明  
 這個錯誤通常由成長過大之合併式複寫系統資料表中的競爭問題引起。 大型系統資料表通常是由較長的發行集保留期限所引起，因為在達到保留期限之前，中繼資料必須儲存於這些資料表中。  
  
## <a name="user-action"></a>使用者動作  
 **若要解決這個問題：**  
  
1.  減少「合併代理程式」-**DownloadGenerationsPerBatch** 和 **-UploadGenerationsPerBatch** 參數的值，以便在您解決造成此錯誤的基礎問題時讓處理繼續進行。 可於代理程式設定檔和命令列中指定代理程式參數。 如需詳細資訊，請參閱：  
  
    -   [處理複寫代理程式設定檔](agents/replication-agent-profiles.md)  
  
    -   [檢視並修改複寫代理程式命令提示字元參數 &#40;SQL Server Management Studio&#41;](agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](concepts/replication-agent-executables-concepts.md)的最小和最大記憶體數量。  
  
2.  為發行集保留期限指定儘可能低的設定。 如需詳細資訊，請參閱＜ [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)＞。  
  
3.  做為合併式複寫維護的一部份，請不時檢查與合併式複寫相關聯的系統資料表成長： **MSmerge_contents**、 **MSmerge_genhistory**、 **MSmerge_tombstone**、 **MSmerge_current_partition_mappings**和 **MSmerge_past_partition_mappings**。 定期重新整理資料表的索引。 如需詳細資訊，請參閱 [重新組織與重建索引](../indexes/indexes.md)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
