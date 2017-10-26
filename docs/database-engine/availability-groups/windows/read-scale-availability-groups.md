---
title: "讀取級別可用性群組 | Microsoft Docs"
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6dfa046a07b9fd5a3eddbe474b5ea63c1163c26c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="read-scale-availability-groups"></a>讀取級別可用性群組
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

除了合併 SQL Server 的類別 HA 功能的最佳部分之外，可用性群組也是提供整合式縮放解決方案的全面解決方案。 在一般資料庫應用程式中，有多個用戶端執行各種類型的工作負載，有時，可能會因資源條件約束而造成瓶頸。 您可以釋出資源，並達到 OLTP 工作負載的更高輸送量，或提供唯讀工作負載的較高效能和級別。 這可以利用 SQL Server 的最快複寫技術達成 - 建立一組已複寫的資料庫，以將報告和分析工作負載卸載至唯讀複本。 

使用可用性群組，可以將一個或多個次要複本設定成支援對次要資料庫的唯讀存取。

執行分析或報告工作負載的用戶端應用程式可以直接連接至次要資料庫。 或者，客戶可以設定唯讀路由清單，並以循環配置資源方式從路由清單中連接至將連接要求轉送至每個次要複本的主要複本。

## <a name="read-scale-availability-groups-without-cluster"></a>沒有叢集的讀取級別可用性群組

在 [!INCLUDE[sssql15-md](..\..\..\includes\sssql15-md.md)] 和以前版本中，所有可用性群組都需要叢集。 叢集已提供商務持續性 - 高可用性和災害復原 (HADR)。 此外，無法設定次要複本進行讀取作業。 如果 HA 不是目標，則設定和操作叢集表示會有大量操作費用。 SQL Server 2017 引進沒有叢集的讀取級別可用性群組。 

如果商務需求是保留主要複本上執行之任務關鍵性工作負載的資源，則使用者現在可以使用唯讀路由，或直接連接至可讀取的次要複本，而不需要根據與任何叢集技術的整合。 這些新功能可供在 Windows 和 Linux 平台上執行的 SQL Server 2017 使用。

>[!IMPORTANT]
>這不是高可用性安裝。 沒有任何基礎結構可監視與協調失敗偵測和自動容錯移轉。 若是需要 HADR 功能的使用者，請使用叢集管理員 (在 Windows 上為 WSFC，在 Linux 上則為 Pacemaker)。 

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>將分散式可用性群組用於地理讀取級別

地理不同的解決方案可以使用分散式可用性群組來實作讀取級別解決方案。 這允許將從主要複本到可讀取次要複本的讀取工作負載卸載至較接近讀取工作負載來源的網站。 這不僅可以降低主要複本上的資源使用量，也可透過減少網路延遲並利用專用資源來協助讀取輸送量。

單一分散式可用性群組最多可以有 17 個可讀取次要複本。 為了增加縮放容量，透過菊輪鍊鏈結多個可用性群組，甚至進一步增加可讀取複本數目。 您也可以在地理分散的環境中部署來自相同可用性群組的兩個分散式可用性群組，以取得低延遲讀取。




## <a name="next-steps"></a>後續步驟 

[在 Linux 上設定讀取級別可用性群組](../../../linux/sql-server-linux-availability-group-configure-rs.md)

## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

