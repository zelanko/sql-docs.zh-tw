---
title: SQL Server 擴充的事件引擎 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], engine
ms.assetid: d74642a5-42b9-4a15-aa3d-f98bfe695050
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89d92fc60e18926351cc94e6e6c21a32a7371ed5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62638231"
---
# <a name="sql-server-extended-events-engine"></a>SQL Server 擴充的事件引擎
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擴充的事件引擎是執行以下作業之服務與物件的集合：  
  
-   啟用事件的定義。  
  
-   啟用事件資料的處理。  
  
-   管理系統中擴充的事件服務和物件。  
  
-   維護擴充的事件工作階段清單及管理對此清單的存取。  
  
 擴充的事件引擎本身並未提供當事件引發時所要採取的任何事件或動作。 使用擴充之事件引擎的程序會定義與該引擎之間的互動。 這些程序會加入事件點，並提供為了回應事件引發所要採取的動作。  
  
 下圖顯示擴充的事件工作階段的簡化檢視。 如需詳細資訊，請參閱 [SQL Server 擴充的事件工作階段](sql-server-extended-events-sessions.md)。  
  
 ![詳細的擴充事件架構](../../database-engine/media/xearchitecturedetailed.gif "詳細的擴充事件架構")  
  
 請注意下列事項：  
  
-   每一個 Windows 處理序都可以有一或多個模組 (**Win32 處理序**、**Win32 模組**)。 這些也稱為「二進位檔」或「可執行模組」。  
  
-   每一個 Windows 處理序模組都可包含一或多個擴充的事件封裝 (**Package**)，其中包含一或多個擴充的事件物件 (**Type**、**Target**、**Action**、**Map**、**Predicate** 和 **Event**)。  
  
-   在主機處理序內，只能有一個擴充的事件引擎執行個體 (**擴充的事件引擎**)，此執行個體會執行以下作業：  
  
    -   管理此工作階段的某些層面 (例如，列舉工作階段)。  
  
    -   處理分派 (**發送器**)。 這與執行緒集區非常類似。  
  
    -   處理事件的記憶體緩衝區 (**緩衝區**)。 當緩衝區填滿時，會將緩衝區分派給目標。  
  
-   當建立工作階段，而且選擇性地將事件繫結至工作階段 (**工作階段內容**) 之後：  
  
    -   也可能會建立目標的執行個體 (**目標執行個體**)，並將其加入工作階段。  
  
    -   當緩衝區填滿時，會將這些緩衝區分派給目標。  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](extended-events.md)  
  
  
