---
title: Mode 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
author: rothja
ms.author: jroth
ms.openlocfilehash: 1bdd16d8e98bd1c038c5bc6c761305e87b65b765
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762509"
---
# <a name="mode-property-ado"></a>Mode 屬性 (ADO)
表示在[連接](../../../ado/reference/ado-api/connection-object-ado.md)、[記錄](../../../ado/reference/ado-api/record-object-ado.md)或[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件中修改資料的可用許可權。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值。 **連接**的預設值是**adModeUnknown**。 **Record**物件的預設值為**adModeRead**。 與基礎來源相關聯之**資料流程**的預設值（以 URL 作為來源開啟，或做為**記錄**的預設**資料流程**）是**adModeRead**。 未與基礎來源（在記憶體中具現化）相關聯之**資料流程**的預設值是**adModeUnknown**。  
  
## <a name="remarks"></a>備註  
 使用**Mode**屬性來設定或傳回目前連接上提供者所使用的存取權限。 只有當**連接**物件已關閉時，您才可以設定**Mode**屬性。  
  
 針對**資料流程**物件，如果未指定存取模式，則會繼承自用來開啟**資料流程**物件的來源。 例如，如果從**記錄**物件開啟**資料流程**，預設會在與**記錄**相同的模式中開啟。  
  
 當物件已關閉時，這個屬性會是讀取/寫入，而當物件開啟時，則是唯讀的。  
  
> [!NOTE]
>  **遠端資料服務使用量**在用戶端**連接**物件上使用時， **Mode**屬性只能設定為**adModeUnknown**。  
  
## <a name="applies-to"></a>套用至  
  
||||  
|-|-|-|  
|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [IsolationLevel 和 Mode 屬性範例（VB）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 和 Mode 屬性範例（VC + +）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
