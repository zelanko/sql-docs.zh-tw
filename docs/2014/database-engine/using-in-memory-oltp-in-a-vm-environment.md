---
title: 在 VM 環境使用記憶體內部 OLTP |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 27ec7eb3-3a24-41db-aa65-2f206514c6f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7f7f04b04792167fe9c4733f3e066c362f3cae4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843055"
---
# <a name="using-in-memory-oltp-in-a-vm-environment"></a>在 VM 環境使用記憶體中的 OLTP
  伺服器虛擬化技術可協助您降低 IT 資本和作業成本，並透過改善的應用程式佈建、維護、可用性和備份/復原程序，達到更高的 IT 效率。 隨著最近的技術進步，可以更輕易地運用虛擬化技術，將複雜的資料庫工作負載合併。 本主題包括在虛擬化環境中使用 [!INCLUDE[hek_1](../includes/hek-1-md.md)] 的最佳作法。  
  
##  <a name="bkmk_memoryPreAllocation"></a> 記憶體預先配置  
 對虛擬化環境中的記憶體而言，更好的效能與增強的支援是基本考量。 您必須能夠依據虛擬機器的需求 (尖峰和非尖峰負載)，快速配置記憶體給虛擬機器，同時也要確保不會浪費記憶體。 有關如何在主機上執行的虛擬機器之間配置和管理記憶體，Hyper-V 動態記憶體功能可以加強這方面的靈活度。  
  
 將具有記憶體最佳化資料表的資料庫虛擬化時，需要修改虛擬化和管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一些最佳做法。 如果沒有記憶體最佳化資料表，則其中兩個最佳作法如下：  
  
-   如果您使用 MIN_SERVER_MEMORY，最好僅指派所需的記憶體數量，這樣才能保留足夠的記憶體給其他程序 (進而避免分頁)。  
  
-   不要設定太高的記憶體預先配置值。 否則，其他程序可能會在需要時，無法得到足夠的記憶體，而導致記憶體分頁。  
  
 如果您為具有經記憶體最佳化資料表的資料庫遵循上述作法，即使您有足夠的記憶體來復原資料庫，在嘗試還原和復原資料庫時，還是會導致資料庫陷入「復原暫止」狀態。 原因如下，當 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 啟動時，會將資料帶入記憶體的積極程度，更勝於動態記憶體配置將記憶體配置給資料庫。  
  
 **解決方式**  
  
 若要緩和這個問題，請預先配置足夠的記憶體給資料庫，以復原或重新啟動資料庫，而不是提供最小值，依賴動態記憶體在需要時提供額外的記憶體。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
