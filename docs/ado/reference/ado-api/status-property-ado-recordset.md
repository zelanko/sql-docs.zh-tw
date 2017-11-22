---
title: "Status 屬性 （ADO 資料錄集） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords: Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0005de0669a2dd68622c2e81c9f7b3be2f912da1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="status-property-ado-recordset"></a>Status 屬性 （ADO 資料錄集）
表示相對於批次更新為目前的記錄或其他的大量作業的狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回一或多個總和[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)值。  
  
## <a name="remarks"></a>備註  
 使用**狀態**屬性來查看哪些變更被暫止的批次更新期間修改的記錄。 您也可以使用**狀態**屬性可檢視的大量作業，例如當您呼叫期間失敗的記錄狀態[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或設定[篩選](../../../ado/reference/ado-api/filter-property.md)屬性**資料錄集**物件陣列的書籤。 這個屬性，您可以決定如何指定的記錄資料失敗並解決它。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>請參閱＜  
 [狀態屬性範例 （資料錄集） (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Status 屬性範例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
