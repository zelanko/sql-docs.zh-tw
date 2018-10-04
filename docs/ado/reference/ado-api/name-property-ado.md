---
title: Name 屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3717aa3ec95c92500d66c968446f7711a6cd4e74
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828646"
---
# <a name="name-property-ado"></a>Name 屬性 (ADO)
表示物件的名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，指出物件的名稱。  
  
## <a name="remarks"></a>備註  
 使用**名稱**屬性來指派的名稱，或擷取的名稱**命令**，**屬性**，**欄位**，或**參數**物件。  
  
 值會是讀取/寫入 on**命令**物件和唯讀**屬性**物件。  
  
 針對**欄位**物件，**名稱**是通常是唯讀。 不過，對於新**欄位**附加到的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)，**名稱**是讀取/寫入之後才[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**已指定與此資料提供者已成功地加入新**欄位**藉由呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法**欄位**集合。  
  
 針對**參數**物件尚未附加至[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合**名稱**屬性是讀取/寫入。 為附加**參數**物件和所有其他物件**名稱**屬性是唯讀的。 若要在集合中是唯一沒有名稱。  
  
 您可以擷取**名稱**由序數參考之後, 您可以對物件直接依名稱參考物件的屬性。 例如，如果`rstMain.Properties(20).Name`會產生`Updatability`，您可以接著參考此屬性維持`rstMain.Properties("Updatability")`。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Field 物件](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Attributes 和 Name 屬性範例 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Attributes 和 Name 屬性範例 （VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
