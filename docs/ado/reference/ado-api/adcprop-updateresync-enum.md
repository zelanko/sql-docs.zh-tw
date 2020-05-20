---
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
ms.openlocfilehash: d27169aa9da35f84a1d91985f7f2d1a41035a100
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760704"
---
# <a name="adcprop_updateresync_enum"></a>ADCPROP_UPDATERESYNC_ENUM
指定[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法後面是否接著隱含的重新[同步](../../../ado/reference/ado-api/resync-method.md)處理方法作業，如果是，則為該作業的範圍。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|使用所有其他 ADCPROP_UPDATERESYNC_ENUM 成員的加總值來叫用重新**同步**。|  
|**adResyncAutoIncrement**|1|預設值。 嘗試為數據源自動遞增或產生的資料行（例如 Microsoft Jet 自動編號欄位或 Microsoft SQL Server 識別欄位），抓取新的識別值。|  
|**adResyncConflicts**|2|針對因為並行衝突而導致更新或刪除作業失敗的所有資料列，叫用重新**同步**。|  
|**adResyncInserts**|8|針對所有成功插入的資料列叫用重新**同步**。 不過，自動遞增資料行值不會重新同步處理。 相反地，新插入之資料列的內容會根據現有的主要金鑰值重新同步處理。 如果主鍵是自動遞增的值，則**Resync**不會抓取所需資料列的內容。 若為自動累加自動遞增主鍵值， **UpdateBatch**請使用結合值**adResyncAutoIncrement**  +  **adResyncInserts**來呼叫 UpdateBatch。|  
|**adResyncNone**|0|不會叫用重新**同步**。|  
|**adResyncUpdates**|4|針對所有已成功更新的資料列叫用重新**同步**。|  
  
## <a name="applies-to"></a>套用至  
 [更新重新同步動態屬性 (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
