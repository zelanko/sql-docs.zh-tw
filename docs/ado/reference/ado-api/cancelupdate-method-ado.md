---
description: CancelUpdate 方法 (ADO)
title: " (ADO) 的 CancelUpdate 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
author: rothja
ms.author: jroth
ms.openlocfilehash: 2355d2a0b2ff0bbe14eb9b7d2a9a373164a4f5e5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975559"
---
# <a name="cancelupdate-method-ado"></a>CancelUpdate 方法 (ADO)
在呼叫[Update](./update-method.md)方法之前，取消對[記錄集](./recordset-object-ado.md)物件的目前或新資料列所做的任何變更，或[記錄](./record-object-ado.md)物件的[Fields](./fields-collection-ado.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>備註  
  
## <a name="recordset"></a>資料錄集  
 您可以使用 **CancelUpdate** 方法來取消對目前資料列所做的任何變更，或是捨棄新加入的資料列。 您無法在呼叫 **Update** 方法之後取消目前資料列或新資料列的變更，除非這些變更都是您可以使用 [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 方法復原的交易一部分，或是批次更新的一部分。 在批次更新的案例中，您可以使用**CancelUpdate**或[CancelBatch](./cancelbatch-method-ado.md)方法來取消**更新**。  
  
 如果您在呼叫 **CancelUpdate** 方法時加入新的資料列，目前的資料列會變成 [AddNew](./addnew-method-ado.md) 呼叫之前的資料列。  
  
 如果您在編輯模式中，而且想要移出目前的記錄 (例如，藉由使用 [move](./move-method-ado.md)、 [NextRecordset](./nextrecordset-method-ado.md)或 [Close](./close-method-ado.md) 方法) ，您可以使用 **CancelUpdate** 來取消任何暫止的變更。 如果更新無法成功張貼到資料來源，您可能需要這麼做。 例如，因為參考完整性違規而失敗的嘗試刪除，將會在呼叫[delete](./delete-method-ado-recordset.md)之後讓**記錄集**處於編輯模式。  
  
## <a name="record"></a>Record  
 **CancelUpdate**方法會取消任何暫止的[欄位](./field-object.md)物件插入或刪除，並取消現有欄位的暫止更新，並將其還原為其原始值。 [**欄位**] 集合中所有欄位的 [[狀態](./status-property-ado-recordset.md)] 屬性會設定為 [ **adFieldOK**]。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Fields 集合 (ADO)](./fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset 物件 (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [Update 和 CancelUpdate 方法範例 (VB) ](./update-and-cancelupdate-methods-example-vb.md)   
 [Update 和 CancelUpdate 方法範例 (VC + +) ](./update-and-cancelupdate-methods-example-vc.md)   
 [ (ADO) 的 AddNew 方法 ](./addnew-method-ado.md)   
 [ (ADO) 的 Cancel 方法 ](./cancel-method-ado.md)   
 [ (RDS) 的 Cancel 方法 ](../rds-api/cancel-method-rds.md)   
 [ (ADO) 的 CancelBatch 方法 ](./cancelbatch-method-ado.md)   
 [RDS)  (CancelUpdate 方法 ](../rds-api/cancelupdate-method-rds.md)   
 [EditMode 屬性](./editmode-property.md)   
 [Update 方法](./update-method.md)