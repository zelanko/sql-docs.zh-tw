---
title: 資料指標的類型（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: rothja
ms.author: jroth
ms.openlocfilehash: 4953b0509cade52a8badd8d578c9fa13f0c2b42b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759044"
---
# <a name="types-of-cursors-ado"></a>資料指標的類型 (ADO)
一般的規則是，您的應用程式應該使用最簡單的資料指標，以提供所需的資料存取權。 除了基本概念（順向、唯讀、靜態、滾動、無緩衝）以外的每個額外資料指標特性，都有一個價格，包括用戶端記憶體、網路負載或效能。 在許多情況下，預設資料指標選項會產生比應用程式實際所需更複雜的資料指標。  
  
 您選擇的資料指標類型取決於您的應用程式使用結果集的方式，以及數個設計考慮，包括結果集的大小、可能使用的資料百分比、資料變更的敏感度，以及應用程式效能需求。  
  
 在最基本的情況下，您的資料指標選擇取決於您是否需要變更或只是要查看資料：  
  
-   如果您只需要滾動一組結果，而不是變更資料，請使用順[向](../../../ado/guide/data/forward-only-cursors.md)或[靜態](../../../ado/guide/data/static-cursors.md)資料指標。  
  
-   如果您有大型的結果集，而且只需要選取幾個資料列，請使用索引[鍵集](../../../ado/guide/data/keyset-cursors.md)資料指標。  
  
-   如果您想要同步處理結果集與最近的所有並行使用者加入、變更和刪除，請使用[動態](../../../ado/guide/data/dynamic-cursors.md)資料指標。  
  
 雖然每個資料指標類型看起來都是相異的，但請記住，這些資料指標類型並不像是重迭的特性和選項的結果，也不會有太大的不同。  
  
 此章節包含下列主題。  
  
-   [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [靜態資料指標](../../../ado/guide/data/static-cursors.md)  
  
-   [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)  
  
-   [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>另請參閱  
 [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)   
 [靜態資料指標](../../../ado/guide/data/static-cursors.md)   
 [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)   
 [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)
