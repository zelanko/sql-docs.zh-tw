---
title: SetPermissions 方法（ADOX） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 94cc5b07c97bd5c8d7c7ae6c30c179e2555b95d5
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762779"
---
# <a name="setpermissions-method-adox"></a>SetPermissions 方法 (ADOX)
指定物件上[群組](../../../ado/reference/adox-api/group-object-adox.md)或[使用者](../../../ado/reference/adox-api/user-object-adox.md)的許可權。  
  
## <a name="syntax"></a>語法  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **字串**值，指定要為其設定許可權的物件名稱。  
  
 *ObjectType*  
 **Long**值，可以是其中一個[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常數，它會指定要取得許可權之物件的型別。  
  
 *動作*  
 **Long**值，可以是其中一個[ActionEnum](../../../ado/reference/adox-api/actionenum.md)常數，指定設定許可權時要執行的動作類型。  
  
 *權限*  
 **長**數值，可以是一或多個[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常數的位元遮罩，表示要設定的許可權。  
  
 *都會*  
 選擇性。 **Long**值，可以是其中一個[InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md)常數，指定物件將如何繼承這些許可權。 預設值為**adInheritNone**。  
  
 *ObjectTypeId*  
 選擇性。 **Variant**值，指定 OLE DB 規格未定義之提供者物件類型的 GUID。 如果*ObjectType*設定為**adPermObjProviderSpecific**，則需要這個參數。否則，就不會使用它。  
  
## <a name="remarks"></a>備註  
 如果提供者不支援設定群組或使用者的存取權限，就會發生錯誤。  
  
> [!NOTE]
>  呼叫**SetPermissions**時，將動作設定為**adAccessRevoke**會覆寫*許可權*參數的任何設定。 如果您想要*許可權*參數中指定的許可權生效，請勿將 [*動作*] 設定為 [ **adAccessRevoke** ]。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Group 物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例（VB）](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 方法（ADOX）](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name 屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
