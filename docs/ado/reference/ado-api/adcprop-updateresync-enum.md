---
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ef67068f1c2451fa5f8e2d314ae49f08f7be181
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
指定是否[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法後面的隱含[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法作業而且如果是，該作業的範圍。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|叫用**重新同步處理**結合其他 ADCPROP_UPDATERESYNC_ENUM 成員的值。|  
|**adResyncAutoIncrement**|1|預設值。 嘗試擷取自動遞增或是資料來源，例如 Microsoft Jet 自動編號欄位或 Microsoft SQL Server Identity 資料行所產生的資料行的新識別值。|  
|**adResyncConflicts**|2|叫用**重新同步處理**的所有資料列中更新或刪除作業失敗，因為發生並行衝突。|  
|**adResyncInserts**|8|叫用**重新同步處理**所有成功插入資料列。 不過，不會重新同步 AutoIncrement 資料行值。 相反地，新插入的資料列的內容會重新同步化依據現有主索引鍵值。 主索引鍵是否為自動遞增的值，**重新同步處理**將不會擷取預期的資料列的內容。 若為自動遞增自動遞增主索引鍵值，呼叫**UpdateBatch**結合值**adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|不會呼叫**重新同步處理**。|  
|**adResyncUpdates**|4|叫用**重新同步處理**所有已成功更新資料列。|  
  
## <a name="applies-to"></a>適用於  
 [更新重新同步動態屬性 (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
