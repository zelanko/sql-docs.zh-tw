---
title: "NumericScale 屬性 (ADOX) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5f943223be304de56e52f54510bd6d27bac6d15
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="numericscale-property-adox"></a>NumericScale 屬性 (ADOX)
指出資料行中的數字值的小數位數。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定並傳回**位元組**小數位數的資料行中的資料值的值時[類型](../../../ado/reference/adox-api/type-property-column-adox.md)屬性是**adNumeric**或**adDecimal**。 **NumericScale**會忽略所有其他資料類型。  
  
## <a name="remarks"></a>備註  
 預設值為零 (0)。  
  
 **NumericScale**是唯讀的[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件已經附加至集合。  
  
## <a name="applies-to"></a>適用於  
 [資料行物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADOX 程式碼範例： NumericScale 和有效位數屬性範例 (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [型別屬性 （資料行） (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
