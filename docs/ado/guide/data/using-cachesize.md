---
title: "使用 CacheSize |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bdce85373638fc8884f50ab7b81abfbbabfe2d47
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="using-cachesize"></a>使用 CacheSize
使用**CacheSize**屬性，即可控制要從提供者的本機記憶體，一次擷取記錄數。 例如，如果**CacheSize**為 10 之後的第一個左,**資料錄集**物件，提供者擷取的前 10 個記錄到本機的記憶體。 隨著您瀏覽**資料錄集**物件，提供者傳回的資料從本機記憶體緩衝區。 一旦您跳過快取中的最後一筆記錄，則提供者會擷取從資料來源的接下來的 10 記錄至快取。  
  
> [!NOTE]
>  **CacheSize**根據**開啟資料列的最大**提供者特有的屬性 (在**屬性**集合**資料錄集**物件)。 您不能設定**CacheSize**大於值**開啟的最大資料列。** 若要修改提供者可以開啟的資料列數目，設定**開啟資料列的最大**。  
  
 值**CacheSize**可調整的生命期限內**資料錄集**物件，但變更此值只會影響快取中的記錄數目後的後續從資料來源擷取。 變更屬性值還不會變更目前的快取內容。  
  
 如果有較少的記錄，以讀取比**CacheSize**指定提供者會傳回其餘的記錄並不會發生錯誤。  
  
 A **CacheSize**不允許設定為 0，並傳回錯誤。  
  
 從快取擷取的記錄不會反映其他使用者對來源資料的同時變更。 若要強制更新的所有快取的資料，使用[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法。  
  
 如果**CacheSize**設定的值大於 1，巡覽方法 ([移動](../../../ado/reference/ado-api/move-method-ado.md)， [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) 可能會導致瀏覽至已刪除如果記錄已擷取之後，就會刪除記錄。 之後的初始項提取，後續的刪除動作將不會反映在您的資料快取直到您嘗試存取的資料值從已刪除的資料列。 不過，設定**CacheSize**設為 1 會排除這個問題因為無法擷取已刪除的資料列。
