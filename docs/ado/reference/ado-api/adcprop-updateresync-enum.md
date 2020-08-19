---
description: ADCPROP_UPDATERESYNC_ENUM
title: ADCPROP_UPDATERESYNC_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
author: rothja
ms.author: jroth
ms.openlocfilehash: 81d1ff4bf67f103b613cb925a590b4d00e54482a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451590"
---
# <a name="adcprop_updateresync_enum"></a>ADCPROP_UPDATERESYNC_ENUM
指定 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 方法是否接著隱含的 [Resync](../../../ado/reference/ado-api/resync-method.md) 方法作業，如果是，該作業的範圍。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|使用所有其他 ADCPROP_UPDATERESYNC_ENUM 成員的合併值叫用重新 **同步** 。|  
|**adResyncAutoIncrement**|1|預設值。 嘗試針對資料來源自動遞增或產生的資料行（例如 Microsoft Jet 自動編號欄位或 Microsoft SQL Server 識別欄位），取得新的識別值。|  
|**adResyncConflicts**|2|針對因為並行衝突而導致 update 或 delete 作業失敗的所有資料列叫用重新 **同步** 。|  
|**adResyncInserts**|8|針對所有已成功插入的資料列叫用重新 **同步** 。 不過，自動遞增資料行值不會重新同步處理。 相反地，新插入之資料列的內容會根據現有的主鍵值重新同步處理。 如果主鍵是自動遞增值，[重新 **同步** 處理] 將不會取出預期資料列的內容。 如果是自動遞增的自動遞增主鍵值，請使用**adResyncAutoIncrement**adResyncInserts 的組合值來呼叫**UpdateBatch**  +  ** **。|  
|**adResyncNone**|0|不會叫用重新 **同步**。|  
|**adResyncUpdates**|4|針對所有已成功更新的資料列叫用重新 **同步** 。|  
  
## <a name="applies-to"></a>套用至  
 [更新重新同步動態屬性 (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
