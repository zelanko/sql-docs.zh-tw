---
title: GetPermissions 方法 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5f5b2a5170b499f5e88d4caac4822d2998691eea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966221"
---
# <a name="getpermissions-method-adox"></a>GetPermissions 方法 (ADOX)
傳回的權限[群組](../../../ado/reference/adox-api/group-object-adox.md)或是[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件或物件容器上。  
  
## <a name="syntax"></a>語法  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，指定包含使用者或群組具有物件的權限的位元遮罩。 這個值可以是一種或多種[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常數。  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 A **Variant**值，指定要設定權限的物件名稱。 設定*名稱*為 null 的值，如果您想要取得的物件容器的權限。  
  
 *ObjectType*  
 A**長**可以是其中一值的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常數，指定要取得權限的物件型別。  
  
 *ObjectTypeId*  
 選擇性。 A **Variant** OLE DB 規格所定義的值，不指定提供者物件類型的 GUID。 如果此參數，則需要*ObjectType*設為**adPermObjProviderSpecific**，否則不會使用它。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Group 物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name 屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
