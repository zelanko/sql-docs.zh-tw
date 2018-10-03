---
title: CursorLocation 屬性 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3860434236f5a0751ddb857c6b8bce1cf54d19ac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718776"
---
# <a name="cursorlocation-property-ado"></a>CursorLocation 屬性 (ADO)
指出資料指標服務的位置。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**值，可以設定為其中一個[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值。  
  
## <a name="remarks"></a>備註  
 這個屬性可讓您選擇各種提供者可存取的資料指標程式庫。 通常，您可以選擇使用 伺服器上的 用戶端資料指標程式庫，或位於的其中一個。  
  
 此屬性設定會影響已經設定的屬性時，才建立連線。 變更**CursorLocation**屬性具有不會影響現有的連線。  
  
 所傳回的資料指標[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法繼承此設定。 **資料錄集**物件會自動繼承此設定及其相關聯的連接。  
  
 這個屬性是讀取/寫入上[連接](../../../ado/reference/ado-api/connection-object-ado.md)或 已關閉[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，和唯讀模式開啟時**資料錄集**。  
  
> [!NOTE]
>  **遠端資料服務使用量**用戶端上使用時**資料錄集**或**連線**物件**CursorLocation**屬性只可以設定為**adUseClient**。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
