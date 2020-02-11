---
title: SQL Server 的 SQL Errors 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f36cd694756544a44df657d97fd84e1967167b55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63183014"
---
# <a name="sql-server-sql-errors-object"></a>SQL Server 的 SQL Errors 物件
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的**SQLServer： SQL Errors**物件提供計數器來監視**SQL 錯誤**。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Errors** 計數器。  
  
|SQL Server SQL Errors 計數器|描述|  
|------------------------------------|-----------------|  
|**錯誤數/秒**|每秒的錯誤數目。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|Item|定義|  
|----------|----------------|  
|**_Total**|所有錯誤的相關資訊。|  
|**資料庫離線錯誤**|追蹤導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 讓目前資料庫離線的嚴重錯誤。|  
|**資訊錯誤**|針對僅提供資訊給使用者而不會導致錯誤的錯誤訊息，提供其相關資訊。|  
|**終止連接錯誤**|追蹤導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 清除目前連接的嚴重錯誤。|  
|**使用者錯誤**|使用者錯誤的相關資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
