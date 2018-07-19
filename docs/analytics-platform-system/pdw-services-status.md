---
title: PDW 服務狀態-Analytics Platform System |Microsoft 文件
description: Parallel Data Warehouse (PDW) 的分析平台系統服務狀態。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6892bfcca05e0f85039dddee65a54b485a7ed433
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909888"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Analytics Platform System 的平行資料倉儲服務狀態
Parallel Data Warehouse **Services 狀態**頁面 Microsoft Analytics Platform System Configuration Manager 中會顯示所有的 SQL Server PDW 服務的目前狀態，並讓您能夠停止和啟動 PDW 服務。 這是唯一支援的方法，以啟動及停止 PDW 服務。 請注意，個別的元件或服務無法啟動獨立的。  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>若要啟動或停止應用裝置服務  
  
1.  若要啟動的應用裝置的服務，請按一下**啟動設備**。  
  
2.  若要停止應用裝置的服務，請按一下**停止設備**。  
  
您不需要按一下 **套用**啟動和停止應用裝置的服務使用時**啟動設備**並**停止設備**。  
  
![DWConfig 應用裝置 PDW 服務](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> 停止 PDW 區域也會停止 PDW 代理程式 (sqldwagent) 節點上。 PDW 代理程式需要 PDW 控制節點，以報告健康情況監視。  
  
## <a name="see-also"></a>另請參閱  
[開啟或關閉 AP 設備的電源&#40;Analytics Platform System&#41;](power-the-aps-appliance-on-or-off.md)  
  
