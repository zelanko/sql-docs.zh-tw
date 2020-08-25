---
description: CacheSize 屬性 (ADO)
title: " (ADO) 的 CacheSize 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
author: rothja
ms.author: jroth
ms.openlocfilehash: d6654adc5cbf5b01435dbc95a2f630cf980cc6d5
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776357"
---
# <a name="cachesize-property-ado"></a>CacheSize 屬性 (ADO)
指出記錄 [集](./recordset-object-ado.md) 物件中從本機快取到記憶體中的記錄數目。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回必須大於0的 **Long** 值。 預設值為 1。  
  
## <a name="remarks"></a>備註  
 您可以使用 **CacheSize** 屬性來控制一次取出多少筆記錄到提供者的本機記憶體中。 例如，如果 **CacheSize** 為10，則在第一次開啟 **記錄集** 物件之後，提供者會將前10筆記錄抓取到本機記憶體中。 當您在 **記錄集** 物件中移動時，提供者會傳回本機記憶體緩衝區中的資料。 當您移動超過快取中的最後一筆記錄時，提供者會將資料來源中的接下來10筆記錄抓取到快取中。  
  
> [!NOTE]
>  **CacheSize**是以**記錄集**物件) 的**Properties**集合中 (的**最大開啟資料列**提供者特定屬性為基礎。 您無法將 **CacheSize** 設定為大於 **最大開啟資料列**的值。 若要修改提供者可以開啟的資料列數目，請設定 [ **開啟**的資料列數上限]。  
  
 **CacheSize**的值可以在**記錄集**物件的存留期間進行調整，但變更此值只會影響自資料來源的後續檢索之後，快取中的記錄數目。 單獨變更屬性值不會變更快取的目前內容。  
  
 如果要抓取的記錄少於 **CacheSize** 指定，則提供者會傳回剩餘的記錄，而且不會發生任何錯誤。  
  
 不允許零的 **CacheSize** 設定，而且會傳回錯誤。  
  
 從快取取出的記錄不會反映其他使用者對來源資料所做的並行變更。 若要強制更新所有快取的資料，請使用 [Resync](./resync-method.md) 方法。  
  
 如果 **CacheSize** 設定為大於1的值，則導覽方法 ([Move](./move-method-ado.md)、 [MoveFirst、MoveLast、MoveNext 和 MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) 可能會導致導覽至已刪除的記錄，如果在抓取記錄之後發生刪除的情況。 初始提取之後，在您嘗試從已刪除的資料列存取資料值之前，後續的刪除將不會反映在您的資料快取中。 但是，將 **CacheSize** 設定為 one 會排除這個問題，因為無法提取刪除的資料列。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 CacheSize 屬性範例 ](./cachesize-property-example-vb.md)   
 [CacheSize 屬性範例 (VC + +) ](./cachesize-property-example-vc.md)   
 [CacheSize 屬性範例 (JScript)](./cachesize-property-example-jscript.md)