---
title: SetObjectOwner 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 50a02898c1694fa43b8bf522a1a1bca65300efda
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965233"
---
# <a name="setobjectowner-method"></a>SetObjectOwner 方法
指定[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)中物件的擁有者。  
  
## <a name="syntax"></a>語法  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>參數  
 *ObjectName*  
 **字串**值，指定要為其指定擁有者的物件名稱。  
  
 *ObjectType*  
 **Long**值，可以是指定擁有者類型的其中一個[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常數。  
  
 *OwnerName*  
 **字串**值，指定要擁有物件的[使用者](../../../ado/reference/adox-api/user-object-adox.md)或[群組](../../../ado/reference/adox-api/group-object-adox.md)的[名稱](../../../ado/reference/adox-api/name-property-adox.md)。  
  
 *ObjectTypeId*  
 選擇性。 **Variant**值，指定 OLE DB 規格未定義之提供者物件類型的 GUID。 如果*ObjectType*設定為**adPermObjProviderSpecific**，則需要這個參數。否則，就不會使用它。  
  
## <a name="remarks"></a>備註  
 如果提供者不支援指定物件擁有者，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Catalog 物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetObjectOwner 和 SetObjectOwner 方法範例（VB）](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)
