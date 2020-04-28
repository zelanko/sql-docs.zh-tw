---
title: 高可用性
description: 瞭解分析平臺系統（AP）如何架構以提供高可用性。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6246ed25909a2e366d8bbafcd912a4fd923cc84a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401107"
---
# <a name="analytics-platform-system-high-availability"></a>分析平臺系統高可用性
瞭解分析平臺系統（AP）如何架構以提供高可用性。  
  
## <a name="high-availability-architecture"></a>高可用性架構  
![設備架構](media/appliance-architecture.png "設備架構")  
  
## <a name="network"></a>網路  
針對網路可用性，AP 應用裝置有兩個不適用的網路。 如果其中一個未使用的網路停止運作，另一個則仍然可用。 此外，Active Directory 已複寫網域控制站，以將連入要求解析為正確的未處理網路。  
  
如需詳細資訊，請參閱設定不確定的[網路介面卡](configure-infiniband-network-adapters.md)。  
  
## <a name="storage"></a>儲存體  
為了保護資料安全，AP 會使用 RAID 1 鏡像來維護兩個使用者資料的複本。 當磁片故障時，硬體系統會將資料重建到備用磁片，並設定發生磁片失敗的警示。  
  
為了讓資料可在線上使用，AP 會使用 Windows 儲存空間和叢集共用磁片區來管理直接連結儲存體中的使用者資料磁片。 每個資料縮放單位都有一個存放集區，其組織成叢集共用磁片區，可透過掛接點供計算節點主機使用。  
  
為確保存放集區保持上線，資料縮放單位中的每個主機都有一個不會容錯移轉的 ISCSI 虛擬機器。 此架構很重要，因為如果主機失敗，仍然可以透過資料縮放單位中的其他主機來存取資料。  
  
## <a name="hosts"></a>主機  
對於主機可用性，所有主機都會設定為 Windows 容錯移轉叢集。 每個機架都有被動主機。 （選擇性）第一個機架（控制 SQL Server 平行處理資料倉儲（PDW）和設備網狀架構）可以有第二部被動主機。 如果主機失敗，針對容錯移轉設定的虛擬機器將會容錯移轉到可用的被動主機。  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW 節點和設備網狀架構  
為了讓 PDW 節點和設備網狀架構具有高可用性，AP 會使用虛擬化。 每個 PDW 和設備網狀架構元件都會在虛擬機器中執行。  
  
每部虛擬機器都定義為 Windows 容錯移轉叢集中的角色。 當虛擬機器失敗時，叢集會在可用的被動主機上將它重新開機。 系統會使用 System Center Virtual Machine Manager 來部署虛擬機器。 發生容錯移轉時，在被動主機上執行的虛擬機器仍然可以透過未使用的網路存取其使用者資料。  
  
「控制節點」和「計算節點」虛擬機器分別設定為單一節點叢集。 單一節點叢集會將無法使用的網路視為叢集資源來管理，以確保叢集一律使用作用中的未通過 IP。 單一節點叢集會管理在虛擬機器內執行的 PDW 進程。 例如，單一節點叢集具有 SQL Server 和資料移動服務（DMS）做為資源，讓它能夠以適當的順序啟動它們。 控制節點 VM 也會控制在協調流程主機上執行的其他 Vm 的啟動順序。  
  
