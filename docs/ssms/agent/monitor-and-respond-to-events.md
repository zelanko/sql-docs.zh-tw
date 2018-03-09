---
title: "監視及回應事件 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- notifications [SQL Server], alert
- events [SQL Server], alerts
- alerts [SQL Server]
- notifications [SQL Server]
- events [SQL Server], automatically responding to
- administrator notifications [SQL Server Agent]
- automatic event responses
- SQL Server Agent alerts
- monitoring [SQL Server], events
- responding to events automatically
ms.assetid: f7fbe155-5b68-4777-bc71-a47637471f32
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9599d16a627d3bef2c5a1f0261d6395b08ec1ecd
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="monitor-and-respond-to-events"></a>監視及回應事件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會監視及自動回應「事件」(Event)，例如：來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的訊息、特定效能狀況與 Windows Management Instrumentation (WMI) 事件。  
  
## <a name="in-this-section"></a>本節內容  
[警示](../../ssms/agent/alerts.md)  
包含如何命名警示和選取警示所回應之事件或效能狀況的相關資訊。  
  
[建立使用者定義的事件](../../ssms/agent/create-a-user-defined-event.md)  
包含有關於如何建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]預先定義之事件以外的事件的資訊。  
  
[運算子](../../ssms/agent/operators.md)  
包含當作業失敗或成功時，如何建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 可用來傳送通知的管理員別名。  
  
## <a name="about-monitoring-and-responding-to-events"></a>關於監視及回應事件  
對於事件的自動回應稱之為「警示」。 您可以在一或多個事件上定義警示，以指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 回應事件的方式。 警示可透過通知管理員或執行作業 (或兩者) 來回應事件。 警示也可以將事件轉送到在另一部電腦上登入的 Microsoft Windows 應用程式。 例如，如果發生嚴重性 19 的事件，您可以指定要立即通知操作員。 透過定義警示，資料庫管理員就可以更有效率地監視和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 只會回應已定義警示的事件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 用來監視事件的方法會取決於事件的類型。  
  
對效能計數器定義了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 警示後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 就會直接監視效能計數器。 若是 WMI 事件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會登錄 WMI 事件的事件查詢。  
  
若要回應來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的訊息， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會監視 Windows 應用程式記錄檔。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 只會回應出現在這個記錄檔中的訊息。 根據預設，SQL Server 會將下列訊息記錄在 Windows 應用程式記錄檔中：  
  
-   嚴重性 19 或更高的 sysmessages 錯誤。  
  
    如果您還要記錄嚴重性低於 19 的特定 sysmessages 錯誤，請使用 sp_altermessage 預存程序將這類錯誤指定為「一律記錄」。  
  
-   使用 WITH LOG 語法叫用的任何 RAISERROR 陳述式。  
  
    建議您使用 PAISERROR WITH LOG，從 SQL Server 執行個體寫入 Windows 應用程式記錄檔。  
  
-   使用 xp_logevent 記錄的任何應用程式事件。  
  
    > [!NOTE]  
    > 記錄應用程式事件會消耗記錄檔空間，並且造成 Windows 應用程式記錄檔超出其大小上限。 請確定 Windows 應用程式記錄檔具有足夠的大小，以免遺失 SQL Server 事件資訊。  
  
當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 記錄訊息時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務會比較訊息和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 管理員所定義的警示。  
  
不管事件的來源為何， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務都會透過執行在事件警示中指定的工作來回應事件。  
  
## <a name="see-also"></a>另請參閱  
[sp_altermessage](http://msdn.microsoft.com/en-us/1b28f280-8ef9-48e9-bd99-ec14d79abaca)  
  
