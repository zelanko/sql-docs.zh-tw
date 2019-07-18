---
title: MSSQL_ENG020557 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020557 error
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6816a0301a03e2c0d01cfe78a5c88213394c445b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057101"
---
# <a name="mssqleng020557"></a>MSSQL_ENG020557
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|20557|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|代理程式關閉。 如需詳細資訊，請參閱 SQL Server Agent 作業記錄中的作業 '%s'。|  
  
## <a name="explanation"></a>說明  
 複寫代理程式已關閉，而未將原因寫入適當的記錄資料表，或者代理程式在處理序仍執行時關閉。  
  
## <a name="user-action"></a>使用者動作  
  
-   重新啟動代理程式，查看現在執行是否已無錯誤。 如需詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](concepts/replication-agent-executables-concepts.md)。  
  
-   請檢查代理程式記錄和作業記錄是否同時發生其他錯誤。 如需有關如何在「複寫監視器」中檢視代理程式狀態和錯誤詳細資料的資訊，請參閱[使用複寫監視器來檢視資訊及執行工作](monitor/view-information-and-perform-tasks-replication-monitor.md)。
-   確認代理程式所存取電腦之間的基本連接能夠正常運作，然後使用公用程式 (例如 **sqlcmd** 公用程式) 連接每部電腦。 連接時，請使用代理程式建立連接的相同帳戶。 如需有關每個代理程式帳戶所需權限的詳細資訊，請參閱＜ [Replication Agent Security Model](security/replication-agent-security-model.md)＞。  
  
-   如果在建立或套用快照集時發生錯誤，則請檢查快照集目錄中的檔案以找出錯誤。  
  
-   若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和其他錯誤訊息。 如需有關如何設定複寫記錄的詳細資訊，請參閱 Microsoft 知識庫文件 [312292](https://support.microsoft.com/kb/312292)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
