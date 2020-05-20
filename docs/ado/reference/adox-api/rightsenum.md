---
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
ms.openlocfilehash: 343d5ec73a9720085f450cde3f35a187cf4b7302
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762809"
---
# <a name="rightsenum"></a>RightsEnum
指定物件上群組或使用者的許可權。  
  
|持續性|值|說明|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384（&H4000）|使用者或群組有權建立此類型的新物件。|  
|**adRightDelete**|65536（&H 10000）|使用者或群組具有從物件刪除資料的許可權。 對於**資料表**之類的物件，使用者有權從記錄中刪除資料值。|  
|**adRightDrop**|256（&H100）|使用者或群組具有從目錄中移除物件的許可權。 例如，**資料表**可以由 DROP TABLE SQL 命令刪除。|  
|**adRightExclusive**|512（&H200）|使用者或群組具有以獨佔方式存取物件的許可權。|  
|**adRightExecute**|536870912（&H20000000）|使用者或群組具有執行物件的許可權。|  
|**adRightFull**|268435456（&H10000000）|使用者或群組具有物件的擁有權限。|  
|**adRightInsert**|32768（&H8000）|使用者或群組具有插入物件的許可權。 對於**資料表**之類的物件，使用者具有將資料插入資料表的許可權。|  
|**adRightMaximumAllowed**|33554432（&H2000000）|使用者或群組具有提供者所允許的最大許可權數目。 特定的許可權與提供者相關。|  
|**adRightNone**|0|使用者或群組沒有物件的許可權。|  
|**adRightRead**|-2147483648 (&H80000000)|使用者或群組具有讀取物件的許可權。 對於[資料表](../../../ado/reference/adox-api/table-object-adox.md)之類的物件，使用者有權讀取資料表中的資料。|  
|**adRightReadDesign**|1024（&H400）|使用者或群組具有讀取物件設計的許可權。|  
|**adRightReadPermissions**|131072（&H20000）|使用者或群組可以查看（但不能變更）目錄中物件的特定許可權。|  
|**adRightReference**|8192（&H2000）|使用者或群組具有參考物件的許可權。|  
|**adRightUpdate**|1073741824（&H40000000）|使用者或群組具有更新物件的許可權。 對於**資料表**之類的物件，使用者有權更新資料表中的資料。|  
|**adRightWithGrant**|4096（&H1000）|使用者或群組具有授與物件使用權限的許可權。|  
|**adRightWriteDesign**|2048（&H800）|使用者或群組具有修改物件設計的許可權。|  
|**adRightWriteOwner**|524288（&H80000）|使用者或群組有權修改物件的擁有者。|  
|**adRightWritePermissions**|262144（&H40000）|使用者或群組可以修改目錄中物件的特定許可權。|  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
