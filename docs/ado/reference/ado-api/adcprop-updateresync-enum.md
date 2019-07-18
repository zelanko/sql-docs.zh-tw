---
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 82a5473a68303d429794d8b98c4e91293e4e30cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921408"
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
指定是否[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法後面隱含[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法作業，如果是的話，該作業的範圍。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|叫用**Resync**結合其他 ADCPROP_UPDATERESYNC_ENUM 成員的值。|  
|**adResyncAutoIncrement**|1|預設值。 嘗試擷取新的識別值，自動遞增或產生的資料來源，例如 Microsoft Jet 自動編號欄位或 Microsoft SQL Server Identity 資料行的資料行。|  
|**adResyncConflicts**|2|叫用**Resync**中更新或刪除作業失敗，因為並行衝突發生的所有資料列。|  
|**adResyncInserts**|8|叫用**Resync**的所有成功插入的資料列。 不過，自動遞增資料行值都不會重新同步。 相反地，新插入的資料列的內容會重新同步處理根據現有的主索引鍵值。 主索引鍵是自動遞增的值，如果**Resync**不會擷取預期的資料列的內容。 自動遞增自動遞增主索引鍵值，呼叫**UpdateBatch**結合值**adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|不會呼叫**Resync**。|  
|**adResyncUpdates**|4|叫用**Resync**所有已成功更新的資料列。|  
  
## <a name="applies-to"></a>適用於  
 [更新重新同步動態屬性 (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
