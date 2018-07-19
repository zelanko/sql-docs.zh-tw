---
title: 將採礦模型加入現有的採礦結構 |Microsoft 文件
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f8b995a5b3fb89956e690598c786dc0a09474021
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019775"
---
# <a name="add-a-mining-model-to-an-existing-mining-structure"></a>將採礦模型加入至現有的採礦結構
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在加入初始模型之後，您就可以將更多採礦模型加入至採礦結構中。 每一個模型必須包含存在於結構中的資料行，但您可以為每一個採礦模型定義不同的資料行使用方式。 如需如何定義採礦模型資料行的詳細資訊，請參閱 [採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### <a name="to-add-a-mining-model-to-the-structure"></a>若要將採礦模型加入至結構  
  
1.  從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [採礦模型] 功能表項目中，選取 [新增採礦模型]。  
  
     就會開啟 [新增採礦模型] 對話方塊。  
  
2.  在 [模型名稱] 之下，輸入新採礦模型的名稱。  
  
3.  在 [演算法名稱] 之下，選取用來建立採礦模型的演算法。  
  
4.  按一下 **[確定]**。  
  
 新的採礦模型就會出現在 [採礦模型] 索引標籤中。模型會使用已存在於結構中的預設資料行。 如需如何修改資料行的相關資訊，請參閱 [變更採礦模型的屬性](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型的工作與操作方法](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
