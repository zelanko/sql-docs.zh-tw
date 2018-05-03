---
title: 類型的資料指標 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44b7fb1d3ce996c541ce0ad719eb3b4396a8f775
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="types-of-cursors-ado"></a>類型的資料指標 (ADO)
一般而言，您的應用程式應該使用最簡單的資料指標，提供必要的資料存取。 每個其他資料指標特性超出基本知識 （順向、 唯讀、 靜態、 捲動、 無緩衝） 都有價格 — 在用戶端記憶體、 網路負載或效能。 在許多情況下，預設資料指標選項會產生更複雜的資料指標比實際需要您的應用程式。  
  
 資料指標類型的選擇取決於您的應用程式如何使用結果集以及數個設計考量，包括物件的結果集，可能使用之資料的百分比、 資料變更與應用程式效能的敏感度大小需求。  
  
 其最基本功能，資料指標選項將取決於您是否需要變更，或只是檢視的資料：  
  
-   如果您只需要捲動的結果，但不是變更資料的一組，使用[順向](../../../ado/guide/data/forward-only-cursors.md)或[靜態](../../../ado/guide/data/static-cursors.md)資料指標。  
  
-   如果您有大型結果集和選取幾個資料列的需要，使用[索引鍵集](../../../ado/guide/data/keyset-cursors.md)資料指標。  
  
-   如果您想要同步處理的結果集與最近新增、 變更，以及刪除所有的並行使用者，請使用[動態](../../../ado/guide/data/dynamic-cursors.md)資料指標。  
  
 雖然每個資料指標類型看起來不同，但請注意，這些資料指標類型不是許多不同的種類為重疊的特性和選項的結果。  
  
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
