---
title: 管理事件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- event-triggered jobs [SQL Server]
- forwarding events [SQL Server]
- alerts [SQL Server], forwarded events
- alerts [SQL Server], management servers
- SQL Server Agent alerts, management servers
ms.assetid: 8f4ee7f5-80df-49fd-b2b8-d020e04b6e1b
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a8a6e25a518e62c8498fb00fcd45b0217e60d71
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286614"
---
# <a name="manage-events"></a>管理事件
  您可以將達到或超過特定錯誤嚴重性層級的所有事件訊息轉送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 這稱為「事件轉送」。 轉送伺服器是一個專用的伺服器，它也可以當做主要伺服器。 您可以利用事件轉送功能將伺服器群組的警示管理集中化，藉以減輕使用頻繁之伺服器的工作負載。  
  
 當某伺服器接收到其他伺服器群組的事件時，接收事件的伺服器稱為「警示管理伺服器」。 在多伺服器的環境中，您可以將主要伺服器指定為警示管理伺服器。  
  
## <a name="advantages-of-using-an-alerts-management-server"></a>使用警示管理伺服器的優點  
 設定警示管理伺服器的優點包括：  
  
-   **集中化**。 可從單一伺服器集中控制和合併檢視多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的事件。  
  
-   **延展性**。 能以一個邏輯伺服器的方式管理很多實體的伺服器。 您可以依照需要對這個實體的伺服器群組新增或移除伺服器。  
  
-   **效率**。 組態時間減少，因為您只需要定義一次警示和運算子。  
  
## <a name="disadvantages-of-using-an-alerts-management-server"></a>使用警示管理伺服器的缺點  
 設定警示管理伺服器的缺點包括：  
  
-   **網路流量增加**。 將事件轉送至警示管理伺服器會增加網路傳輸量。 將事件轉送限制在高於指定嚴重性層級的事件，可減緩流量增加的情況。  
  
-   **單一失敗點**。 如果警示管理伺服器離線，則不會對受管理伺服器群組上的任何事件發出警示。  
  
-   **伺服器負載**。 處理轉送事件的警示會造成警示管理伺服器的處理負載增加。  
  
## <a name="guidelines-for-using-an-alerts-management-server"></a>使用警示管理伺服器的指導方針  
 在設定警示管理伺服器時，請遵守下列指導方針：  
  
-   若要接收轉送的事件，則警示管理伺服器必須是預設的 SQL Server 執行個體。  
  
-   避免在警示管理伺服器上執行重要或使用頻繁的應用程式。  
  
-   小心規劃網路傳輸量，包括設定許多伺服器來共用相同的警示管理伺服器。 如果發生阻塞，請減少使用某一特別警示管理伺服器的伺服器數量。  
  
     在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 內註冊的伺服器構成一份清單，其中就是可供該伺服器用來選擇作為警示轉送伺服器的伺服器。  
  
-   在需要伺服器特定回應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體上定義警示，而不要將警示轉送到警示管理伺服器。  
  
     警示管理伺服器會將轉送來的所有伺服器視為一個邏輯整體。 例如，警示管理伺服器會以相同的方式，回應來自伺服器 A 的 605 事件和來自伺服器 B 的 605 事件。  
  
-   請在設定警示系統後，定期檢查 Microsoft Windows 應用程式記錄檔中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 事件。  
  
     警示引擎所遇到的失敗狀況，會以來源名稱 "SQL Server Agent" 寫入本機 Windows 應用程式記錄檔中。 例如，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 無法傳送已定義的電子郵件通知，則會在應用程式記錄檔中記錄一個事件。  
  
 如果本機定義的警示未啟動，卻發生了會引發警示的事件，則會將事件轉送至警示管理伺服器 (如果它符合警示轉送條件的話)。 轉送時可依據本機站台的使用者需求，來關閉或開啟本機覆寫 (本機定義的警示，也定義於警示管理伺服器上)。 即使事件也是由本機警示所處理的，您仍舊可以要求一律轉送事件。  
  
 下列是在多伺服器環境中管理事件的一般工作：  
  
 **若要指定警示管理伺服器**  
  
-   [Transact-SQL](../sql-server-management-studio-ssms.md)  
  
 **若要定義對警示的回應**  
  
-   [Transact-SQL](define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)  
  
## <a name="running-event-triggered-jobs"></a>執行事件觸發作業  
 您可以定義執行一個作業來回應警示。 例如，您可以執行一個作業來更正或進一步診斷由警示所偵測到的問題。  
  
> [!NOTE]  
>  因為作業可能引發事件，請小心不要建立遞迴式警示作業迴圈。  
  
## <a name="see-also"></a>另請參閱  
 [sys.sysmessages &#40;Transact SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysmessages-transact-sql)  
  
  
