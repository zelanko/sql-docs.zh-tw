---
title: "Name 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c2bf66589dc841e7f543b166b432f39a0869b3f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="name-property-ado"></a>Name 屬性 (ADO)
表示物件的名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，指出物件的名稱。  
  
## <a name="remarks"></a>備註  
 使用**名稱**指派的名稱，或擷取的名稱屬性**命令**，**屬性**，**欄位**，或**參數**物件。  
  
 值是讀取/寫入上**命令**物件和唯讀**屬性**物件。  
  
 如**欄位**物件**名稱**是通常是唯讀。 不過，對於新**欄位**已附加至的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)，**名稱**是讀取/寫入之後才[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**已指定與此資料提供者已成功地加入新**欄位**藉由呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法**欄位**集合。  
  
 如**參數**物件尚未附加至[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合，**名稱**屬性是讀取/寫入。 針對附加**參數**物件和所有其他物件，**名稱**屬性是唯讀的。 若要在集合中是唯一沒有名稱。  
  
 您可以擷取**名稱**由序數參考之後, 您可以在物件直接依名稱參考物件的屬性。 例如，如果`rstMain.Properties(20).Name`產生`Updatability`，您可以接著參考這個屬性做為`rstMain.Properties("Updatability")`。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[命令物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Field 物件](../../../ado/reference/ado-api/field-object.md)|  
|[參數物件](../../../ado/reference/ado-api/parameter-object.md)|[屬性物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [屬性和名稱屬性範例 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [屬性和名稱屬性的範例 （VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   

