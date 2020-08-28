---
description: FormattedValue 屬性 (ADO MD)
title: FormattedValue 屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::FormattedValue
- FormattedValue
helpviewer_keywords:
- FormattedValue property [ADO MD]
ms.assetid: 5c06451e-06ec-4da6-9a87-2d043469248a
author: rothja
ms.author: jroth
ms.openlocfilehash: 5905b4aba040505c60fa78721718b3ab03c51622
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986699"
---
# <a name="formattedvalue-property-ado-md"></a>FormattedValue 屬性 (ADO MD)
表示資料 [格](./cell-object-ado-md.md) 值的格式化顯示。  
  
## <a name="return-values"></a>傳回值  
 傳回 **字串** ，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 您可以使用**FormattedValue**屬性來取得[Cell](./cell-object-ado-md.md)物件之[value](./value-property-ado-md.md)屬性的格式化顯示值。 例如，如果資料格的值是1056.87，而此值代表金額，則 **FormattedValue** 會是 $1056.87。  
  
## <a name="applies-to"></a>套用至  
 [Cell 物件 (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的集格範例 ](./cellset-example-vb.md)   
 [Value 屬性 (ADO MD)](./value-property-ado-md.md)