---
title: LockType 屬性 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f98fea2139f64bffc214c392747a21bc41678de
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="locktype-property-ado"></a>LockType 屬性 (ADO)
表示在編輯期間鎖定記錄類型。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值。 預設值是**Recordset**。  
  
## <a name="remarks"></a>備註  
 設定**LockType**屬性之前開啟[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)指定開啟它時，應該使用何種類型的鎖定提供者。 讀取屬性的傳回類型的鎖定上開放使用**資料錄集**物件。  
  
 提供者可能不支援所有的鎖定類型。 如果提供者無法支援所要求**LockType**設定，它會取代另一種鎖定。 若要判斷中可用的實際鎖定功能**資料錄集**物件，請使用[支援](../../../ado/reference/ado-api/supports-method.md)方法**adUpdate**和**adUpdateBatch**.  
  
 **Locktype**如果，則不支援設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。 如果設定不支援的值，則不會產生錯誤。支援的最接近**LockType**將改為使用。  
  
 **LockType**屬性是讀取/寫入時**資料錄集**開啟時，已關閉，且為唯讀。  
  
> [!NOTE]
>  **遠端資料服務使用量**使用用戶端時**資料錄集**物件**LockType**屬性只能設定為**Adlockpessimistic**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CursorType、 LockType 和 EditMode 屬性範例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、 LockType 和 EditMode 屬性範例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
