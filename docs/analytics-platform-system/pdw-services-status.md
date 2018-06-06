---
title: PDW 服務狀態-Analytics Platform System |Microsoft 文件
description: Parallel Data Warehouse (PDW) Analytics Platform System 的服務狀態。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e2252bb821f9522515f1625b0fc118323cb50d1f
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Parallel Data Warehouse Analytics Platform System 的服務狀態
Parallel Data Warehouse**服務狀態**頁面 Microsoft Analytics Platform System Configuration Manager 中會顯示所有的 SQL Server PDW 服務的目前狀態，並提供停止及啟動 PDW 服務的能力。 這是唯一支援的方法，啟動及停止 PDW 服務。 請注意，個別的元件或服務無法啟動獨立的。  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>若要啟動或停止應用裝置服務  
  
1.  若要啟動的應用裝置的服務，請按一下**開始應用裝置**。  
  
2.  若要停止的應用裝置的服務，請按一下**停止應用裝置**。  
  
不需要按一下**套用**啟動和停止應用裝置服務使用時**開始應用裝置**和**停止應用裝置**。  
  
![DWConfig 應用裝置 PDW 服務](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> 停止 PDW 區域也會停止 PDW 代理程式 (sqldwagent) 的 HDInsight 區域節點上。 HDInsight 區域是仍運作正常，但是健全狀況監視將無法使用。 （PDW 代理程式需要報告健康狀態監控的 PDW 控制節點）。  
  
## <a name="see-also"></a>另請參閱  
[開啟或關閉電源 AP 應用裝置&#40;Analytics Platform System&#41;](power-the-aps-appliance-on-or-off.md)  
  
