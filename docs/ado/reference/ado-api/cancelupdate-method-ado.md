---
title: "CancelUpdate 方法 (ADO) |Microsoft 文件"
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
f1_keywords: Recordset15::CancelUpdate
helpviewer_keywords: CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7a118a37c403d9d50019e72b10f482d7b3f089c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="cancelupdate-method-ado"></a>CancelUpdate 方法 (ADO)
取消目前的或新的資料列的任何變更[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，然後再呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>備註  
  
## <a name="recordset"></a>資料錄集  
 使用**CancelUpdate**方法來取消目前的資料列所做的變更或捨棄新加入的資料列。 您無法取消目前的資料列或新的資料列的變更之後您呼叫,**更新**方法，除非所做的變更可以回復與交易的一部分，否則[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法或組件批次更新。 在批次更新，您可以取消**更新**與**CancelUpdate**或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果您要加入新的資料列，當您呼叫**CancelUpdate**方法中，目前的資料列變成資料列之前的目前[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)呼叫。  
  
 如果您在編輯模式，並想要移出目前的記錄 (例如，藉由使用[移動](../../../ado/reference/ado-api/move-method-ado.md)， [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)，或[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法)，您可以使用**CancelUpdate**取消任何暫止的變更。 若要這樣做，如果更新不能已成功地公佈到資料來源。 例如，嘗試刪除失敗，因為參考完整性違規會離開**資料錄集**處於編輯模式下呼叫後[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)。  
  
## <a name="record"></a>記錄  
 **CancelUpdate**方法會取消任何暫止的插入或刪除[欄位](../../../ado/reference/ado-api/field-object.md)物件，並取消擱置中的現有欄位的更新並還原至其原始值。 [狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性中的所有欄位**欄位**集合設定為**adFieldOK**。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [更新和 CancelUpdate 方法範例 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [更新和 CancelUpdate 方法範例 （VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel 方法 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [EditMode 屬性](../../../ado/reference/ado-api/editmode-property.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
