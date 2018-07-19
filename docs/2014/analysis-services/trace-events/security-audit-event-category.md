---
title: Security Audit 事件類別目錄 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [Analysis Services], security audit
- security events [Analysis Services]
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79141f6ed5c61e03b792875fbff2253f9e8bd0aa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180905"
---
# <a name="security-audit-event-category"></a>安全性稽核事件類別目錄
  [安全性稽核] 事件類別目錄具有下表所描述的事件類別。  
  
|Event Class|事件識別碼|描述|  
|-----------------|--------------|-----------------|  
|稽核登入|1|記錄啟動追蹤之後的所有新連接事件，例如，當用戶端要求連接到執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的伺服器時。|  
|稽核登出|2|記錄啟動追蹤之後的所有新中斷連接事件，例如當用戶端發出中斷連接命令時。|  
|Audit Server Starts and Stops|4|記錄服務的關閉、啟動與暫停活動。|  
|稽核物件權限事件|18|記錄所有物件權限之變更。|  
|稽核管理作業事件|19|記錄備份、還原、同步處理、附加、卸離、影像載入和影像儲存的伺服器作業。|  
  
 如需每個安全性稽核事件類別之相關聯資料行的資訊，請參閱 [安全性稽核資料行](security-audit-data-columns.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 追蹤事件](analysis-services-trace-events.md)  
  
  
