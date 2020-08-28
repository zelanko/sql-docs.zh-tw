---
description: 使用 CacheSize
title: 使用 CacheSize |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: rothja
ms.author: jroth
ms.openlocfilehash: 97f6dba7bf01b3236d6b8b00e6338185cf6a8d41
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978999"
---
# <a name="using-cachesize"></a>使用 CacheSize
您可以使用 **CacheSize** 屬性來控制一次取出多少筆記錄到提供者的本機記憶體中。 例如，如果 **CacheSize** 為10，則在第一次開啟 **記錄集** 物件之後，提供者會將前10筆記錄抓取到本機記憶體中。 當您在 **記錄集** 物件中移動時，提供者會傳回本機記憶體緩衝區中的資料。 當您移動超過快取中的最後一筆記錄時，提供者會將資料來源中的接下來10筆記錄抓取到快取中。  
  
> [!NOTE]
>  **CacheSize**是以**記錄集**物件) 的**Properties**集合中 (的**最大開啟資料列**提供者特定屬性為基礎。 您無法將**CacheSize**設定為大於**最大開啟資料列**的值。 若要修改提供者可以開啟的資料列數目，請設定 [ **開啟**的資料列數上限]。  
  
 **CacheSize**的值可以在**記錄集**物件的存留期間進行調整，但變更此值只會影響自資料來源的後續檢索之後，快取中的記錄數目。 單獨變更屬性值不會變更快取的目前內容。  
  
 如果要抓取的記錄少於 **CacheSize** 指定，則提供者會傳回剩餘的記錄，而且不會發生任何錯誤。  
  
 不允許零的 **CacheSize** 設定，而且會傳回錯誤。  
  
 從快取取出的記錄不會反映其他使用者對來源資料所做的並行變更。 若要強制更新所有快取的資料，請使用 [Resync](../../../ado/reference/ado-api/resync-method.md) 方法。  
  
 如果將 **CacheSize** 設定為大於1的值，則導覽方法 ([Move](../../../ado/reference/ado-api/move-method-ado.md)、 [MoveFirst、MoveLast、MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) 可能會導致導覽至已刪除的記錄，如果在抓取記錄之後發生刪除的情況。 初始提取之後，在您嘗試從已刪除的資料列存取資料值之前，後續的刪除將不會反映在您的資料快取中。 但是，將 **CacheSize** 設定為1會排除這個問題，因為無法提取刪除的資料列。
