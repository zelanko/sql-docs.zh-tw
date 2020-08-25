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
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400924"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>設備實體元件-Analytics Platform System
PDW 和設備網狀架構實體元件的名稱和描述。 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="component-diagrams"></a><a name="diagrams"></a>元件圖  
這會顯示實體元件的名稱，以及它們位於6個計算節點設備第一個機架中的位置。  
  
![PDW 區域元件名稱 - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
PDW 元件的實際名稱是 PDW 區功能變數名稱稱，後面接著虛線，後面接著元件名稱。 例如，如果 PDW 區功能變數名稱稱是 PDW123，則實際的名稱為 **PDW123-CTL01**、 **PDW123 pqth4a-cmp01**等。  
  
同樣地，設備網狀架構元件的實際名稱是設備網域，後面接著虛線，後面接著元件名稱。 例如，如果設備網域是 FSW123，則設備網狀架構 Vm 會是 **FSW123-WDS**、 **FSW123-AD01**、 **FSW123-VMM**等等。  
  
以下是具有6個計算節點之 PDW 區域的匯總視圖。  
  
![PDW 元件名稱](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw-components"></a><a name="pdw"></a>PDW 元件  
PDW 虛擬機器是 PDW 區域的一部分。  
  
*PDW_region*-CTL01  
執行控制節點的虛擬機器。 這會在 HST01 上執行，並可容錯移轉至 HST02。  
  
> [!WARNING]  
> SQL Server PDW 不支援使用 Hyper-v 管理員建立 CTL01 虛擬機器的快照集。 快照集會依賴本機儲存體，如果虛擬機器嘗試容錯移轉至其備份，將會導致錯誤。 建立快照集也會造成其他 VM 的可靠性問題，該 VM 會容錯移轉至被動伺服器。  
  
*PDW_region*-pqth4a-cmp01 至 *PDW_Region*-CMP06  
執行計算節點的虛擬機器。 在這6個計算節點圖中，透過 HSA06 HSA01 的主機會分別執行計算節點 Vm PQTH4A-CMP01 至 CMP06。  
  
## <a name="appliance-fabric-components"></a><a name="fabric"></a>設備網狀架構元件  
這些元件是設備網狀架構的一部分。  
  
### <a name="virtual-machines"></a>虛擬機器  
*appliance_domain*-WDS  
此虛擬機器裝載 Windows 部署服務的 (WDS) ，讓分析平臺系統使用透過設備網路部署 Windows 作業系統。 它也會裝載 DHCP 服務，這可讓設備主機加入設備網路，而不需要預先設定的 IP 位址。  
  
*Appliance_domain*WDS 虛擬機器會在 HST01 上執行，並可容錯移轉至 HST02。 WDS 虛擬機器和 VMM 虛擬機器，在設備安裝期間將 Windows 部署在實體主機上。 在設備生命週期期間，WDS 和 VMM 會執行像是更換主機的作業。  
  
*appliance_domain*-VMM  
Virtual Machine Manager (VMM) 會在虛擬機器中執行，並可容錯移轉至 HST02。 VMM 會裝載 System Center，以在實體主機上部署作業系統。 VMM 也提供 Windows Server Update Services (WSUS) 在所有主機和虛擬機器上套用或移除 Windows 更新。  
  
*appliance_domain*-AD01、 *appliance_domain*-AD02  
Active Directory Domain Services （包含網域名稱系統 (DNS) ）會在 HST01 和 HST02 上的虛擬機器中執行。 為了達到設備的高可用性，會將 AD01 和 AD02 複寫至網域控制站，而不會容錯移轉。 如果其中一個失敗，則會有另一個已提供正確資料。  
  
*appliance_domain*-ISCSI01  
其中一個 ISCSI 虛擬機器會在儲存儲存體 (HSA01-HSA06) 的每個主機上執行。 此 VM 不會容錯移轉。  
  
### <a name="hosts"></a>主機  
*appliance_domain*-HST01 至 *appliance_domain*-HST06  
PDW 控制項節點和設備網狀架構虛擬機器的主機。 HST03 是選擇性的被動主機。  
  
*appliance_domain*-HSA01 至 *appliance_domain*-HSA08  
已附加儲存體 (HSA) 的主機。 每個主機都會執行一個計算節點 VM 和一個 ISCSI VM。  
  
### <a name="cluster-for-pdw"></a>適用于 PDW 的叢集  
*appliance_domain*-WFOHST01  
PDW 叢集的名稱是 WFOHST01。 它會管理所有屬於 PDW 的實體主機和虛擬機器。  
  
### <a name="direct-attached-storage"></a>直接附加儲存體  
*appliance_domain*-DAS01 至 *appliance_domain*-DAS03  
這是連接到計算節點的直接連接儲存體。 HP 針對每個計算節點各有一個 DAS。 每三個計算節點的 Dell 和量子都有一個 DAS。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[設備配置 &#40;Analytics Platform System&#41;](appliance-configuration.md)  
[裝置管理工作 &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
