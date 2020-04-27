---
title: 資料庫鏡像或 AlwaysOn 可用性群組（SQL Server）不支援跨資料庫交易 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c3616e40ff54c67d27902ddf9454084fb62e282
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62813653"
---
# <a name="cross-database-transactions-not-supported-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>資料庫鏡像或 AlwaysOn 可用性群組不支援跨資料庫交易 (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]或資料庫鏡像皆不支援跨資料庫交易和分散式交易。 這是因為無法確保交易不可部分完成性/完整性，原因如下：  
  
-   對於跨資料庫交易：每個資料庫都會獨立認可。 因此，即使資料庫是在單一可用性群組中，在某個資料庫認可交易之後，但在另一個資料庫認可交易之前可能會發生容錯移轉。 對於資料庫鏡像，此問題更為複雜，因為在容錯移轉之後，鏡像資料庫通常與另一個資料庫位於不同的伺服器執行個體，即使兩個資料庫是在相同的兩個夥伴之間建立鏡像，也無法確保這兩個資料庫會同時容錯移轉。  
  
-   對於分散式交易：在容錯移轉之後，新的主體伺服器/主要複本無法連接到先前主體伺服器/主要複本上的分散式交易協調器。 因此，新的主體伺服器/主要複本無法取得交易狀態。  
  
 下列資料庫鏡像範例將說明如何發生邏輯不一致的情況。 在此範例中，應用程式會使用跨資料庫交易來插入兩個資料列：其中一個資料列會插入鏡像資料庫 A 中的資料表，而另一個資料列則插入另一個資料庫 B 中的資料表。然後，資料庫 A 會在具有自動容錯移轉的高安全性模式下進行鏡像。 認可交易時，資料庫 A 會無法使用，而鏡像工作階段便自動容錯移轉至資料庫 A 的鏡像。  
  
 容錯移轉之後，在資料庫 B 上認可跨資料庫交易可能會成功，但不見得能順利在容錯移轉資料庫上認可。 如果資料庫 A 的原始主體伺服器在故障之前尚未將跨資料庫交易的記錄傳送至鏡像伺服器，就可能會發生這種情況。 容錯移轉之後，該筆交易不會存在新主體伺服器上。 資料庫 A 和 B 會成為不一致，因為插入資料庫 B 的資料仍維持完整，但是插入資料庫 A 的資料已經遺失。  
  
 使用 MS DTC 交易時可能也會發生類似的狀況。 例如，在容錯移轉之後，新的主體會連絡 MS DTC。 不過，MS DTC 並不了解新的主體伺服器，而且它會結束「準備認可」的所有交易，因為它認為這些交易已在其他資料庫中認可。  
  
> [!IMPORTANT]  
>  搭配 DTC 使用資料庫鏡像或可用性群組不會導致不支援 SQL Server 安裝。 不過，如果資料庫是資料庫鏡像工作階段或可用性群組的一部分，且 DTC 同時用於此資料庫，則 Microsoft 只會調查與搭配 DTC 使用資料庫鏡像或可用性群組無關的支援問題。  
  
  
