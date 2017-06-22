---
title: "Locks 事件類別目錄 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Locks event category [SQL Server]
- SQL Server event classes, Locks event category
- event classes [SQL Server], Locks event category
- lock escalation [SQL Server], locks event category
ms.assetid: 27d6afa2-7dab-4fe7-a1ad-064b879dc654
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8d1e11870107c27084efc54d0c9901f5f1be0f1a
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="locks-event-category"></a>Locks 事件類別目錄
  使用 **Locks** 事件類別目錄的事件類別，監視 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體中的鎖定活動。 這些事件類別可協助您調查，因多位使用者同時讀取和修改資料而造成的鎖定問題。  
  
 因為「 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 」經常要處理許多鎖定，於追蹤期間擷取 **Locks** 事件類別，會帶來大量負擔，而且導致產生龐大的追蹤檔案或資料表。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[Deadlock Graph 事件類別](../../relational-databases/event-classes/deadlock-graph-event-class.md)|提供死結的 XML 描述。|  
|[Lock:Acquired 事件類別](../../relational-databases/event-classes/lock-acquired-event-class.md)|指出已經在資源上取得鎖定，例如，資料表中的資料列。|  
|[Lock:Cancel 事件類別](../../relational-databases/event-classes/lock-cancel-event-class.md)|追蹤在取得鎖定之前，已經先取消的鎖定要求 (例如，以避免發生死結)。|  
|[Lock:Deadlock Chain 事件類別](../../relational-databases/event-classes/lock-deadlock-chain-event-class.md)|監視何時發生死結狀況以及牽涉哪些物件。|  
|[Lock:Deadlock 事件類別](../../relational-databases/event-classes/lock-deadlock-event-class.md)|追蹤交易何時要求鎖定已由其他交易鎖定的資源，而造成死結。|  
|[Lock:Escalation 事件類別](../../relational-databases/event-classes/lock-escalation-event-class.md)|指出細粒鎖定已經轉換成粗粒鎖定。|  
|[Lock:Released 事件類別](../../relational-databases/event-classes/lock-released-event-class.md)|追蹤何時釋放鎖定。|  
|[Lock:Timeout &#40;timeout &#62; 0&#41; 事件類別](../../relational-databases/event-classes/lock-timeout-timeout-0-event-class.md)|追蹤何時因為其他交易在所需資源上具有封鎖的鎖定，而無法完成鎖定要求。 只有在鎖定的逾時值大於零的狀況發生時，才會發生此事件。|  
|[Lock:Timeout 事件類別](../../relational-databases/event-classes/lock-timeout-event-class.md)|追蹤何時因為其他交易在所需資源上具有封鎖的鎖定，而無法完成鎖定要求。|  
  
  
