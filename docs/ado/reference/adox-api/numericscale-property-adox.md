---
title: NumericScale 屬性 (ADOX) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 227abf011a72d18210424def292cc9a620033356
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="numericscale-property-adox"></a>NumericScale 屬性 (ADOX)
指出資料行中的數字值的小數位數。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定並傳回**位元組**小數位數的資料行中的資料值的值時[類型](../../../ado/reference/adox-api/type-property-column-adox.md)屬性是**adNumeric**或**adDecimal**。 **NumericScale**會忽略所有其他資料類型。  
  
## <a name="remarks"></a>備註  
 預設值為零 (0)。  
  
 **NumericScale**是唯讀的[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件已經附加至集合。  
  
## <a name="applies-to"></a>適用於  
 [Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADOX 程式碼範例： NumericScale 和有效位數屬性範例 (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type 屬性 (Column) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
