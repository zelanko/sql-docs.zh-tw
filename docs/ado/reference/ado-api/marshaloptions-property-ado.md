---
title: MarshalOptions 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: rothja
ms.author: jroth
ms.openlocfilehash: 182946d30141ecbbcc2cba706338609b431abb97
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754498"
---
# <a name="marshaloptions-property-ado"></a>MarshalOptions 屬性 (ADO)
指出[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的哪些記錄要封送處理回伺服器。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)值。 預設值為**adMarshalAll**。  
  
## <a name="remarks"></a>備註  
 使用用戶端[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)時，已在用戶端上修改的記錄會透過稱為封送處理的技術寫回仲介層或 Web 服務器，這是跨執行緒或進程界限封裝和傳送介面方法參數的程式。 設定**MarshalOptions**屬性可改善修改的遠端資料被封送處理，以更新至仲介層或 Web 服務器的效能。  
  
> [!NOTE]
>  **遠端資料服務使用量**此屬性僅用於用戶端**記錄集**。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [MarshalOptions 屬性範例（VB）](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [MarshalOptions 屬性範例 (VC++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   
