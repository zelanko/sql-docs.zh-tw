---
title: 硬體元件
description: 分析平臺系統（AP）使用可擴充的元件，因此您可以根據業務需求購買正確的處理和儲存體數量。 當您訂購 AP 時，您將需要這些核心硬體元件的組合。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: db9966315d60fd4de1de7ae6805620d3f2144e6f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401138"
---
# <a name="hardware-components-for-analytics-platform-system"></a>分析平臺系統的硬體元件

分析平臺系統（AP）使用可擴充的元件，因此您可以根據業務需求購買正確的處理和儲存體數量。 當您訂購 AP 時，您將需要這些核心硬體元件的組合。 特定硬體廠商可能會使用不同的命名慣例或具有其他元件。  
 
  
## <a name="rackandnetwork"></a>機架和網路 
 
AP 元件全都儲存在一或多個符合您資料中心的機架中。 每個機架都隨附配電裝置（Pdu）、兩個不強大的交換器，以及兩個乙太網路交換器。  
  
![機架和網路](media/rack-and-network.png "AP 機架和網路")  
  
## <a name="datascaleunit"></a>資料縮放單位
 
資料縮放單位包含資料主機和直接連接儲存體（DAS），可用於處理和儲存使用者資料。 若要新增容量，您可以根據硬體廠商支援的設定來新增資料縮放單位。 隨著資料縮放單位數目的增加，您必須視需要新增額外的機架 & 網路元件，以提供更多的電源、網路和機架的基礎結構。  
  
### <a name="data-host"></a>資料主機  

「資料主機」是專門用來處理使用者資料的伺服器。 平行處理資料倉儲（PDW）會在每個資料主機上執行一個計算節點。 針對 HPE 設備，資料縮放單位有兩個數據主機。 針對 Dell 和量程設備，資料縮放單位有三個數據主機。  
  
### <a name="direct-attached-storage"></a>直接連接的儲存體
 
直接連接存放裝置（DAS）是連接至資料主機的磁片集區。 所有的資料主機都可以存取任何磁片。 在不共用任何架構的情況下，在資料主機上執行的計算節點不會共用個別磁片。 不過，為了達到高可用性，會共用儲存體存取，而且每個資料主機都可以存取任何磁片。  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>資料縮放單位架構-DELL 和量子
  
![擴充性單位](media/scalability-unit-dell.png "Dell 擴充性單位")  
  
### <a name="data-scale-unit-architecture---hpe"></a>資料縮放單位架構-HPE 
 
![HPE 的擴充性單位](media/scalability-unit-hpe.png "HPE 的擴充性單位")  
  
### <a name="data-scale-unit-description"></a>資料縮放單位描述

資料縮放單位有一個伺服器（主機）適用于每個計算節點，以及一個連接到序列連結 SCSI （SAS）的直接連接磁片陣列。 在存放裝置封包中，磁片陣列分成兩個部分，每個都有多餘的電源供應器。 Windows Server 儲存空間會藉由跨 RAID 1 鏡像磁片配對來複製資料，來管理使用者資料。 每個磁片配對中的磁片會儲存在磁片陣列的不同部分。  
  
磁片陣列也包含熱備用磁片和系統磁片。 如果磁片故障，儲存空間會使用正常運作磁片上的正確資料複本，在熱備件上重建重複的資料複本。 這是一項重要的自我修復功能，可協助防止資料遺失。  
  
計算節點的磁片總數：  
  
-   DELL 有96個磁片 = （3部伺服器） * （每部伺服器 16 \*個磁片）（2個用於冗余磁片）。  
  
-   HPE 有64個磁片 = （2部伺服器） * （每部伺服器 16 \*個磁片）（2個用於冗余磁片）。  
  
-   此外，每個磁碟陣列都具有熱備用磁片和系統磁片。  
  
**為了達到高可用性**，當計算節點故障時，它仍然可以透過資料縮放單位中的其他主機來運作並存取其使用者資料。 至少有一個直接連接的實體主機必須運作，或儲存體的資料存取遺失。  
  
**針對磁片大小**，直接連接的存放裝置可以有1、2或 3 tb 的磁片磁碟機。 所有資料縮放單位都必須有相同大小的磁片。  
  
## <a name="basescaleunit"></a>基本縮放單位 
 
基礎縮放單位包含設備所需的大腦電力主機、資料主機和直接連接儲存體的最小數目。 其中包含下列元件。 
  
### <a name="orchestration-host"></a>協調流程主機  
這部伺服器會執行 PDW 的大腦。
  
### <a name="passive-host"></a>被動主機  
此伺服器提供高可用性。 它已上線，並已準備好執行工作，以防協調流程或資料主機失敗。 協調流程主機、被動主機和資料縮放單位伺服器會設定為 Windows 容錯移轉叢集。 設備中的每個機架都需要一個被動主機。  
  
### <a name="optional-passive-host"></a>選用的被動主機  
若要新增更多的複本，您可以選擇將第二個被動主機新增至基底縮放單位。  
  
### <a name="data-scale-unit"></a>資料縮放單位  
基底縮放單位包含一個放在機架底部的資料縮放單位。  
  
下圖顯示基底縮放單位加上機架和網路。 這是分析平臺系統裝置的最低設定。  
  
![基本縮放單位](media/base-scale-unit.png "基本縮放單位")  
 
