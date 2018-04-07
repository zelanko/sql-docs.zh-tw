---
title: 分析平台系統的硬體元件
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: 如此您就可以根據您的業務需求購買適合的處理和儲存體容量，analytics Platform System (APS) 會使用可擴充的元件。
ms.date: 10/20/2016
ms.topic: article
ms.assetid: aa1cdcc7-cfee-4658-bbce-7d319bfb7483
caps.latest.revision: 17
ms.openlocfilehash: 4b972c4b926463a67588c4ee41ed0157da7cdc80
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="analytics-platform-system-hardware-components"></a>分析平台系統的硬體元件

如此您就可以根據您的業務需求購買適合的處理和儲存體容量，analytics Platform System (APS) 會使用可擴充的元件。 當您訂購 AP 時，您需要這些核心硬體元件的組合。 特定的硬體廠商可能會使用不同的命名慣例，或使用其他元件。  
 
  
## <a name="rackandnetwork"></a>機架和網路 
 
APS 元件會在一或多個放入您的資料中心的機架中儲存。 每個機架內建電源分配單元 (Pdu)、 兩個 InfiniBand 參數，以及兩個乙太網路交換器。  
  
![機架和網路](media/rack-and-network.png "APS 機架和網路")  
  
## <a name="datascaleunit"></a>資料縮放單位
 
資料擴充單元包含資料的主控件和直接連結存放裝置 (DAS) 來處理和儲存使用者資料。 若要增加容量，您會加入資料擴充單元，根據您的硬體廠商所支援的組態。 當資料縮放單位數目增加時，您需要加入其他機架 & 網路元件，如有必要，以提供更多電源、 網路和機架基礎結構。  
  
### <a name="data-host"></a>資料主機  

資料主機是專門用來處理使用者資料的伺服器。 Parallel Data Warehouse (PDW) 會執行一個計算節點，每個資料主機上。 資料擴充單元 HPE 裝置中，有兩個資料主機。 Dell 和配量應用裝置的資料擴充單元會有三個資料的主控件。  
  
### <a name="direct-attached-storage"></a>直接連結存放裝置
 
直接連結存放裝置 (DAS) 是一組資料主機連接的磁碟。 所有資料主機可以存取任何磁碟。 無共用 」 的一部分資料的主機上執行的計算節點的架構不會共用個別磁碟。 不過，高可用性，共用儲存體存取，而且每個資料主機可以存取任何磁碟。  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>資料縮放單位架構-DELL 和配量
  
![延展性單位](media/scalability-unit-dell.png "Dell 延展性單位")  
  
### <a name="data-scale-unit-architecture---hpe"></a>資料縮放單位架構 HPE 
 
![HPE 延展性單位](media/scalability-unit-hpe.png "HPE 延展性單位")  
  
### <a name="data-scale-unit-description"></a>資料的小數位數單元描述

資料擴充單元會針對每個計算節點和一個直接連接的磁碟陣列，附加與序列連接 SCSI (SAS) 有一部伺服器 （主機）。 中的封包的儲存體，磁碟陣列分為兩個部分各有備援電源供應器。 Windows Server 儲存空間管理使用者資料在 RAID 1 鏡像磁碟組之間複製資料。 在每個磁碟對磁碟會儲存在不同的磁碟陣列的一半。  
  
磁碟陣列也會包含熱備援磁碟與系統磁碟。 如果某個磁碟失敗，儲存空間會使用正常運作的磁碟上的資料複本重建複本上的熱備援的資料。 這是重要的自我修復功能，有助於防範資料遺失。  
  
運算節點的磁碟總數：  
  
-   DELL 有 96 磁碟 = （3 部伺服器） * （16 個磁碟，每一部伺服器） \* (2 備援磁碟)。  
  
-   HPE 有 64 部磁碟 = （2 部伺服器） * （16 個磁碟，每一部伺服器） \* (2 備援磁碟)。  
  
-   此外，每個磁碟陣列具有熱備援磁碟和系統磁碟。  
  
**高可用性**，當節點容錯移轉它的計算可以仍然函式及存取其使用者資料透過資料擴充單元中的其他主機。 至少一個直接附加的實體主機必須可以正常運作，或者遺漏資料存取存放裝置。  
  
**磁碟大小**，直接連結存放裝置可以有 1、 2 或 3 Tb 的磁碟機。 所有的資料縮放單位必須具有相同大小的磁碟。  
  
## <a name="basescaleunit"></a>基本比例單位 
 
基底延展單位包含大腦電源主控件、 資料主機，以及所需的應用裝置的直接連結存放裝置的最小數目。 它包含下列元件。  
  
### <a name="orchestration-host"></a>協調流程主控件  
此伺服器執行 PDW 的大腦。
  
### <a name="passive-host"></a>被動主機  
此伺服器提供高可用性。 它已上線而且準備好的協調流程或資料主機故障的情況下，執行工作。 協調流程主控件、 被動的主控件和資料的小數位數單元伺服器都會設定為 Windows 容錯移轉叢集。 應用裝置中的每個機架需要一個被動的主機。  
  
### <a name="optional-passive-host"></a>選擇性的被動主機  
若要新增進一步備援，您尚未新增第二個被動主應用程式的基底延展單位的選項。  
  
### <a name="data-scale-unit"></a>資料縮放單位  
基底延展單位包含一個資料縮放單位它放在底部的機架。  
  
這個圖表可顯示的基底延展單位加上機架和網路。 這是 Analytics Platform System 應用裝置的最低設定。  
  
![基底的延展單位](media/base-scale-unit.png "基本比例單位")  
 
