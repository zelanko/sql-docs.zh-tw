---
description: 判斷編輯模式
title: 判斷編輯模式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: rothja
ms.author: jroth
ms.openlocfilehash: ec235cfd012b79449fdebfab9c99399d967ca32f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991359"
---
# <a name="determining-edit-mode"></a>判斷編輯模式
ADO 會維護與目前記錄相關聯的編輯緩衝區。 **EditMode**屬性會指出是否已對此緩衝區進行變更，或是否已建立新的記錄。 使用 **EditMode** 來判斷目前記錄的編輯狀態。 如果編輯程式已中斷，並判斷您是否需要使用 **Update** 或 **CancelUpdate** 方法，您可以測試暫止的變更。  
  
 **EditMode** 會傳回下表所列的其中一個 **EditModeEnum** 常數。  
  
|持續性|描述|  
|--------------|-----------------|  
|**adEditNone**|指出沒有進行中的編輯作業。|  
|**adEditInProgress**|指出目前記錄中的資料已修改但未儲存。|  
|**adEditAdd**|指出已呼叫 **AddNew** 方法，而複製緩衝區中的目前記錄是尚未儲存至資料庫的新記錄。|  
|**adEditDelete**|表示已刪除目前的記錄。|  
  
 只有在目前有記錄時， **EditMode**才能傳回有效的值。 如果**BOF**或**EOF**為**True**或目前的記錄已刪除，則**EditMode**會傳回錯誤。
