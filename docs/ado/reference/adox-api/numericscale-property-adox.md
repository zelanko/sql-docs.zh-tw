---
description: NumericScale 屬性 (ADOX)
title: NumericScale 屬性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 161b6049ca5392eafacaf0fd97db653070f105e0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983889"
---
# <a name="numericscale-property-adox"></a>NumericScale 屬性 (ADOX)
表示資料行中數值的小數位數。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 當[Type](./type-property-column-adox.md)屬性為**adNumeric**或**adDecimal**時，設定並傳回**位元組**值，這是資料行中資料值的小數位數。 所有其他資料類型都會忽略**NumericScale** 。  
  
## <a name="remarks"></a>備註  
 預設值為零 (0)。  
  
 針對已附加至集合的資料[行](./column-object-adox.md)物件， **NumericScale**是唯讀的。  
  
## <a name="applies-to"></a>套用至  
 [Column 物件 (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADOX 程式碼範例： NumericScale 和 Precision 屬性範例 (VB) ](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type 屬性 (Column) (ADOX)](./type-property-column-adox.md)