---
title: "EditModeEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b59850d8b04854ee74f94664b53dc22242c6913
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="editmodeenum"></a>EditModeEnum
指定記錄的編輯狀態。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|表示未編輯的作業正在進行中。|  
|**adEditInProgress**|1|指出目前記錄中的資料已修改但尚未儲存。|  
|**adEditAdd**|2|表示[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)已呼叫方法，並複製緩衝區中目前的記錄是尚未儲存在資料庫中的新記錄。|  
|**adEditDelete**|4|指出目前的記錄已被刪除。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>適用於  
 [EditMode 屬性](../../../ado/reference/ado-api/editmode-property.md)
