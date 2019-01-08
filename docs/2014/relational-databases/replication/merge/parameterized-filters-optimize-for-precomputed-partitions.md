---
title: 使用預先計算的資料分割最佳化參數化篩選效能 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication], about precomputed partitions
ms.assetid: 85654bf4-e25f-4f04-8e34-bbbd738d60fa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8f80afa10c1dbd067648db26c2bed0f423f371b7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800171"
---
# <a name="optimize-parameterized-filter-performance-with-precomputed-partitions"></a>使用預先計算的資料分割最佳化參數化篩選效能
  預先計算的資料分割是可用於篩選合併式發行集的效能最佳化。 預先計算的資料分割也是在篩選發行集上使用邏輯記錄的需求。 如需邏輯記錄的詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](group-changes-to-related-rows-with-logical-records.md)。  
  
 當「訂閱者」與「發行者」同步時，「發行者」必須評估「訂閱者」的篩選以決定哪些資料列屬於該「訂閱者」的資料分割或資料集。 在發行者端針對每一個接收到已篩選資料集來判斷變更的資料分割成員資格之處理，稱為 *資料分割評估*。 若沒有預先計算的資料分割，則自從上次為特定的「訂閱者」執行「合併代理程式」之後，必須對「發行者」端的篩選資料行所作之變更執行資料分割評估，而且每個與「發行者」同步的「訂閱者」都必須重複這個過程。  
  
 但是，如果「發行者」和「訂閱者」正在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本上執行並使用預先計算的資料分割，則在進行變更時，「發行者」端所有變更的資料分割成員資格會被預先計算並保存。 如此一來，訂閱者與發行者同步處理時，它可以立即啟動來下載與其資料分割相關的變更，不必再經過資料分割評估處理。 當發行集內有大量的變更、訂閱者或發行項時，如此就可以大幅提高效能。  
  
 除了使用預先計算的資料分割之外，請預先產生快照集並/或允許「訂閱者」在第一次進行同步處理時要求產生並套用快照集。 使用上述一或兩個選項為使用參數化篩選的發行集提供快照集。 如果不指定任何選項，訂閱會使用一系列 SELECT 與 INSERT 陳述式進行初始化，而非使用 **bcp** 公用程式；此處理要慢很多。 如需詳細資訊，請參閱＜ [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md)＞。  
  
 **使用預先計算的資料分割**  
  
 依預設，在所有遵守上述指導方針之新的及現有的發行集上，都會啟用預先計算的資料分割。 此設定可透過 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或以程式設計的方式來變更。 如需詳細資訊，請參閱＜ [Optimize Parameterized Row Filters](../publish/optimize-parameterized-row-filters.md)＞。  
  
## <a name="requirements-for-using-precomputed-partitions"></a>使用預先計算的資料分割之需求  
 如果滿足下列需求，依預設，會使用啟用的預先計算之資料分割來建立新的合併式發行集，並且會自動升級現有發行集以使用此功能。 如果發行集不滿足這些需求，則可以對其進行變更，然後便可啟用預先計算的資料分割。 如果只有其中一部份發行項滿足這些需求，則考慮建立兩個發行集，其中一個啟用預先計算的資料分割。  
  
### <a name="requirements-for-filter-clauses"></a>篩選子句的需求  
  
-   任何用於參數化資料列篩選器的函數，例如 HOST_NAME() 和 SUSER_SNAME()，應直接出現在參數化篩選子句中，不可巢狀包含在檢視或動態函數中。 如需這些函式的詳細資訊，請參閱 [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql)、[SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql) 和[參數化資料列篩選](parameterized-filters-parameterized-row-filters.md)。  
  
-   在建立資料分割後不應變更每個「訂閱者」傳回的值。 例如，如果您在篩選中使用 HOST_NAME() (沒有覆寫 HOST_NAME() 值)，則不要變更「訂閱者」端的電腦名稱。  
  
-   聯結篩選不應包含動態函數 (例如依據正進行同步處理的「訂閱者」，評估為不同值的 HOST_NAME() 與 SUSER_SNAME() 函數)。 僅參數化資料列篩選器應包含動態函數。  
  
-   非決定性函數不能用於篩選子句。 如需有關不具決定性函數的詳細資訊，請參閱＜ [Deterministic and Nondeterministic Functions](../../user-defined-functions/deterministic-and-nondeterministic-functions.md)＞。  
  
-   聯結篩選子句或參數化篩選子句中所參考的檢視不應包含動態函數。  
  
-   發行集中不應有循環聯結篩選關聯性。  
  
### <a name="database-collation"></a>資料庫定序  
  
-   如果使用預先計算的資料分割，則在進行比較時總是使用資料庫的定序，而不是資料表或資料行的定序。 請考慮下列案例：  
  
    -   區分大小寫定序的資料庫包含不區分大小寫定序的資料表。  
  
    -   資料表包含 **ComputerName**資料列，用來與參數化篩選中「訂閱者」的主機名稱作比較。  
  
    -   資料表在此資料行中包含一個值為 MYCOMPUTER 的資料列，及一個值為 mycomputer 的資料列。  
  
     如果「訂閱者」用主機名稱 mycomputer 來進行同步處理，則「訂閱者」僅會接收一個資料列，因為比較會區分大小寫 (資料庫的定序)。 如果未使用預先計算的資料分割，則「訂閱者」會接收兩個資料列，因為資料表具有不區分大小寫的定序。  
  
## <a name="performance-of-precomputed-partitions"></a>預先計算的資料分割之效能  
 當變更從「訂閱者」上傳到「發行者」時，預先計算的資料分割會有小的效能消耗，但是在評估資料分割及將變更從「發行者」下載到「訂閱者」會花費大量合併處理時間，因此網路優勢仍十分重要。 效能利益視同時進行同步處理的「訂閱者」數量，與每個將資料列從一個資料分割移到其他資料分割的同步處理之更新數量的不同而有所不同。  
  
## <a name="see-also"></a>另請參閱  
 [參數化資料列篩選器](parameterized-filters-parameterized-row-filters.md)  
  
  
