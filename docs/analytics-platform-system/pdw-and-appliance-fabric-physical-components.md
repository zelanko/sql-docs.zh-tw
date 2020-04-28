---
title: 設備實體元件
description: PDW 和設備網狀架構實體元件的名稱和描述。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5cbed66f53189668518e04848002ae69adb8c614
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400924"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>設備實體元件-Analytics Platform System
PDW 和設備網狀架構實體元件的名稱和描述。 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="component-diagrams"></a><a name="diagrams"></a>元件圖  
這會顯示實體元件的名稱，以及它們位於6計算節點設備第一個機架中的位置。  
  
![PDW 區域元件名稱 - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
PDW 元件的實際名稱是 PDW 區功能變數名稱稱，後面接著虛線，後面接著元件名稱。 例如，如果 PDW 區功能變數名稱稱為 PDW123，則實際名稱為**PDW123 CTL01**、 **PDW123-pqth4a-cmp01**等。  
  
同樣地，設備網狀架構元件的實際名稱是設備網域，後面接著虛線，再接著元件名稱。 例如，如果設備網域是 FSW123，則設備網狀架構 Vm 會是**FSW123-WDS**、 **FSW123-AD01**、 **FSW123-VMM**等等。  
  
以下是具有6個計算節點之 PDW 區域的匯總視圖。  
  
![PDW 元件名稱](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw-components"></a><a name="pdw"></a>PDW 元件  
PDW 虛擬機器是 PDW 區域的一部分。  
  
*PDW_region*-CTL01  
執行控制節點的虛擬機器。 這會在 HST01 上執行，而且可以故障切換至 HST02。  
  
> [!WARNING]  
> SQL Server PDW 不支援使用 Hyper-v 管理員建立 CTL01 虛擬機器的快照集。 快照集會依賴本機儲存體，如果虛擬機器嘗試容錯移轉至其備份，將會導致錯誤。 建立快照集也會造成容錯移轉到被動伺服器的其他 VM 的可靠性問題。  
  
*PDW_region*-透過*PDW_Region*-CMP06 的 pqth4a-cmp01  
執行計算節點的虛擬機器。 在此6個計算節點圖中，透過 HSA06 HSA01 的主機會分別執行計算節點 Vm PQTH4A-CMP01 至 CMP06。  
  
## <a name="appliance-fabric-components"></a><a name="fabric"></a>設備網狀架構元件  
這些元件是設備網狀架構的一部分。  
  
### <a name="virtual-machines"></a>虛擬機器  
*appliance_domain*-WDS  
這部虛擬機器裝載 Windows 部署服務（WDS），其分析平臺系統會使用透過應用裝置網路部署 Windows 作業系統。 它也會裝載 DHCP 服務，讓應用裝置主機可以加入設備網路，而不需要預先設定的 IP 位址。  
  
*Appliance_domain*WDS 虛擬機器會在 HST01 上執行，而且可以故障切換至 HST02。 WDS 虛擬機器和 VMM 虛擬機器，會在設備安裝期間于實體主機上部署 Windows。 在設備生命週期期間，WDS 和 VMM 會執行像是更換主機之類的作業。  
  
*appliance_domain*-VMM  
Virtual Machine Manager （VMM）會在虛擬機器中執行，而且可以故障切換到 HST02。 VMM 會主控 System Center，以在實體主機上部署作業系統。 VMM 也提供 Windows Server Update Services （WSUS）來套用或移除所有主機和虛擬機器上的 Windows 更新。  
  
*appliance_domain*-AD01， *appliance_domain*-AD02  
Active Directory Domain Services （其中包含網域名稱系統（DNS））會在 HST01 和 HST02 上的虛擬機器中執行。 針對設備的高可用性，AD01 和 AD02 是複寫的網域控制站，且不會容錯移轉。 如果其中一個失敗，則會有另一個已可使用正確的資料。  
  
*appliance_domain*-ISCSI01  
一部 ISCSI 虛擬機器在每個已附加儲存體的主機上執行（HSA01-HSA06）。 此 VM 不會容錯移轉。  
  
### <a name="hosts"></a>主機  
*appliance_domain*-透過*appliance_domain*-HST06 的 HST01  
PDW 控制節點和設備網狀架構虛擬機器的主機。 HST03 是選擇性的被動主機。  
  
*appliance_domain*-透過*appliance_domain*-HSA08 的 HSA01  
已附加儲存體的主機（RSA-HSA）。 每部主機都會執行一個計算節點 VM 和一個 ISCSI VM。  
  
### <a name="cluster-for-pdw"></a>適用于 PDW 的叢集  
*appliance_domain*-WFOHST01  
PDW 叢集的名稱是 WFOHST01。 它會管理屬於 PDW 的所有實體主機和虛擬機器。  
  
### <a name="direct-attached-storage"></a>直接連接的儲存體  
*appliance_domain*-透過*appliance_domain*-DAS03 的 DAS01  
這是連接到計算節點的直接連接儲存體。 HP 針對每兩個計算節點各有一個 DAS。 Dell 和量程對於每三個計算節點都有一個 DAS。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[設備設定 &#40;分析平臺系統&#41;](appliance-configuration.md)  
[&#40;分析平臺系統&#41;的裝置管理工作](appliance-management-tasks.md)  
  
