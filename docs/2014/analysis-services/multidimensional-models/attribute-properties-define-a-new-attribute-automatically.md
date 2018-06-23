---
title: 自動定義新屬性 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 007f736d3e14a4e8ac2d2b1446819b72a3443fbd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131404"
---
# <a name="define-a-new-attribute-automatically"></a>自動定義新屬性
  您可以在 [維度設計師] 中使用拖放式編輯，在維度中建立新屬性。  
  
### <a name="to-create-a-new-attribute-automatically"></a>自動建立新屬性  
  
1.  在維度設計師中，開啟您要在其中建立屬性的維度。  
  
2.  在 **[維度結構]** 索引標籤上，從 **[資料來源檢視]** 窗格的資料表中選取想要繫結屬性的資料行，然後將該資料行拖曳至 **[屬性]** 窗格。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會建立與所繫結之資料行相同名稱的新屬性。 如果有多個屬性使用相同資料行， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在屬性名稱後面附加一個數字。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的維度](dimensions-in-multidimensional-models.md)   
 [維度屬性內容參考](dimension-attribute-properties-reference.md)  
  
  