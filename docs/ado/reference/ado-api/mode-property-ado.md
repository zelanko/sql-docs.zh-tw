---
description: Mode 屬性 (ADO)
title: " (ADO) 的 Mode 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: eab9f3db1bfe9417411dc832cfa24e3d4496257b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990599"
---
# <a name="mode-property-ado"></a>Mode 屬性 (ADO)
指出可用來修改 [連接](./connection-object-ado.md)、 [記錄](./record-object-ado.md)或 [資料流程](./stream-object-ado.md) 物件中資料的許可權。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 [ConnectModeEnum](./connectmodeenum.md) 值。 **連接**的預設值為**adModeUnknown**。 **記錄**物件的預設值為**adModeRead**。 與基礎來源相關聯之**資料流程**的預設值 (以 URL 作為來源開啟，或做為**記錄**) 的預設**資料流程**的預設值為**adModeRead**。 未與基礎來源 (具現) 化之 **資料流程** 的預設值為 **adModeUnknown**。  
  
## <a name="remarks"></a>備註  
 使用 **Mode** 屬性來設定或傳回目前連接上提供者所使用的存取權限。 只有在**連接**物件關閉時，才可以設定**Mode**屬性。  
  
 若為 **資料流程** 物件，如果未指定存取模式，它會繼承自用來開啟 **資料流程** 物件的來源。 例如，如果 **資料流程** 是從 **記錄** 物件開啟，則預設會在與 **記錄**相同的模式中開啟。  
  
 這個屬性是讀取/寫入，而物件則是在物件開啟時關閉且為唯讀。  
  
> [!NOTE]
>  **遠端資料服務使用量** 使用於用戶端 **連接** 物件時， **Mode** 屬性只能設定為 **adModeUnknown**。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Connection 物件 (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Record 物件 (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Stream 物件 (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [IsolationLevel 和 Mode 屬性範例 (VB) ](./isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 和 Mode 屬性範例 (VC + +) ](./isolationlevel-and-mode-properties-example-vc.md)