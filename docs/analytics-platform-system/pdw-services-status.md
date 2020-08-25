---
title: PDW 服務狀態
description: 分析平臺系統的平行資料倉儲 (PDW) 服務狀態。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2789c8b74420a56a32d08a0339d4ee6d3cc112d1
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400848"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>分析平臺系統的平行處理資料倉儲服務狀態
[Microsoft Analytics Platform System Configuration Manager 中的 [平行資料倉儲 **服務狀態** ] 頁面會顯示所有 SQL Server PDW 服務的目前狀態，並提供停止和啟動 PDW 服務的能力。 這是啟動及停止 PDW 服務的唯一支援方法。 請注意，無法獨立啟動個別的元件或服務。  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>若要啟動或停止設備服務  
  
1.  若要啟動設備服務，請按一下 [ **啟動設備**]。  
  
2.  若要停止設備服務，請按一下 [ **停止設備**]。  
  
使用 [**啟動設備**] 和 [**停止設備**] 啟動和停止設備服務時，不**需要按一下 [** 套用]。  
  
![DWConfig 應用裝置 PDW 服務](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> 停止 PDW 區域也會停止在節點上 (sqldwagent) 的 PDW 代理程式。 PDW 代理程式需要 PDW 控制節點來報告健康情況監視。  
  
## <a name="see-also"></a>另請參閱  
[開啟或關閉 &#40;Analytics Platform System&#41;的 AP 設備 ](power-the-aps-appliance-on-or-off.md)  
  
