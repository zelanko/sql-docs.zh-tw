---
title: 硬體組態]-[Analytics Platform System |Microsoft Docs
description: Analytics Platform System (APS) 設備硬體方法具有結構性，與可調整的單位，讓您購買根據業務需求的正確數量的處理和儲存體。 應用裝置儲存體的平行處理資料倉儲從幾 tb 調整至 6 pb 以上的資料。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f3e1759dcde0dd792ce5179de08e9add1ef355e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960899"
---
# <a name="hardware-configurations---analytics-platform-system"></a>硬體組態]-[Analytics Platform System
Analytics Platform System (APS) 硬體的架構可調整的單位，以便您購買根據業務需求的正確數量的處理和儲存體。 設備調整儲存體的 SQL Server Parallel Data Wareouse (PDW) 從幾 tb 擴充到超過 6 Pb 的資料。  
  
## <a name="contents"></a>目錄  
  
-   [一個機架組態](#section1)  
  
-   [多重機架組態](#section2)  

  
## <a name="section1"></a>一個機架組態  
設備中的第一個機架都包含執行 PDW 所需的元件。 最小的設備組態是機架和網路，以及基底縮放單位。 這些圖表顯示的方式可以設定的第一個設備的機架。 您可以有 2 到 9 的第一個機架，取決於硬體供應商中的計算節點之間。  
  
### <a name="first-rack-configurations---dell"></a>第一次機架組態-DELL  
DELL 應用裝置的最低設定有 3 個計算節點。 您可以加入第一個機架，總共 9 個計算節點的最多 2 的資料縮放單位。  
  
![第一個機架組態 Dell](media/first-rack-configurations-dell.png "Dell 第一個機架組態")  
  
### <a name="first-rack-configurations---hpe"></a>第一次機架組態]-[HPE  
HPE 應用裝置的最低設定有 2 個計算節點。 您可以新增最多 3 個資料規模單位至第一個機架，總共 8 個計算節點。  
  
![HPE 先機架組態 HPE](media/first-rack-configurations-hpe.png "HPE 先機架組態")  
  
## <a name="section2"></a>多重機架組態  
若要將容量新增至 PDW 中，您可以將資料縮放單位，以及其他的機架 & 網路元件，提供適當的電源，視網路，並上架的基礎結構。 每個額外的機架 & 網路需要被動的主機。  
  
每個硬體廠商指定的資料規模單位可以加入指定的容量，您的應用裝置的數目。 我們建議您新增至少查看效能在百分之 20 uplift 足夠資料規模單位。 比方說，加入一個資料擴展至已有 20 個資料規模單位的應用裝置的單位可能會導致顯著的效能提升。 不錯的效益不是值得的成本與精力。  
  
### <a name="scale-out-example---hpe"></a>相應放大範例-HPE  
下圖顯示包含 20 個計算節點的 3 個機架 HP 設備。  
  
![HPE 設備與 20 個計算節點](media/scale-out-hpe.png "HPE 設備與 20 個計算節點")  
  
### <a name="scale-out-example---dell-quanta"></a>相應放大範例-DELL，配量  
下圖顯示包含 21 的計算節點的 3 個機架 DELL 或 Quanta 設備。  
  
![Dell 設備使用 21 的計算節點](media/scale-out-dell.png "Dell 設備使用 21 的計算節點")  
 
