---
title: 設備實體元件 Analytics Platform System |Microsoft Docs
description: 名稱及描述 PDW 與設備網狀架構實體元件。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: fb7ad8715d3f7a885bc48f6bdcc7f1ec2842f269
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960420"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>設備實體元件 Analytics Platform System
名稱及描述 PDW 與設備網狀架構實體元件。 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>元件圖表  
這會顯示實體的元件，而且它們位於第一個 6 計算節點設備的機架中的名稱。  
  
![PDW 區域元件名稱-HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
PDW 元件的實際名稱是 PDW 區域名稱，後面接著虛線後, 接著的元件名稱。 例如，如果 PDW123 PDW 區域名稱，實際名稱是**PDW123 CTL01**， **PDW123 CMP01**等等。  
  
同樣地，設備的網狀架構元件的實際名稱是設備網域，後面接著虛線後, 接著的元件名稱。 比方說，如果設備網域是 FSW123，設備 fabric Vm 就會**FSW123 WDS**， **FSW123 AD01**， **FSW123 VMM**，依此類推。  
  
以下是具有 6 個計算節點的 PDW 區域的合併的檢視。  
  
![PDW 元件名稱](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW 元件  
PDW 虛擬機器是 PDW 區域的一部分。  
  
*PDW_region*-CTL01  
執行控制節點的虛擬機器。 這在 HST01 上執行，並可以容錯移轉至 HST02。  
  
> [!WARNING]  
> SQL Server PDW 不支援使用 HYPER-V 管理員建立 CTL01 虛擬機器的快照集。 快照集依賴本機儲存體，這會導致錯誤，如果虛擬機器會嘗試容錯移轉至其備份。 建立快照集也可以讓可靠性問題的其他 vm 容錯移轉至被動的伺服器。  
  
*PDW_region*-透過 CMP01 *PDW_Region*-CMP06  
執行計算節點的虛擬機器。 這 6 計算節點在圖表中，透過執行 HSA06 HSA01 主機會分別計算節點 Vm CMP01 透過 CMP06。  
  
## <a name="fabric"></a>設備的網狀架構元件  
這些元件是設備的網狀架構的一部分。  
  
### <a name="virtual-machines"></a>虛擬機器  
*appliance_domain*-WDS  
此虛擬機器主機 Windows 部署服務 (WDS)、 Analytics Platform System 使用透過設備網路部署 Windows 作業系統。 它也會裝載的 DHCP 服務，也可讓設備主機，而不需要預先設定的 IP 位址加入設備的網路。  
  
*Appliance_domain*-WDS 虛擬機器上 HST01 執行，並可以容錯移轉至 HST02。 WDS 虛擬機器和 VMM 虛擬機器，請在實體主機上部署 Windows，應用裝置安裝期間。 在應用裝置生命週期中，WDS 和 VMM 執行作業，例如取代主機。  
  
*appliance_domain*-VMM  
Virtual Machine Manager (VMM) 虛擬機器中執行，並可以容錯移轉至 HST02。 VMM 會裝載 System Center 部署在實體主機上的作業系統。 VMM 也會提供 Windows Server Update Services (WSUS) 即可套用或移除所有主機和虛擬機器的 Windows 更新。  
  
*appliance_domain*-AD01， *appliance_domain*-ad02 移  
虛擬機器中的 active Directory 網域服務，其中包含網域名稱系統 (DNS)，是同時 HST01 和 HST02 上執行。 應用裝置的高可用性，AD01 和 ad02 移為複寫的網域控制站，就無法容錯移轉。 如果其中一個失敗，另一個已有正確的資料。  
  
*appliance_domain*-ISCSI01  
在每部主機上的一個 ISCSI 的虛擬機器是以連接存放裝置 (HSA01 HSA06) 執行。 此 VM 會容錯移轉。  
  
### <a name="hosts"></a>主控件  
*appliance_domain*-透過 HST01 *appliance_domain*-HST06  
PDW 控制節點和設備 fabric 虛擬機器的主機。 HST03 是選擇性的被動主應用程式。  
  
*appliance_domain*-透過 HSA01 *appliance_domain*-HSA08  
使用儲存體主機附加 (HSA)。 每個 HAS 主機執行一個計算節點 VM，另一個 ISCSI VM。  
  
### <a name="cluster-for-pdw"></a>適用於 PDW 的叢集  
*appliance_domain*-WFOHST01  
PDW 叢集稱為 WFOHST01。 它會管理所有的實體主機和虛擬機器屬於 PDW。  
  
### <a name="direct-attached-storage"></a>直接連結存放裝置  
*appliance_domain*-透過 DAS01 *appliance_domain*-DAS03  
這是連接到計算節點的直接連結存放裝置。 HP 都有一個 DAS 每隔兩個計算節點。 Dell 和配量都有一個 DAS 每隔三個計算節點。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[設備設定&#40;Analytics Platform System&#41;](appliance-configuration.md)  
[設備管理工作&#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
