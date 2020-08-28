---
description: SetObjectOwner 方法
title: SetObjectOwner 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::SetObjectOwner
- _Catalog::raw_SetObjectOwner
helpviewer_keywords:
- SetObjectOwner method [ADOX]
ms.assetid: e5170a37-9d6e-43db-bfb6-9b6631fa3048
author: rothja
ms.author: jroth
ms.openlocfilehash: d021d91f89032146cb87516e6d5dd486de946378
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983319"
---
# <a name="setobjectowner-method"></a>SetObjectOwner 方法
指定 [目錄](./catalog-object-adox.md)中物件的擁有者。  
  
## <a name="syntax"></a>語法  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>參數  
 *ObjectName*  
 **字串**值，指定要為其指定擁有者的物件名稱。  
  
 *ObjectType*  
 **Long**值，可以是指定擁有者類型的其中一個[ObjectTypeEnum](./objecttypeenum.md)常數。  
  
 *OwnerName*  
 **字串**值，指定要擁有物件的[使用者](./user-object-adox.md)或[群組](./group-object-adox.md)的[名稱](./name-property-adox.md)。  
  
 *ObjectTypeId*  
 選擇性。 **Variant**值，指定 OLE DB 規格未定義之提供者物件類型的 GUID。 如果 *ObjectType* 設定為 **adPermObjProviderSpecific**，則需要此參數。否則，就不會使用它。  
  
## <a name="remarks"></a>備註  
 如果提供者不支援指定物件擁有者，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Catalog 物件 (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetObjectOwner 和 SetObjectOwner 方法範例 (VB) ](./getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [GetObjectOwner 方法 (ADOX)](./getobjectowner-method-adox.md)