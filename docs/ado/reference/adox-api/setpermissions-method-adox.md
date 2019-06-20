---
title: SetPermissions 方法 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fcc44037ac746621c044bca755fd9b957356dc38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705800"
---
# <a name="setpermissions-method-adox"></a>SetPermissions 方法 (ADOX)
指定的權限[群組](../../../ado/reference/adox-api/group-object-adox.md)或是[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件上。  
  
## <a name="syntax"></a>語法  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 A**字串**值，指定要設定權限的物件名稱。  
  
 *ObjectType*  
 A**長**可以是其中一值的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常數，指定要取得權限的物件型別。  
  
 *動作*  
 A**長**可以是其中一值的[ActionEnum](../../../ado/reference/adox-api/actionenum.md)常數，指定要執行設定權限時的動作類型。  
  
 *權限*  
 A**長**可以是位元遮罩值的一或多個[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常數，表示要設定的權限。  
  
 *Inherit*  
 選擇性。 A**長**可以是其中一值的[InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md)常數，指定如何物件會繼承這些權限。 預設值是**adInheritNone**。  
  
 *ObjectTypeId*  
 選擇性。 A **Variant**值，指定不由 OLE DB 規格定義的提供者物件類型的 GUID。 如果此參數，則需要*ObjectType*設為**adPermObjProviderSpecific**，否則不會使用它。  
  
## <a name="remarks"></a>備註  
 如果提供者不支援設定存取權限的群組或使用者，會發生錯誤。  
  
> [!NOTE]
>  當呼叫**SetPermissions**，將動作設定為**adAccessRevoke**會覆寫的任何設定*權限*參數。 未設定*動作*要**adAccessRevoke**若要在指定的權限*權限*參數才會生效。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Group 物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name 屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
