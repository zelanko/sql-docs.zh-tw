---
description: RightsEnum
title: RightsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
author: rothja
ms.author: jroth
ms.openlocfilehash: ead66b4c3215ef0d7a42e8ec029e97502dac2f4f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439550"
---
# <a name="rightsenum"></a>RightsEnum
指定物件之群組或使用者的許可權或許可權。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 ( # B0 H4000) |使用者或群組有權建立此類型的新物件。|  
|**adRightDelete**|65536 ( # B0 H10000) |使用者或群組具有從物件刪除資料的許可權。 對於 **資料表**之類的物件，使用者具有從記錄中刪除資料值的許可權。|  
|**adRightDrop**|256 ( # B0 H100) |使用者或群組具有從目錄中移除物件的許可權。 例如， **資料表** 可以由 DROP TABLE SQL 命令來刪除。|  
|**adRightExclusive**|512 ( # B0 H200) |使用者或群組具有獨佔存取物件的許可權。|  
|**adRightExecute**|536870912 ( # B0 H20000000) |使用者或群組有執行物件的許可權。|  
|**adRightFull**|268435456 ( # B0 H10000000) |使用者或群組擁有物件的擁有權限。|  
|**adRightInsert**|32768 ( # B0 H8000) |使用者或群組具有插入物件的許可權。 對於 **資料表**之類的物件，使用者具有將資料插入資料表中的許可權。|  
|**adRightMaximumAllowed**|33554432 ( # B0 H2000000) |使用者或群組具有提供者允許的最大許可權數目。 特定許可權視提供者而定。|  
|**adRightNone**|0|使用者或群組沒有物件的許可權。|  
|**adRightRead**|-2147483648 (&H80000000)|使用者或群組有讀取物件的許可權。 對於 [資料表](../../../ado/reference/adox-api/table-object-adox.md)之類的物件，使用者有權讀取資料表中的資料。|  
|**adRightReadDesign**|1024 ( # B0 H400) |使用者或群組有權讀取物件的設計。|  
|**adRightReadPermissions**|131072 ( # B0 H20000) |使用者或群組可以在目錄中查看物件的特定許可權，但不能變更。|  
|**adRightReference**|8192 ( # B0 H2000) |使用者或群組具有參考物件的許可權。|  
|**adRightUpdate**|1073741824 ( # B0 H40000000) |使用者或群組具有更新物件的許可權。 對於 **資料表**之類的物件，使用者有權更新資料表中的資料。|  
|**adRightWithGrant**|4096 ( # B0 H1000) |使用者或群組具有授與物件使用權限的許可權。|  
|**adRightWriteDesign**|2048 ( # B0 H800) |使用者或群組有權修改物件的設計。|  
|**adRightWriteOwner**|524288 ( # B0 H80000) |使用者或群組有權修改物件的擁有者。|  
|**adRightWritePermissions**|262144 ( # B0 H40000) |使用者或群組可以修改目錄中物件的特定許可權。|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)  
    :::column-end:::
    :::column:::
        [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)  
    :::column-end:::
:::row-end:::
