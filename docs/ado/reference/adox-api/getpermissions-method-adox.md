---
title: GetPermissions 方法（ADOX） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966221"
---
# <a name="getpermissions-method-adox"></a>GetPermissions 方法 (ADOX)
傳回物件或物件容器上的[群組](../../../ado/reference/adox-api/group-object-adox.md)或[使用者](../../../ado/reference/adox-api/user-object-adox.md)的許可權。  
  
## <a name="syntax"></a>語法  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**Long**值，指定包含群組或使用者對物件之許可權的位元遮罩。 這個值可以是一或多個[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常數。  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **Variant**值，指定要為其設定許可權的物件名稱。 如果您想要取得物件容器的許可權，請將 [*名稱*] 設定為 null 值。  
  
 *ObjectType*  
 **Long**值，可以是其中一個[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常數，它會指定要取得許可權之物件的型別。  
  
 *ObjectTypeId*  
 選擇性。 **Variant**值，指定 OLE DB 規格未定義之提供者物件類型的 GUID。 如果*ObjectType*設定為**adPermObjProviderSpecific**，則需要這個參數。否則，就不會使用它。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Group 物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例（VB）](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name 屬性（ADOX）](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
