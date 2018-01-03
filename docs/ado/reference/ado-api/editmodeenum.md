---
title: "EditModeEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: EditModeEnum
helpviewer_keywords: EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d5f1463191ced2f9e4768193ae5c79c5619896a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="editmodeenum"></a>EditModeEnum
指定記錄的編輯狀態。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|表示未編輯的作業正在進行中。|  
|**adEditInProgress**|@shouldalert|指出目前記錄中的資料已修改但尚未儲存。|  
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
