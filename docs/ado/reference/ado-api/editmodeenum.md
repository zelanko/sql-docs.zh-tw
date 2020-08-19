---
description: EditModeEnum
title: EditModeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
author: rothja
ms.author: jroth
ms.openlocfilehash: 64310c3399d24d557fc0896587dad0dc4fde091b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444040"
---
# <a name="editmodeenum"></a>EditModeEnum
指定記錄的編輯狀態。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|指出沒有進行中的編輯作業。|  
|**adEditInProgress**|1|指出目前記錄中的資料已修改但未儲存。|  
|**adEditAdd**|2|指出已呼叫 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 方法，而複製緩衝區中的目前記錄是尚未儲存在資料庫中的新記錄。|  
|**adEditDelete**|4|表示已刪除目前的記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>套用至  
 [EditMode 屬性](../../../ado/reference/ado-api/editmode-property.md)
