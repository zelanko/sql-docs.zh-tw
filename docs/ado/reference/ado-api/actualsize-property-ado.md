---
title: ActualSize 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
author: rothja
ms.author: jroth
ms.openlocfilehash: fd8288fa9f39593cb1f5fb91818925d36d731b9f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760674"
---
# <a name="actualsize-property-ado"></a>ActualSize 屬性 (ADO)
表示域值的實際長度（以位元組為單位）。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 傳回**Long**值。  
  
## <a name="remarks"></a>備註  
 使用**ActualSize**屬性可傳回[欄位](../../../ado/reference/ado-api/field-object.md)物件值的實際長度。 對於所有欄位而言， **ActualSize**屬性都是唯讀的。 如果 ADO 無法判斷**欄位**物件值的長度， **ActualSize**屬性會傳回**adUnknown**。  
  
 **ActualSize**和[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)屬性不同，如下列範例所示。 已宣告類型為**adVarChar**且最大長度為50個字元的**欄位**物件會傳回**DefinedSize**屬性值50，但它所傳回的**ActualSize**屬性值是儲存在目前記錄之欄位中的資料長度。 **DefinedSize**大於255個位元組的**欄位**會被視為可變長度的資料行。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActualSize 和 DefinedSize 屬性範例（VB）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 屬性範例（VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 屬性](../../../ado/reference/ado-api/definedsize-property.md)
