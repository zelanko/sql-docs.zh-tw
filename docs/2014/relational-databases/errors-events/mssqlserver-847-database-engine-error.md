---
title: MSSQLSERVER_847 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 847 (Database Engine error)
ms.assetid: 67208b7c-bd8d-48a1-9f70-a6488e0f5f9b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6bd85b72fc786d4aa807d73e57a69193b515067d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62762797"
---
# <a name="mssqlserver847"></a>MSSQLSERVER_847
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|847|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|N/A|  
|訊息文字|等候閂鎖時發生逾時: 類別 '%ls'，識別碼 %p，類型 %d，工作 0x%p : %d，等候時間 %d，旗標 0x%I64x，主控工作 0x%p。 繼續等候。|  
  
## <a name="explanation"></a>說明  
 就在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將緩衝閂鎖錯誤寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔的同時，電腦可能停止回應 (凍結)，或者發生逾時或其他例行作業中止。  
  
 如果訊息中的狀態欄位值為 0x04 on，表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正等候 I/O 作業完成。 您可能也會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中看到 [MSSQLSERVER_833](mssqlserver-833-database-engine-error.md) 訊息。  
  
 如果訊息中的狀態欄位值為 0x04 off，意指頁面發生嚴重的競爭問題。 若問題物件是資料頁，起因可能就在於程式碼設計不良。 反之若非資料頁，則錯誤大致是因伺服器瓶頸所造成，例如硬體資源不足。  
  
## <a name="user-action"></a>使用者動作  
 若要解決這個問題，請依據您的環境採取下列一個或多個步驟，應可減緩或消除錯誤訊息的出現：  
  
-   判斷您的硬體是否有瓶頸。 若有必要，請升級硬體使其足以支援所處環境的組態、查詢和負載需求。 如需瓶頸的詳細資訊，請參閱[找出瓶頸](../performance/identify-bottlenecks.md)。  
  
-   檢查所有記錄的錯誤，據以執行硬體廠商提供的任何診斷事項。  
  
-   確定磁碟機並未壓縮。 資料檔案和記錄檔不支援儲存在壓縮磁碟機上。 如需有關檔案和檔案群組的詳細資訊，請參閱[資料庫檔案與檔案群組](../databases/database-files-and-filegroups.md)。  
  
-   將下列選項設成 off，看看錯誤訊息是否會消失：  
  
    -   SQL Server priority boost 組態選項  
  
    -   輕量型共用 (Fiber 模式) 選項  
  
    -   Set working set size 選項  
  
    > [!NOTE]  
    >  上述設定一旦變更而不再是預設值 OFF，通常會造成不利影響。 如需設定的詳細資訊，請參閱[伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
-   微調查詢以減少系統資源耗用。 效能微調有助於減輕系統負擔，並可縮短個別查詢的回應時間。  
  
-   將 AUTO_SHRINK 選項設成 OFF，以使資料庫大小改變時的負擔降低。  
  
-   確定 FILEGROWTH 選項的設定值夠大，以免遞增次數過於頻繁。 請排程作業於離峰時段檢查資料庫中可用的空間量，再據以增加資料庫大小。  
  
  
