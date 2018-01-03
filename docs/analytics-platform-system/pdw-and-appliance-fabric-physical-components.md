---
title: "PDW 和應用裝置光纖實體元件 (Analytics Platform System)"
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
ms.assetid: 7748d3da-0b7c-4ec6-9c22-4897758ba573
caps.latest.revision: "17"
ms.openlocfilehash: 95e80aaa641b04391d96b55f7491e21f1a30b6d1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-and-appliance-fabric-physical-components"></a>PDW 和應用裝置網狀架構的實體元件
名稱及描述 PDW 和應用裝置網狀架構實體元件。 PDW 區域包含所有這些元件。  
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>元件圖表  
這會顯示實體元件，而且它們位於第一個機架 6 計算節點應用裝置中的名稱。  
  
![PDW 區域元件名稱-HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
PDW 元件的實際名稱是 PDW 區域名稱，後面接著虛線，後面接著該元件名稱。 例如，如果 PDW123 PDW 區域名稱，實際名稱是**PDW123 CTL01**， **PDW123 CMP01**等等。  
  
同樣地，應用裝置網狀架構元件的實際名稱是應用裝置的網域，後面接著虛線，後面接著該元件名稱。 例如，如果 FSW123 應用裝置的網域，應用裝置網狀架構的 Vm 為**FSW123 WDS**， **FSW123 AD01**， **FSW123 VMM**等等。  
  
以下是與 6 的計算節點的 PDW 區域的合併的檢視。  
  
![PDW 元件名稱](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW 元件  
PDW 虛擬機器是 PDW 區域的一部分。  
  
*PDW_region*-CTL01  
虛擬機器執行的控制節點。 這在 HST01 上執行，並可以容錯移轉到 HST02。  
  
> [!WARNING]  
> SQL Server PDW 不支援使用 HYPER-V 管理員建立 CTL01 虛擬機器的快照。 快照集依賴本機儲存體，如果虛擬機器會嘗試容錯移轉至其備份將會造成錯誤。 建立快照集也可能導致可靠性問題的其他 VM 容錯移轉至被動伺服器。  
  
*PDW_region*-透過 CMP01 *PDW_Region*-CMP06  
虛擬機器執行於計算節點。 此 6 計算節點在流程圖中，透過執行 HSA06 HSA01 主機會分別計算節點 Vm CMP01 透過 CMP06。  
  
## <a name="fabric"></a>應用裝置網狀架構元件  
這些元件是應用裝置網狀架構的一部分。  
  
### <a name="virtual-machines"></a>虛擬機器  
*appliance_domain*-WDS  
此虛擬機器主機 Windows 部署服務 (WDS)，它會使用 Analytics Platform System 應用裝置網路上部署 Windows 作業系統。 它也會裝載 DHCP 服務，可讓應用裝置主機加入網路應用裝置，而不需要預先設定的 IP 位址。  
  
*Appliance_domain*-WDS 虛擬機器 HST01 上執行，並可以容錯移轉到 HST02。 WDS 虛擬機器和 VMM 虛擬機器，請在實體主機上部署 Windows 應用裝置安裝期間。 應用裝置生命週期期間 WDS 和 VMM 執行作業，例如取代主應用程式。  
  
*appliance_domain*VMM  
Virtual Machine Manager (VMM) 虛擬機器中執行，並可以容錯移轉到 HST02。 VMM 會裝載 System Center 部署在實體主機上的作業系統。 VMM 也可讓 Windows Server Update Services (WSUS) 來套用或移除主機和虛擬機器的所有 Windows 更新。  
  
*appliance_domain*-AD01， *appliance_domain*-ad02 移  
Active Directory 網域服務，其中包含網域名稱系統 (DNS)，會 HST01 和 HST02 上執行的虛擬機器中。 應用裝置的高可用性，AD01 和 ad02 移複寫的網域控制站，而且它們執行的動作無法容錯移轉。 如果其中一個失敗，另一個已提供正確的資料。  
  
*appliance_domain*-ISCSI01  
在每個主機上的一個 ISCSI 的虛擬機器是連接的存放裝置 (HSA01 HSA06) 以執行。 此 VM 會容錯移轉。  
  
### <a name="hosts"></a>主控件  
*appliance_domain*-透過 HST01 *appliance_domain*-HST06  
針對 PDW 控制節點和應用裝置網狀架構虛擬機器主機。 HST03 是選擇性的被動主機。  
  
*appliance_domain*-透過 HSA01 *appliance_domain*-HSA08  
連接的存放裝置 (HSA) 與主機。 每個 HAS 主機執行一個計算節點 VM，另一個 ISCSI VM。  
  
### <a name="cluster-for-pdw"></a>PDW 的叢集  
*appliance_domain*-WFOHST01  
PDW 叢集名為 WFOHST01。 它會管理的所有實體主機和虛擬機器屬於 PDW。  
  
### <a name="direct-attached-storage"></a>直接連結存放裝置  
*appliance_domain*-透過 DAS01 *appliance_domain*-DAS03  
這是連接到計算節點的直接連結存放裝置。 HP 都有一個 DAS 每兩個計算節點。 Dell 和配量有一個 DAS 每三個計算節點。  
  
## <a name="see-also"></a>請參閱  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[應用裝置組態 &#40;Analytics Platform System &#41;](appliance-configuration.md)  
[應用裝置管理工作 &#40;Analytics Platform System &#41;](appliance-management-tasks.md)  
  
