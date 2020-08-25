---
description: SetPermissions 方法 (ADOX)
title: " (ADOX) 的 SetPermissions 方法 |Microsoft Docs"
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
ms.openlocfilehash: 3a13e1dc23556888c2d4ee5c013472614b764d57
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769397"
---
# <a name="setpermissions-method-adox"></a>SetPermissions 方法 (ADOX)
指定物件上 [群組](./group-object-adox.md) 或 [使用者](./user-object-adox.md) 的許可權。  
  
## <a name="syntax"></a>語法  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **字串**值，指定要為其設定許可權的物件名稱。  
  
 *ObjectType*  
 **Long**值，可以是其中一個[ObjectTypeEnum](./objecttypeenum.md)常數，指定要取得許可權之物件的類型。  
  
 *動作*  
 **Long**值，可以是其中一個[ActionEnum](./actionenum.md)常數，指定設定許可權時要執行的動作類型。  
  
 *權限*  
 **Long**值，可以是一個或多個[RightsEnum](./rightsenum.md)常數的位元遮罩，表示要設定的許可權。  
  
 *繼承*  
 選擇性。 **Long**值，可以是其中一個[InheritTypeEnum](./inherittypeenum.md)常數，指定物件將如何繼承這些許可權。 預設值為 **adInheritNone**。  
  
 *ObjectTypeId*  
 選擇性。 **Variant**值，指定 OLE DB 規格未定義之提供者物件類型的 GUID。 如果 *ObjectType* 設定為 **adPermObjProviderSpecific**，則需要此參數。否則，就不會使用它。  
  
## <a name="remarks"></a>備註  
 如果提供者不支援設定群組或使用者的存取權限，就會發生錯誤。  
  
> [!NOTE]
>  呼叫 **SetPermissions**時，將動作設定為 **adAccessRevoke** 會覆寫 *許可權* 參數的任何設定。 如果您希望*rights*參數中指定的許可權生效，請勿將*動作*設定為**adAccessRevoke** 。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Group 物件 (ADOX)](./group-object-adox.md)  
    :::column-end:::
    :::column:::
        [User 物件 (ADOX)](./user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB) ](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions 方法 (ADOX) ](./getpermissions-method-adox.md)   
 [Name 屬性 (ADOX)](./name-property-adox.md)