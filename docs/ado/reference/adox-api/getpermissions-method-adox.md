---
title: "GetPermissions 方法 (ADOX) |Microsoft 文件"
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
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 542abb8ab3c8fb5857508b4fafb6f50412c825bb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getpermissions-method-adox"></a>GetPermissions 方法 (ADOX)
傳回的權限[群組](../../../ado/reference/adox-api/group-object-adox.md)或[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件或物件容器上。  
  
## <a name="syntax"></a>語法  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，指定包含群組或使用者具有物件的權限的位元遮罩。 這個值可以是下列其中一個或多個[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)常數。  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 A **Variant**值，指定要設定權限的物件名稱。 設定*名稱*為 null 的值，如果您想要取得的物件容器的權限。  
  
 *ObjectType*  
 A**長**值可以是下列其中之一的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)常數，指定要取得權限的物件類型。  
  
 *ObjectTypeId*  
 選擇性。 A **Variant** OLE DB 規格所定義的值，未指定提供者物件類型的 GUID。 這個參數是必要項，如果*ObjectType*設**adPermObjProviderSpecific**，否則不會使用它。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[群組物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[使用者物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name 屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)

