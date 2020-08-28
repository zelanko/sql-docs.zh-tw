---
description: ActualSize 屬性 (ADO)
title: " (ADO) 的 ActualSize 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 6684c03c94d26b8c8f6366ac41ccd1b331016426
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976899"
---
# <a name="actualsize-property-ado"></a>ActualSize 屬性 (ADO)
表示欄位值的實際長度（以位元組為單位）。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 傳回 **Long** 值。  
  
## <a name="remarks"></a>備註  
 您可以使用 **ActualSize** 屬性來傳回 [欄位](./field-object.md) 物件值的實際長度。 針對所有欄位， **ActualSize** 屬性是唯讀的。 如果 ADO 無法判斷 **欄位** 物件值的長度， **ActualSize** 屬性會傳回 **adUnknown**。  
  
 **ActualSize**和[DefinedSize](./definedsize-property.md)屬性是不同的，如下列範例所示。 宣告類型為**adVarChar**且最大長度為50個字元的**欄位**物件會傳回**DefinedSize**屬性值50，但它所傳回的**ActualSize**屬性值是儲存在目前記錄之欄位中的資料長度。 **DefinedSize**大於255個位元組的**欄位**會被視為可變長度資料行。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](./field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActualSize 和 DefinedSize 屬性範例 (VB) ](./actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 屬性範例 (VC + +) ](./actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 屬性](./definedsize-property.md)