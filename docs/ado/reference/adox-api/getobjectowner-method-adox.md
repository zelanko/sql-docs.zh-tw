---
description: GetObjectOwner 方法 (ADOX)
title: " (ADOX) 的 GetObjectOwner 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: rothja
ms.author: jroth
ms.openlocfilehash: f4acea759ba213eac4365d79fa040c20e5a673cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440040"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner 方法 (ADOX)
傳回 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md)中物件的擁有者。  
  
## <a name="syntax"></a>語法  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**字串**值，指定擁有物件的[使用者](../../../ado/reference/adox-api/user-object-adox.md)或[群組](../../../ado/reference/adox-api/group-object-adox.md)的[名稱](../../../ado/reference/adox-api/name-property-adox.md)。  
  
#### <a name="parameters"></a>參數  
 *ObjectName*  
 指定要傳回其擁有者之物件名稱的 **字串** 值。  
  
 *ObjectType*  
 **Long**值，可以是其中一個[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常數，指定要取得其擁有者的物件類型。  
  
 *ObjectTypeId*  
 選擇性。 **Variant**值，指定 OLE DB 規格未定義之提供者物件類型的 GUID。 如果 *ObjectType* 設定為 **adPermObjProviderSpecific**，則需要此參數。否則，就不會使用它。  
  
## <a name="remarks"></a>備註  
 如果提供者不支援傳回物件擁有者，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Catalog 物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetObjectOwner 和 SetObjectOwner 方法範例 (VB) ](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)
