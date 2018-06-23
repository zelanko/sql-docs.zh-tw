---
title: 建立模型資料行的別名 |Microsoft 文件
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
- data mining [Analysis Services], how-to topics
- mining models [Analysis Services], columns
- column names [Analysis Services]
ms.assetid: c80ebe66-a8f8-4f24-9fe8-8288de9d13bc
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cf049cdd7fabbc50fdacf5ab72ca3ce1845482f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035557"
---
# <a name="create-an-alias-for-a-model-column"></a>建立模型資料行的別名
  您可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中為模型資料行建立別名。 當採礦結構名稱太長而不易處理，或者當您想要將資料行重新命名，以針對其內容或它在模型中的使用方式給予較為描述性的名稱時，這麼做很有用。 例如，如果建立結構資料行的複本，然後再針對特定的模型以不同的方式分隔資料行，就可以將該資料行重新命名，以更為正確的方式來反映內容。  
  
 若要建立模型資料行的別名，可以使用 [屬性] 窗格，並設定資料行的 [Name](../scripting/properties/name-element-assl.md) 屬性。  
  
 在資料採礦設計師的 [採礦模型] 索引標籤上，別名會顯示在資料行使用方式標籤旁的括弧中。  
  
 如需如何在採礦模型中設定屬性的資訊，請參閱[採礦模型資料行](mining-model-columns.md)。  
  
### <a name="to-add-an-alias-to-a-mining-model-column"></a>若要將別名加入至採礦模型資料行  
  
1.  在資料採礦設計師的 [採礦模型] 索引標籤上，以滑鼠右鍵在採礦模型中按一下要變更的採礦資料行的資料格，然後選取 [屬性]。  
  
2.  在畫面右側的 [屬性] 視窗中，按一下 [Name] 屬性旁的資料格，然後刪除目前的值。 輸入資料行的新名稱。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型的工作與操作方法](mining-model-tasks-and-how-tos.md)   
 [採礦模型屬性](mining-model-properties.md)  
  
  