---
title: "PDW 服務狀態 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fc9bee2-c372-4c4a-956c-fb54215d8918
caps.latest.revision: "14"
ms.openlocfilehash: 7a6b1a1f9a6ef922833930abf00ca10482648141
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-services-status"></a>PDW 服務狀態
Parallel Data Warehouse**服務狀態**頁面 Microsoft Analytics Platform System Configuration Manager 中會顯示所有的 SQL Server PDW 服務的目前狀態，並提供停止及啟動 PDW 服務的能力。 這是唯一支援的方法，啟動及停止 PDW 服務。 請注意，個別的元件或服務無法啟動獨立的。  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>若要啟動或停止應用裝置服務  
  
1.  若要啟動的應用裝置的服務，請按一下**開始應用裝置**。  
  
2.  若要停止的應用裝置的服務，請按一下**停止應用裝置**。  
  
不需要按一下**套用**啟動和停止應用裝置服務使用時**開始應用裝置**和**停止應用裝置**。  
  
![DWConfig 應用裝置 PDW 服務](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> 停止 PDW 區域也會停止 PDW 代理程式 (sqldwagent) 的 HDInsight 區域節點上。 HDInsight 區域是仍運作正常，但是健全狀況監視將無法使用。 （PDW 代理程式需要報告健康狀態監控的 PDW 控制節點）。  
  
## <a name="see-also"></a>請參閱  
[APS 應用裝置開啟或關閉 &#40; 的電源Analytics Platform System &#41;](power-the-aps-appliance-on-or-off.md)  
  
