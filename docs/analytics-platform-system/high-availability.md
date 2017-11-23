---
title: "分析平台系統的高可用性"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "描述如何 Analytics Platform System (APS) 的高可用性架構。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 5ab245e9-0316-4d25-a626-4745ce856925
caps.latest.revision: "9"
ms.openlocfilehash: 78b55161af9bfe8da16d7276bddc4e2f2cff9ee5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="analytics-platform-system-high-availability"></a>分析平台系統的高可用性
描述如何 Analytics Platform System (APS) 的高可用性架構。  
  
## <a name="high-availability-architecture"></a>高可用性架構  
![應用裝置架構](media/appliance-architecture.png "應用裝置架構")  
  
## <a name="network"></a>網路  
APS 應用裝置網路可用性有兩個 InfiniBand 網路。 如果其中一個 InfiniBand 網路效能降低，另一個控制器則仍可使用。 此外，Active Directory 已複寫至正確的 InfiniBand 網路解析內送要求的網域控制站。  
  
如需詳細資訊，請參閱[設定 InfiniBand 網路介面卡](configure-infiniband-network-adapters.md)。  
  
## <a name="storage"></a>儲存空間  
若要保護資料安全，AP 使用 RAID 1 鏡像即可維護所有使用者資料的兩個副本。 當磁碟失敗時，硬體系統會重建備援的磁碟上的資料，並設定是磁碟失敗警示。  
  
將可用的資料保持在線上，AP 會使用 Windows 儲存空間 」 與 「 叢集共用磁碟區來管理直接連結存放裝置的使用者資料磁碟。 沒有一個儲存集區，每個組織成叢集共用磁碟區可透過掛接點的運算節點主機資料延展單位。  
  
若要確保存放集區仍然會保持連線，資料延展單位中的每一部主機會有不會容錯移轉 ISCSI 虛擬機器。 此架構非常重要的因為如果主機失敗，資料就仍然可以存取透過資料延展單位中的其他主機。  
  
## <a name="hosts"></a>主控件  
主機可用性，所有主機都設定成 Windows 容錯移轉叢集。 每個機架有被動主機。 第一個機架，控制 SQL Server Parallel Data Warehouse (PDW) 和應用裝置網狀架構，可以選擇第二個被動主機。 如果主機失敗，已針對容錯移轉的虛擬機器將無法透過可用的被動主控件。  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW 節點和應用裝置網狀架構  
APS PDW 節點和應用裝置網狀架構的高可用性，會使用虛擬化。 每個虛擬機器中執行的 PDW 與設備網狀架構元件。  
  
每個虛擬機器會定義為在 Windows 容錯移轉叢集的角色。 當虛擬機器失敗時，叢集會可用性的被動主機上重新啟動它。 使用 System Center Virtual Machine Manager 所部署虛擬機器。 發生容錯移轉，被動的主機上執行的虛擬機器時，仍能夠存取其使用者資料透過 InfiniBand 網路。  
  
控制節點和計算節點的虛擬機器分別設定為單一節點叢集。 單一節點叢集為叢集資源，以確保叢集都一律會使用 active InfiniBand IP 管理 InfiniBand 網路。 單一節點叢集會管理虛擬機器內執行的 PDW 處理程序。 例如，單一節點叢集有 SQL Server 和資料移動服務 (DMS) 做為資源，讓它可以啟動它們依正確順序。 控制節點 VM 也會控制在協調流程主控件執行的 Vm 的啟動順序。  
  
