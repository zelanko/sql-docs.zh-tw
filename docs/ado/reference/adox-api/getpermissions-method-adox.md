---
description: GetPermissions 方法 (ADOX)
title: " (ADOX) 的 GetPermissions 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 31d2bd1d17f790a29674b99ee24a668876e53492
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984419"
---
# <a name="getpermissions-method-adox"></a>GetPermissions 方法 (ADOX)
傳回物件或物件容器上 [群組](./group-object-adox.md) 或 [使用者](./user-object-adox.md) 的許可權。  
  
## <a name="syntax"></a>語法  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 **Long** 值，指定包含群組或使用者對物件之許可權的位元遮罩。 這個值可以是一或多個 [RightsEnum](./rightsenum.md) 常數。  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **Variant**值，指定要為其設定許可權的物件名稱。 如果您想要取得物件容器的許可權，請將 *名稱* 設定為 null 值。  
  
 *ObjectType*  
 **Long**值，可以是其中一個[ObjectTypeEnum](./objecttypeenum.md)常數，指定要取得許可權之物件的類型。  
  
 *ObjectTypeId*  
 選擇性。 **Variant**值，指定 OLE DB 規格未定義之提供者物件類型的 GUID。 如果 *ObjectType* 設定為 **adPermObjProviderSpecific**，則需要此參數。否則，就不會使用它。  
  
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
 [名稱屬性 (ADOX) ](./name-property-adox.md)   
 [SetPermissions 方法 (ADOX)](./setpermissions-method-adox.md)