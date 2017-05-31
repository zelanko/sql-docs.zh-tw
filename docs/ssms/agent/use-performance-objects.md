---
title: "使用效能物件 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5197a38da57e041039dab93d037064bba79db7ff
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="use-performance-objects"></a>使用效能物件
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 包含效能物件及計數器，可用來監視服務執行的狀況。 這些效能物件可讓您使用「效能監視器」(一種 Windows 工具)，來識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務在背景執行哪些工作。 例如，您可以識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務目前正在執行多少使用中的作業，以找出被封鎖的作業。  
  
針對電腦上所安裝的每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體，都有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務效能物件及計數器存在。 效能物件是依據每項物件所代表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體來命名的。  
  
下表顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務效能物件的命名方式：  
  
|執行個體類型|物件名稱|  
|-----------------|---------------|  
|預設值|**SQLAgent:***object*:*counter*|  
|具名|**SQLAgent$**<br /> **&#42;instance_name&#42; :***object*:*counter*|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 的下列效能物件。  
  
|物件名稱|說明|  
|---------------|---------------|  
|[SQLAgent:Jobs](http://msdn.microsoft.com/en-us/225b5e2d-4a78-4178-b2b6-b419df83c4aa)|有關已啟動作業、成功率及目前狀態的效能資訊|  
|[SQLAgent:JobSteps](http://msdn.microsoft.com/en-us/44f9983c-1753-4fe0-8475-973aa2460b3a)|作業步驟的狀態資訊|  
|[SQLAgent:Alerts](http://msdn.microsoft.com/en-us/e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a)|警示及通知數的相關資訊|  
|[SQLAgent:Statistics](http://msdn.microsoft.com/en-us/ebe92bfa-0721-48aa-9ba6-e7904ad265a1)|一般效能資訊|  
  
## <a name="see-also"></a>另請參閱  
[效能的監視與微調](http://msdn.microsoft.com/en-us/87f23f03-0f19-4b2e-bfae-efa378f7a0d4)  
[如何：啟動系統監視器 (Windows)](http://msdn.microsoft.com/en-us/5e51bb79-5737-470b-9c47-fac330c001c5)  
  

