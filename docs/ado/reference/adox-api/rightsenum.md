---
title: RightsEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32cd777bad44e0784943aab1c0a4c9ba665f7247
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286848"
---
# <a name="rightsenum"></a>RightsEnum
在物件上指定的權限或群組或使用者權限。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 (&AMP; H4000)|使用者或群組擁有權限建立此類型的新物件。|  
|**adRightDelete**|65536 (&AMP; H10000)|使用者或群組已刪除的資料從物件的權限。 物件，例如**資料表**，使用者有權從記錄中刪除資料值。|  
|**adRightDrop**|256 (&AMP; H100)|使用者或群組已從目錄移除物件的權限。 例如，**資料表**卸除資料表 SQL 命令，可以刪除。|  
|**adRightExclusive**|512 (&AMP; H200)|使用者或群組已經以獨佔方式存取物件的權限。|  
|**adRightExecute**|536870912 (&AMP; H20000000)|使用者或群組擁有執行物件的權限。|  
|**adRightFull**|268435456 (&AMP; H10000000)|使用者或群組對物件的所有權限。|  
|**adRightInsert**|32768 (&AMP; H8000)|使用者或群組已插入之物件的權限。 物件，例如**資料表**，使用者具有將資料插入資料表的權限。|  
|**adRightMaximumAllowed**|33554432 (&AMP; H 2000000)|使用者或群組擁有權限的提供者所允許的最大數目。 特定的權限是提供者而定。|  
|**adRightNone**|0|使用者或群組擁有物件的權限。|  
|**adRightRead**|-2147483648 (&H80000000)|使用者或群組具有讀取該物件的權限。 物件，例如[資料表](../../../ado/reference/adox-api/table-object-adox.md)，使用者有權讀取資料表中的資料。|  
|**adRightReadDesign**|1024 (&AMP; H400)|使用者或群組擁有權限讀取物件的設計。|  
|**adRightReadPermissions**|131072 (&AMP; H20000)|使用者或群組可以檢視，但不是變更類別目錄中之物件的特定權限。|  
|**adRightReference**|8192 (&AMP; H2000)|使用者或群組擁有權限參考的物件。|  
|**adRightUpdate**|1073741824 (&AMP; H40000000)|使用者或群組已更新物件的權限。 物件，例如**資料表**，使用者已更新資料表中的資料的權限。|  
|**adRightWithGrant**|4096 (&AMP; H1000)|使用者或群組擁有權限授與權限的物件。|  
|**adRightWriteDesign**|2048 (&AMP; H800)|使用者或群組擁有權限修改物件的設計。|  
|**adRightWriteOwner**|524288 (&AMP; H80000)|使用者或群組已修改的物件擁有者的權限。|  
|**adRightWritePermissions**|262144 (&AMP; H40000)|使用者或群組可以修改物件的類別目錄中的特定權限。|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
