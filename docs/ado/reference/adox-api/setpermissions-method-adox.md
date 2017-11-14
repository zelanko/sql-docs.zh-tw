---
title: "SetPermissions 方法 (ADOX) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e830221fab599ace1304fb50ad8b0b22824e2bed
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setpermissions-method-adox"></a>SetPermissions 方法 (ADOX)
指定的權限[群組](../../../ado/reference/adox-api/group-object-adox.md)或[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件上。  
  
## <a name="syntax"></a>語法  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 A**字串**值，指定要設定權限的物件名稱。  
  
 *ObjectType*  
 A**長**值可以是下列其中之一的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常數，指定要取得權限的物件類型。  
  
 *動作*  
 A**長**值可以是下列其中之一的[ActionEnum](../../../ado/reference/adox-api/actionenum.md)常數，指定要設定權限時所執行的動作類型。  
  
 *權限*  
 A**長**值可以是位元遮罩的一或多個[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常數，表示權限設定。  
  
 *繼承*  
 選擇性。 A**長**值可以是下列其中之一的[InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md)常數，指定如何物件都會繼承這些權限。 預設值是**adInheritNone**。  
  
 *ObjectTypeId*  
 選擇性。 A **Variant**值，指定不由 OLE DB 規格定義的提供者物件類型的 GUID。 這個參數是必要項，如果*ObjectType*設**adPermObjProviderSpecific**，否則不會使用它。  
  
## <a name="remarks"></a>備註  
 如果提供者不支援設定存取權限的群組或使用者，會發生錯誤。  
  
> [!NOTE]
>  當呼叫**SetPermissions**，將動作設定為**adAccessRevoke**覆寫任何設定*權限*參數。 請勿設定*動作*至**adAccessRevoke**如果您想在指定的權限*權限*參數才會生效。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[群組物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[使用者物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name 屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)

