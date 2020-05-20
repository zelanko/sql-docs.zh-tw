---
title: CancelUpdate 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: d62837bd06798fd8ce7b51b0345cf5e5a6463e4b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763159"
---
# <a name="cancelupdate-method-ado"></a>CancelUpdate 方法 (ADO)
在呼叫[Update](../../../ado/reference/ado-api/update-method.md)方法之前，取消對[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的目前或新資料列或[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合所做的任何變更。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>備註  
  
## <a name="recordset"></a>資料錄集  
 使用**CancelUpdate**方法可取消對目前資料列所做的任何變更，或捨棄新加入的資料列。 您無法在呼叫**Update**方法之後取消對目前資料列或新資料列的變更，除非變更是您可以使用[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法復原的交易之一部分，或是批次更新的一部分。 在批次更新的情況下，您可以使用**CancelUpdate**或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法來取消**更新**。  
  
 當您呼叫**CancelUpdate**方法時，如果要加入新的資料列，目前的資料列會成為[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)呼叫之前的目前資料列。  
  
 如果您處於編輯模式，而且想要移出目前的記錄（例如，藉由使用[move](../../../ado/reference/ado-api/move-method-ado.md)、 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)或[Close](../../../ado/reference/ado-api/close-method-ado.md)方法），您可以使用**CancelUpdate**來取消任何暫止的變更。 如果更新無法成功張貼到資料來源，您可能需要執行此動作。 例如，因為參考完整性違規而失敗的嘗試刪除，會在呼叫[delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)之後讓**記錄集**處於編輯模式。  
  
## <a name="record"></a>Record  
 **CancelUpdate**方法會取消任何暫止的[欄位](../../../ado/reference/ado-api/field-object.md)物件插入或刪除動作，並取消現有欄位的暫止更新，並將它們還原成其原始值。 **Fields**集合中所有欄位的[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性會設定為**adFieldOK**。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Update 和 CancelUpdate 方法範例（VB）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update 和 CancelUpdate 方法範例（VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法（ADO）](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel 方法（ADO）](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法（RDS）](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 方法（ADO）](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法（RDS）](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [EditMode 屬性](../../../ado/reference/ado-api/editmode-property.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
