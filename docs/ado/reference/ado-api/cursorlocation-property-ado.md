---
title: CursorLocation 屬性（ADO） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afee71d4f37e2b3a27247fbeacf51dab66cc1e23
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933281"
---
# <a name="cursorlocation-property-ado"></a>CursorLocation 屬性 (ADO)
表示資料指標服務的位置。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回可設定為其中一個[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值的**Long**值。  
  
## <a name="remarks"></a>備註  
 這個屬性可讓您在提供者可存取的各種資料指標程式庫之間進行選擇。 通常，您可以選擇使用用戶端資料指標程式庫，或是位於伺服器上的其中一個。  
  
 此屬性設定會影響只有在設定屬性之後才建立的連接。 變更**CursorLocation**屬性不會影響現有的連接。  
  
 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法所傳回的資料指標會繼承此設定。 **記錄集**物件將會自動從其相關聯的連接繼承此設定。  
  
 這個屬性在[連接](../../../ado/reference/ado-api/connection-object-ado.md)或封閉式[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)上是讀取/寫入，而在開啟的**記錄集**上是唯讀的。  
  
> [!NOTE]
>  **遠端資料服務使用量**在用戶端**記錄集**或**連接**物件上使用時， **CursorLocation**屬性只能設定為**adUseClient**。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
