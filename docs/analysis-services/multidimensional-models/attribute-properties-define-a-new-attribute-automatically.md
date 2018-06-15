---
title: 自動定義新屬性 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5368288930526435682723ba8f50d878ff029ce1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021705"
---
# <a name="attribute-properties---define-a-new-attribute-automatically"></a>屬性內容-自動定義新屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以在 [維度設計師] 中使用拖放式編輯，在維度中建立新屬性。  
  
### <a name="to-create-a-new-attribute-automatically"></a>自動建立新屬性  
  
1.  在維度設計師中，開啟您要在其中建立屬性的維度。  
  
2.  在 **[維度結構]** 索引標籤上，從 **[資料來源檢視]** 窗格的資料表中選取想要繫結屬性的資料行，然後將該資料行拖曳至 **[屬性]** 窗格。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會建立與所繫結之資料行相同名稱的新屬性。 如果有多個屬性使用相同資料行， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在屬性名稱後面附加一個數字。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的維度](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)   
 [維度屬性 （Property） 參考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
