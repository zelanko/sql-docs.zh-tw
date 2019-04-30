---
title: Analytics Platform System 中的高可用性 |Microsoft Docs
description: 了解 Analytics Platform System (APS) 的高可用性架構的方式。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5c8a562ab105e1bc40b590916d0881757036aeff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280349"
---
# <a name="analytics-platform-system-high-availability"></a>Analytics Platform System 的高可用性
了解 Analytics Platform System (APS) 的高可用性架構的方式。  
  
## <a name="high-availability-architecture"></a>高可用性架構  
![設備架構](media/appliance-architecture.png "設備架構")  
  
## <a name="network"></a>Network  
如需網路可用性，AP 設備會有兩個 InfiniBand 網路。 如果其中一個 InfiniBand 網路故障，另一個是仍然可用。 此外，Active Directory 已複寫網域控制站來解析到正確的 InfiniBand 網路的連入要求。  
  
如需詳細資訊，請參閱 <<c0> [ 設定的 InfiniBand 網路介面卡](configure-infiniband-network-adapters.md)。  
  
## <a name="storage"></a>儲存體  
若要保護資料安全，AP 使用 RAID 1 鏡像設定至保留的所有使用者資料的兩份。 當磁碟失敗時，硬體系統重建備用磁碟資料，並設定警示是在磁碟故障。  
  
將可用的資料保持在線上，APS 會使用 Windows 儲存空間 」 與 「 叢集共用磁碟區來管理直接連結存放裝置中的使用者資料磁碟。 沒有每個組織成叢集共用磁碟區計算節點主機透過掛接點，您可以使用哪些資料縮放單位的一個儲存體集區。  
  
若要確保儲存體集區為線上狀態，資料縮放單位中的每一部主機會有不會容錯移轉 ISCSI 虛擬機器。 此架構很重要的因為主機失敗，資料是否仍然可以存取透過資料縮放單位中的其他主機。  
  
## <a name="hosts"></a>主控件  
主應用程式可用性，所有主機都設定至 Windows 容錯移轉叢集。 每個機架有被動主機。 第一個機架，控制 SQL Server Parallel Data Warehouse (PDW) 和設備的網狀架構，可以選擇第二個被動主應用程式。 如果主機失敗，已針對容錯移轉的虛擬機器將會容錯移轉至可用的被動主應用程式。  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW 節點和設備的網狀架構  
PDW 節點和設備的網狀架構的高可用性 / AP 使用虛擬化。 PDW 與設備的網狀架構元件的每個執行中虛擬機器。  
  
每個虛擬機器被指 Windows 容錯移轉叢集中的角色。 當虛擬機器失敗時，叢集會在可用的被動主機上重新啟動它。 使用 System Center Virtual Machine Manager 所部署虛擬機器。 發生容錯移轉，在被動的主機上執行的虛擬機器時，仍能夠存取使用者資料透過 InfiniBand 網路。  
  
控制節點和計算節點的虛擬機器分別設定為單一節點的叢集。 單一節點叢集管理的 InfiniBand 網路做為叢集資源，以確定叢集一律使用作用中的 InfiniBand IP。 單一節點叢集會管理虛擬機器內執行的 PDW 處理程序。 例如，單一節點叢集的 SQL Server 和資料移動服務 (DMS) 做為資源以便它可以啟動它們依正確順序。 控制節點 VM 也會控制在協調流程主控件執行的其他 Vm 啟動順序。  
  
