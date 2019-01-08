---
title: 類型的資料指標 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db77de95e83e596a8a301fa65885ee640c742a71
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543556"
---
# <a name="types-of-cursors-ado"></a>資料指標的類型 (ADO)
一般而言，您的應用程式應該使用最簡單的資料指標，提供所需的資料存取。 進階功能 （順向、 唯讀、 靜態、 捲動、 未緩衝處理） 每個其他資料指標特性有價格-在用戶端記憶體、 網路負載或效能。 在許多情況下，預設資料指標選項會產生比應用程式真正需要更複雜資料指標。  
  
 您選擇的資料指標類型取決於您的應用程式如何使用結果集以及也幾個設計考量，包括大小的結果集，可能使用之資料的百分比、 資料變更與應用程式效能的敏感度需求。  
  
 其最基本功能，您的資料指標所選擇將取決於您是否需要變更，或只是檢視的資料：  
  
-   如果您只需要捲動的結果，但不是變更資料的一組，使用[順](../../../ado/guide/data/forward-only-cursors.md)或是[靜態](../../../ado/guide/data/static-cursors.md)資料指標。  
  
-   如果您有大型結果集和選取多個資料列的需要，使用[keyset](../../../ado/guide/data/keyset-cursors.md)資料指標。  
  
-   如果您想要同步處理的結果集與最近加入、 變更時，並刪除所有的並行使用者，請使用[動態](../../../ado/guide/data/dynamic-cursors.md)資料指標。  
  
 雖然每個資料指標類型似乎不同，但請注意，這些資料指標類型不是這麼多不同只是重疊的特性和選項的結果。  
  
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
