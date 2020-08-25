---
description: Precision 屬性 (ADOX)
title: Precision 屬性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::put_Precision
- _Column::PutPrecision
- _Column::GetPrecision
- _Column::get_Precision
- _Column::Precision
helpviewer_keywords:
- Precision property [ADOX]
ms.assetid: 0e0ecbbf-d7de-49d4-a128-5a519ecd54ba
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e75cfa88eb66b88084a823d0558923210aed4db
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769778"
---
# <a name="precision-property-adox"></a>Precision 屬性 (ADOX)
表示資料 [行](./column-object-adox.md)中資料值的最大有效位數。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定和傳回 **Long** 值，當 [type](./type-property-column-adox.md) 屬性是數數值型別時，這是資料行中資料值的最大有效位數。 所有其他資料類型都會忽略有效**位數**。  
  
## <a name="remarks"></a>備註  
 預設值為零 (**0**)。  
  
 針對已附加至集合的資料 [行](./column-object-adox.md) 物件，這個屬性是唯讀的。  
  
## <a name="applies-to"></a>套用至  
 [Column 物件 (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADOX 程式碼範例： NumericScale 和 Precision 屬性範例 (VB) ](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [類型屬性 (資料行)  (ADOX) ](./type-property-column-adox.md)   
 [Column 物件 (ADOX)](./column-object-adox.md)