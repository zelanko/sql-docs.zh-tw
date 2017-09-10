---
title: "建立模型資料行的別名 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- mining models [Analysis Services], columns
- column names [Analysis Services]
ms.assetid: c80ebe66-a8f8-4f24-9fe8-8288de9d13bc
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a49c5aac7289573631a3ed50349c98690c28212d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-an-alias-for-a-model-column"></a>建立模型資料行的別名
  您可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中為模型資料行建立別名。 當採礦結構名稱太長而不易處理，或者當您想要將資料行重新命名，以針對其內容或它在模型中的使用方式給予較為描述性的名稱時，這麼做很有用。 例如，如果建立結構資料行的複本，然後再針對特定的模型以不同的方式分隔資料行，就可以將該資料行重新命名，以更為正確的方式來反映內容。  
  
 若要建立模型資料行的別名，可以使用 [屬性] 窗格，並設定資料行的 [Name](../../analysis-services/scripting/properties/name-element-assl.md) 屬性。  
  
 在資料採礦設計師的 [採礦模型] 索引標籤上，別名會顯示在資料行使用方式標籤旁的括弧中。  
  
 如需如何在採礦模型中設定屬性的資訊，請參閱[採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### <a name="to-add-an-alias-to-a-mining-model-column"></a>若要將別名加入至採礦模型資料行  
  
1.  在資料採礦設計師的 [採礦模型] 索引標籤上，以滑鼠右鍵在採礦模型中按一下要變更的採礦資料行的資料格，然後選取 [屬性]。  
  
2.  在畫面右側的 [屬性] 視窗中，按一下 [Name] 屬性旁的資料格，然後刪除目前的值。 輸入資料行的新名稱。  
  
## <a name="see-also"></a>請參閱＜  
 [採礦模型工作和使用說明](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [採礦模型屬性](../../analysis-services/data-mining/mining-model-properties.md)  
  
  
