---
title: EditModeEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3702e111333194804f3c0bd7335e4403f4bfddd0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="editmodeenum"></a>EditModeEnum
指定記錄的編輯狀態。  
  
|常數|Value|Description|  
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
