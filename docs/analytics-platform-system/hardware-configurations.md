---
title: 硬體設定
description: 分析平臺系統（AP）設備硬體會以可調整的單位進行架構，讓您根據業務需求購買正確的處理和儲存體數量。 設備可將平行處理資料倉儲的儲存體從數 tb 調整至超過 6 pb 的資料。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee16045931da345f06c141597ccd25d19a36dea7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401137"
---
# <a name="hardware-configurations---analytics-platform-system"></a>硬體設定-Analytics Platform System
分析平臺系統（AP）硬體會以可擴充的單位進行架構，讓您根據業務需求購買正確的處理和儲存體數量。 設備可將 SQL Server Parallel Data Wareouse （PDW）的儲存體從數 Tb 調整為超過 6 Pb 的資料。  
  
## <a name="contents"></a>內容  
  
-   [一機架設定](#section1)  
  
-   [多機架設定](#section2)  

  
## <a name="section1"></a>一機架設定  
設備中的第一個機架包含執行 PDW 所需的元件。 最小設備設定是一個機架和網路，再加上一個基本的縮放單位。 這些圖表會顯示裝置的第一個機架的設定方式。 您的第一個機架中可以有2到9個計算節點，視硬體廠商而定。  
  
### <a name="first-rack-configurations---dell"></a>第一個機架設定-DELL  
DELL 設備的最低設定具有3個計算節點。 您最多可以將2個數據縮放單位新增至第一個機架，總共9個計算節點。  
  
![Dell 第一個機架設定](media/first-rack-configurations-dell.png "Dell 第一個機架設定")  
  
### <a name="first-rack-configurations---hpe"></a>第一個機架設定-HPE  
HPE 設備的最低設定有2個計算節點。 您最多可以將3個數據縮放單位新增至第一個機架，總共8個計算節點。  
  
![適用于 HPE 的 HPE 第一個機架設定](media/first-rack-configurations-hpe.png "HPE 第一個機架設定")  
  
## <a name="section2"></a>多機架設定  
若要將容量新增至 PDW，您可以視需要新增資料縮放單位以及額外的機架 & 網路元件，以提供適當的電源、網路和機架基礎結構。 每個額外的機架 & 網路都需要被動主機。  
  
每個硬體廠商都會指定您的應用裝置容量可新增的資料縮放單位數目。 我們建議您新增足夠的資料縮放單位，以在效能中至少看到20% 的升級。 例如，將一個資料縮放單位新增至已有20個數據縮放單位的應用裝置，可能會導致效能得到微不足道。 Net 增益並不值得成本和努力。  
  
### <a name="scale-out-example---hpe"></a>相應放大範例-HPE  
此圖顯示包含20個計算節點的3個機架 HP 應用裝置。  
  
![具有20個計算節點的 HPE 應用裝置](media/scale-out-hpe.png "具有20個計算節點的 HPE 應用裝置")  
  
### <a name="scale-out-example---dell-quanta"></a>Scale Out 範例-DELL、量子  
此圖顯示3個機架的 DELL 或量子設備，其中包含21個計算節點。  
  
![具有21個計算節點的 Dell 設備](media/scale-out-dell.png "具有21個計算節點的 Dell 設備")  
 
