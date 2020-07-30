---
title: Name 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
author: rothja
ms.author: jroth
ms.openlocfilehash: 368def89951e7d0eacca9b999b647abd949c3b10
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243229"
---
# <a name="name-property-ado"></a>Name 屬性 (ADO)
指出物件的名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回表示物件名稱的**字串**值。  
  
## <a name="remarks"></a>備註  
 使用 [**名稱**] 屬性可將名稱指派給或取出**命令**、**屬性**、**欄位**或**參數**物件的名稱。  
  
 在**命令**物件上的值是讀取/寫入，而在**屬性**物件上為唯讀。  
  
 如果是**欄位**物件，**名稱**通常是唯讀的。 不過，對於已附加至[記錄](../../../ado/reference/ado-api/record-object-ado.md)之[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**欄位**物件，只有在指定**欄位**的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性，且資料提供者已藉由呼叫**Fields**集合的[Update](../../../ado/reference/ado-api/update-method.md)方法來成功加入新**欄位**之後，**名稱**才會是讀取/寫入。  
  
 對於尚未附加至[Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合的**參數**物件， **Name**屬性是讀取/寫入。 對於附加的**參數**物件和所有其他物件而言， **Name**屬性是唯讀的。 名稱在集合中不需要是唯一的。  
  
 您可以使用序數參考抓取物件的**Name**屬性，之後您就可以直接依名稱參考該物件。 例如，如果 `rstMain.Properties(20).Name` 產生 `Updatability` ，您之後就可以將這個屬性稱為 `rstMain.Properties("Updatability")` 。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
        [Field 物件](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)  
        [Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [Attributes 和 Name 屬性範例（VB）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Attributes 和 Name 屬性範例（VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
