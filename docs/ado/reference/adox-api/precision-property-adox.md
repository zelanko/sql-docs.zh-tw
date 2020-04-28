---
title: Precision 屬性（ADOX） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d1416842f3c122e9e5e5e28b8a14310b679697cd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965566"
---
# <a name="precision-property-adox"></a>Precision 屬性 (ADOX)
指出資料[行](../../../ado/reference/adox-api/column-object-adox.md)中資料值的最大有效位數。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 當[Type](../../../ado/reference/adox-api/type-property-column-adox.md)屬性為數數值型別時，設定並傳回**Long**值，這是資料行中資料值的最大有效位數。 所有其他資料類型都會忽略有效**位數**。  
  
## <a name="remarks"></a>備註  
 預設值為零 (**0**)。  
  
 對於已經附加至集合的資料[行](../../../ado/reference/adox-api/column-object-adox.md)物件而言，這個屬性是唯讀的。  
  
## <a name="applies-to"></a>套用至  
 [Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADOX 程式碼範例： NumericScale 和 Precision 屬性範例（VB）](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type 屬性（Column）（ADOX）](../../../ado/reference/adox-api/type-property-column-adox.md)   
 [Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
