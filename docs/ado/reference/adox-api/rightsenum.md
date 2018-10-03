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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1904a77ae104576f2a9f82fc09d8728e2ec88c11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47760506"
---
# <a name="rightsenum"></a>RightsEnum
指定物件的權限或群組或使用者的權限。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 （& H4000）|使用者或群組已建立此型別的新物件的權限。|  
|**adRightDelete**|65536 (&AMP; H 10000)|使用者或群組已刪除的資料，從物件的權限。 物件，例如**資料表**，使用者有權從記錄中刪除資料值。|  
|**adRightDrop**|256 （& H100）|使用者或群組已從目錄移除物件的權限。 例如，**資料表**卸除資料表 SQL 命令來刪除。|  
|**adRightExclusive**|512 （& H200）|使用者或群組已經以獨佔方式存取物件的權限。|  
|**adRightExecute**|536870912 （& H20000000）|使用者或群組擁有執行物件的權限。|  
|**adRightFull**|268435456 （& H10000000）|使用者或群組對物件的所有權限。|  
|**adRightInsert**|32768 （& H8000）|使用者或群組已插入之物件的權限。 物件，例如**資料表**，使用者具有將資料插入資料表的權限。|  
|**adRightMaximumAllowed**|33554432 (&AMP; H 2000000)|使用者或群組具有權限提供者所允許的最大數目。 特定權限會提供者而不同。|  
|**adRightNone**|0|使用者或群組擁有物件的權限。|  
|**adRightRead**|-2147483648 (&H80000000)|使用者或群組具有權限來讀取物件。 物件，例如[資料表](../../../ado/reference/adox-api/table-object-adox.md)，使用者有權讀取資料表中的資料。|  
|**adRightReadDesign**|1024 (&AMP; H400)|使用者或群組具有讀取物件設計的權限。|  
|**adRightReadPermissions**|131072 （& H20000）|使用者或群組可以檢視，但不是變更，請在目錄中物件的特定權限。|  
|**adRightReference**|8192 (&AMP; H2000)|使用者或群組具有參考物件的權限。|  
|**adRightUpdate**|1073741824 （& H40000000）|使用者或群組已更新之物件的權限。 物件，例如**資料表**，使用者已更新資料表中的資料的權限。|  
|**adRightWithGrant**|4096 (&AMP; H1000)|使用者或群組具有權限授與權限的物件。|  
|**adRightWriteDesign**|2048 (&AMP; H800)|使用者或群組有權修改物件的設計。|  
|**adRightWriteOwner**|524288 （& H80000）|使用者或群組已修改物件的擁有者的權限。|  
|**adRightWritePermissions**|262144 （& H40000）|使用者或群組可以修改的物件在目錄中的特定權限。|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
