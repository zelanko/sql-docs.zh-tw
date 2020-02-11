---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a8c4ddb27bbc6831095062af5491fb501b6d5b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933041"
---
# <a name="editmodeenum"></a>EditModeEnum
指定記錄的編輯狀態。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|表示沒有正在進行的編輯作業。|  
|**adEditInProgress**|1|指出目前記錄中的資料已修改但未儲存。|  
|**adEditAdd**|2|表示已呼叫[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法，而且複製緩衝區中的目前記錄是尚未儲存在資料庫中的新記錄。|  
|**adEditDelete**|4|指出目前的記錄已刪除。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>套用至  
 [EditMode 屬性](../../../ado/reference/ado-api/editmode-property.md)
