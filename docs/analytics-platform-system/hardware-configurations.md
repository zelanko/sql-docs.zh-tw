---
title: "硬體設定 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "讓您根據業務需求購買適合的處理和儲存體容量，Analytics Platform System (APS) 硬體的架構與可延展單位。"
ms.date: 01/05/2017
ms.topic: article
ms.assetid: f95945b7-97ae-4ab9-bae5-c792a516acea
caps.latest.revision: "9"
ms.openlocfilehash: 6762775fdec3cd3a01a372ed5c16fbc4a93c1426
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="hardware-configurations"></a>硬體設定
讓您根據業務需求購買適合的處理和儲存體容量，Analytics Platform System (APS) 硬體的架構與可延展單位。 應用裝置縮放儲存體的 SQL Server Parallel Data Wareouse (PDW) 從幾個 Tb 到超過 6 pb 計的資料。  
  
## <a name="contents"></a>目錄  
  
-   [一個機架組態](#section1)  
  
-   [多個機架組態](#section2)  

  
## <a name="section1"></a>一個機架組態  
第一個機架應用裝置中的包含執行 PDW 所需的元件。 機架和網路加上的基底擴充單元，最小應用裝置組態。 這些圖表顯示方式，可以設定的第一個設備的機架。 您可以有 2 到 9 的計算節點的第一個機架，根據硬體廠商。  
  
### <a name="first-rack-configurations---dell"></a>第一次機架組態-DELL  
DELL 應用裝置的最低設定有 3 個計算節點。 您可以加入第一個機架 9 的運算節點總共最多 2 的資料縮放單位。  
  
![第一個機架組態 Dell](media/first-rack-configurations-dell.png "Dell 第一個機架組態")  
  
### <a name="first-rack-configurations---hpe"></a>第一次機架組態-HPE  
HPE 應用裝置的最低設定有 2 個計算節點。 您可以加入第一個機架 8 運算節點總共最多 3 的資料縮放單位。  
  
![HPE 先機架組態 HPE](media/first-rack-configurations-hpe.png "HPE 先機架組態")  
  
## <a name="section2"></a>多個機架組態  
要新增容量至 PDW 中，您可以加入資料擴充單元，以及其他的機架 & 網路元件，提供適當的電源，視網路，並追蹤基礎結構。 每個額外的機架 & 網路需要被動的主機。  
  
每個硬體廠商指定資料比例單位可以加入指定您的應用裝置的容量的數。 我們建議您加入足夠的資料延展單位，以查看至少 20 %uplift 效能。 例如，加入一個資料的小數位數已經有 20 的資料比例單位的應用裝置的單位可能會導致較不明顯的效能提高。 網路優勢，不是值得的成本與努力。  
  
### <a name="scale-out-example---hpe"></a>範例-HPE 外延展  
下圖顯示包含 20 的計算節點 3 機架 HP 應用裝置。  
  
![20 個電腦節點 HPE 應用裝置](media/scale-out-hpe.png "HPE 應用裝置 20 個電腦節點")  
  
### <a name="scale-out-example--dell-quanta"></a>向外延展範例-DELL，配量  
下圖顯示包含 21 的計算節點 3 機架 DELL 或 Quanta 應用裝置。  
  
![Dell 應用裝置與 21 的計算節點](media/scale-out-dell.png "Dell 應用裝置與 21 的計算節點")  
 
