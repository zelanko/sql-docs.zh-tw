---
title: NumericScale 屬性（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords:
- NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16fdefcb06d2b1b90dfc3da39aaf6b1c9659debc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965743"
---
# <a name="numericscale-property-adox"></a>NumericScale 屬性 (ADOX)
表示資料行中數值的小數位數。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 當[Type](../../../ado/reference/adox-api/type-property-column-adox.md)屬性為**adNumeric**或**adDecimal**時，設定並傳回**Byte**值，這是資料行中資料值的小數位數。 所有其他資料類型都會忽略**NumericScale** 。  
  
## <a name="remarks"></a>備註  
 預設值為零 (0)。  
  
 **NumericScale**已附加至集合的資料[行](../../../ado/reference/adox-api/column-object-adox.md)物件是唯讀的。  
  
## <a name="applies-to"></a>套用至  
 [Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADOX 程式碼範例： NumericScale 和 Precision 屬性範例（VB）](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type 屬性 (Column) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
