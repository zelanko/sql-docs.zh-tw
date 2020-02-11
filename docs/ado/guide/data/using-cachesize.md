---
title: 使用 CacheSize |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2e3a67e9ad0f1f26f804ecb38e960041863fad9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923572"
---
# <a name="using-cachesize"></a>使用 CacheSize
您可以使用**CacheSize**屬性來控制要一次從提供者取得本機記憶體中的多少筆記錄。 例如，如果**CacheSize**是10，則在第一次開啟**記錄集**物件之後，提供者會將前10筆記錄抓取到本機記憶體。 當您在**記錄集**物件上移動時，提供者會傳回本機記憶體緩衝區中的資料。 當您移至快取中的最後一筆記錄之後，此提供者就會從資料來源將接下來10筆記錄抓取至快取中。  
  
> [!NOTE]
>  **CacheSize**是以**最大開啟資料列**提供者特定的屬性（在**記錄集**物件的**Properties**集合中）為基礎。 您無法將**CacheSize**設定為大於**最大開啟資料列**的值。 若要修改提供者可以開啟的資料列數目，請設定 [**開啟的最大資料列**數]。  
  
 **CacheSize**的值可以在**記錄集**物件的生命週期內進行調整，但變更此值只會影響從資料來源後續的檢索之後快取中的記錄數目。 單獨變更屬性值不會變更目前的快取內容。  
  
 如果要抓取的記錄少於**CacheSize**指定，則提供者會傳回其餘的記錄，而且不會發生錯誤。  
  
 不允許**CacheSize**設定為零，且會傳回錯誤。  
  
 從快取中取出的記錄不會反映其他使用者對來源資料所做的並行變更。 若要強制更新所有快取的資料，請使用[Resync](../../../ado/reference/ado-api/resync-method.md)方法。  
  
 如果**CacheSize**設定為大於1的值，流覽方法（[Move](../../../ado/reference/ado-api/move-method-ado.md)、 [MoveFirst、MoveLast、MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)）可能會導致導覽至已刪除的記錄（如果在抓取記錄之後發生刪除）。 初始提取之後，除非您嘗試從已刪除的資料列存取資料值，否則後續的刪除將不會反映在資料快取中。 不過，將**CacheSize**設定為1會排除這個問題，因為無法提取已刪除的資料列。
