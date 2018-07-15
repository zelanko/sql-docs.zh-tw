---
title: 指定作業回應 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], responses
- SQL Server Agent jobs, responses
- actions [SQL Server Agent jobs]
- responding to jobs
ms.assetid: 050242e1-9b79-4ade-91a9-580707b9d2d9
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef60a02b437ed6a66a5db0db4e07938d2a70c4e5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323708"
---
# <a name="specify-job-responses"></a>指定作業回應
  作業回應可指定完成作業後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式服務將採取的動作。 作業回應可確保資料庫管理員知道作業已完成，以及作業的執行頻率。 典型的作業回應包括：  
  
-   使用電子郵件、電子呼叫或 **net send** 訊息通知操作員。  
  
     如果操作員必須執行後續動作，請使用其中一個作業回應。 例如，如果備份作業成功完成，必須告知操作員以取下備份磁帶，並將其存放在安全的地方。  
  
-   將事件訊息寫入至 Windows 應用程式記錄。  
  
     這個回應只用於失敗的作業。  
  
-   自動刪除作業。  
  
     如果確定您將不再需要重新執行這個作業，請使用這個作業回應。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何通知操作員作業狀態。|[Notify an Operator of Job Status](notify-an-operator-of-job-status.md)|  
|描述如何將作業狀態寫入 Windows 應用程式記錄檔。|[Write the Job Status to the Windows Application Log](../../reporting-services/report-server/windows-application-log.md)|  
  
## <a name="see-also"></a>另請參閱  
 [監視及回應事件](monitor-and-respond-to-events.md)  
  
  
