---
title: 硬體元件-Analytics Platform System |Microsoft Docs
description: Analytics Platform System (APS) 會使用可擴充的元件，以便您可以根據業務需求購買正確數量的處理和儲存體。 當您訂購 AP 時，您需要這些核心硬體元件的組合。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8cf7fd100f72e14b09ea086a1ebff5140a9068a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157376"
---
# <a name="hardware-components-for-analytics-platform-system"></a>Analytics Platform System 的硬體元件

Analytics Platform System (APS) 會使用可擴充的元件，以便您可以根據業務需求購買正確數量的處理和儲存體。 當您訂購 AP 時，您需要這些核心硬體元件的組合。 特定的硬體廠商可能會使用不同的命名慣例或其他元件。  
 
  
## <a name="rackandnetwork"></a>機架和網路 
 
APS 元件所有儲存在一或多個符合您的資料中心的機架。 每個機架隨附電源分配單元 (Pdu)、 兩個 InfiniBand 參數，以及兩個乙太網路交換器。  
  
![機架和網路](media/rack-and-network.png "APS 機架和網路")  
  
## <a name="datascaleunit"></a>資料縮放單位
 
在資料縮放單位會包含資料主機和直接連結存放裝置 (DAS) 來處理和儲存使用者資料。 若要增加容量，您會新增資料縮放單位，根據您的硬體廠商所支援的設定。 當資料縮放單位的數目增加時，您需要新增額外的機架 & 網路元件，如有必要，以提供更多能力、 網路和機架基礎結構。  
  
### <a name="data-host"></a>資料主機  

資料主機是專門用來處理使用者資料的伺服器。 Parallel Data Warehouse (PDW) 資料的每部主機上執行計算節點。 HPE 設備的資料縮放單位會有資料的兩部主機。 Dell 和配量的設備，資料縮放單位會有三個資料的主控件。  
  
### <a name="direct-attached-storage"></a>直接連結存放裝置
 
直接連結存放裝置 (DAS) 是與資料主機連接的磁碟集區。 所有資料主機可以存取的任何磁碟。 做為一部分無共用架構中，資料的主機上執行的計算節點不會共用個別磁碟。 不過，對於高可用性、 共用儲存體存取，而且每個資料主機可以存取的任何磁碟。  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>資料縮放單位架構-DELL 和配量
  
![延展性單位](media/scalability-unit-dell.png "Dell 延展性單位")  
  
### <a name="data-scale-unit-architecture---hpe"></a>資料縮放單位架構 HPE 
 
![HPE 延展性單位](media/scalability-unit-hpe.png "HPE 延展性單位")  
  
### <a name="data-scale-unit-description"></a>資料擴展單元描述

在資料縮放單位會有一部伺服器 （主機） 針對每個計算節點和一個直接連接的磁碟陣列附加使用序列連接 SCSI (SAS)。 封包的儲存體，磁碟陣列分成兩半各有冗餘電源供應器。 Windows Server 儲存空間來管理使用者資料在 RAID 1 鏡像磁碟配對之間複製資料。 每一磁碟對磁碟會儲存在磁碟陣列的不同部分。  
  
磁碟陣列也包含熱備援磁碟並為系統磁碟機。 如果磁碟故障時，儲存空間會使用正確的複本資料的正常運作的磁碟上重建的熱備援的資料複本。 這是一項重要自我修復功能，可協助保護避免資料遺失。  
  
計算節點的磁碟總數：  
  
-   DELL 有 96 磁碟 = （3 個伺服器） * （每一部伺服器的 16 個磁碟） \* (2 個備援磁碟)。  
  
-   HPE 有 64 個磁碟 = （2 個伺服器） * （每一部伺服器的 16 個磁碟） \* (2 個備援磁碟)。  
  
-   此外，每個磁碟陣列具有熱備援磁碟並為系統磁碟機。  
  
**高可用性**、 當計算節點容錯移轉，它可以仍能運作，並存取其使用者資料透過資料縮放單位中的其他主機。 直接附加的實體主機中至少一個必須可以正常運作或遺失的資料存取的儲存體。  
  
**磁碟大小的**，直接連結存放裝置可以有 1、 2 或 3 Tb 的磁碟機。 所有的資料縮放單位必須具有相同大小的磁碟。  
  
## <a name="basescaleunit"></a>基底的縮放單位 
 
基底縮放單位會包含核心分裂 power 主機、 資料主機及所需的應用裝置的直接連結存放裝置的最小數目。 它包含下列元件。 
  
### <a name="orchestration-host"></a>協調流程主控件  
此伺服器執行的 PDW。
  
### <a name="passive-host"></a>被動的主機  
此伺服器提供高可用性。 為上線狀態，準備好要執行作業，以防萬一發生失敗的協調流程或資料的主機。 協調流程主控件、 被動的主控件和資料規模單位伺服器都會設定為 Windows 容錯移轉叢集。 每個機架設備中的需要一個被動的主機。  
  
### <a name="optional-passive-host"></a>選擇性的被動主機  
進一步新增備援，您可以選擇第二個被動將主機新增至基底縮放單位。  
  
### <a name="data-scale-unit"></a>資料縮放單位  
基底縮放單位會包含一個資料縮放單位會放在機架底部。  
  
下圖顯示基底縮放單位，再加上的機架和網路。 這是 Analytics Platform System appliance 的最低設定。  
  
![基底的縮放單位](media/base-scale-unit.png "基底縮放單位")  
 
