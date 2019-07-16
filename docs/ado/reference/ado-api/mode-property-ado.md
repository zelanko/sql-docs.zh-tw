---
title: Mode 屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc5b2e2bce410309656bad5591a3df90781cc8bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932221"
---
# <a name="mode-property-ado"></a>Mode 屬性 (ADO)
表示在修改資料的可用權限[連接](../../../ado/reference/ado-api/connection-object-ado.md)，[記錄](../../../ado/reference/ado-api/record-object-ado.md)，或[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值。 預設值**連接**是**adModeUnknown**。 預設值**記錄**物件**adModeRead**。 預設值**Stream**為基礎的來源相關聯 (使用 URL 做為來源，或做為預設開啟**Stream**的**記錄**) 是**adModeRead**。 預設值**Stream**與基礎無關 （在記憶體中具現化） 的來源是**adModeUnknown**。  
  
## <a name="remarks"></a>備註  
 使用 **模式**屬性來設定，或在目前的連線提供者所傳回的存取權限使用中。 您可以設定**模式**屬性時，才**連線**物件已關閉。  
  
 針對**Stream**物件，如果未指定的存取模式，它繼承自來源用來開啟**Stream**物件。 例如，如果**Stream**從開啟**記錄**物件，即可為相同的模式中開啟的預設**記錄**。  
  
 雖然物件已關閉，且為唯讀狀態開啟物件時，這個屬性是讀取/寫入。  
  
> [!NOTE]
>  **遠端資料服務使用量**用戶端上使用時**連接**物件**模式**屬性只能設定為**adModeUnknown**。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [IsolationLevel 和 Mode 屬性範例 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 和 Mode 屬性範例 （VC + +）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
