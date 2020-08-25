---
description: CursorLocation 屬性 (ADO)
title: " (ADO) 的 CursorLocation 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
author: rothja
ms.author: jroth
ms.openlocfilehash: 6bb1c7932047e72d586275a4b56d1424539477f4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775587"
---
# <a name="cursorlocation-property-ado"></a>CursorLocation 屬性 (ADO)
表示資料指標服務的位置。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回可設定為其中一個[CursorLocationEnum](./cursorlocationenum.md)值的**Long**值。  
  
## <a name="remarks"></a>備註  
 這個屬性可讓您選擇可供提供者存取的各種資料指標程式庫。 通常，您可以選擇使用用戶端資料指標程式庫或位於伺服器上的資料指標程式庫。  
  
 此屬性設定只會影響在設定屬性之後所建立的連接。 變更 **CursorLocation** 屬性不會影響現有的連接。  
  
 [Execute](./execute-method-ado-connection.md)方法所傳回的資料指標會繼承此設定。 **記錄集** 物件會自動從其相關聯的連接繼承此設定。  
  
 這個屬性是在 [連接](./connection-object-ado.md) 或已關閉的 [記錄集](./recordset-object-ado.md)上的讀取/寫入，而且在開啟的 **記錄集**上是唯讀的。  
  
> [!NOTE]
>  **遠端資料服務使用量** 當用於用戶端 **記錄集** 或 **連接** 物件時， **CursorLocation** 屬性只能設定為 **adUseClient**。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Connection 物件 (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset 物件 (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [附錄 A：提供者](../../guide/appendixes/appendix-a-providers.md)