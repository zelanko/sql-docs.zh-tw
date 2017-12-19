---
title: "將採礦模型加入現有的採礦結構 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], adding
- mining structures [Analysis Services], mining models
- adding mining models
ms.assetid: fcf72300-0674-4e73-a826-9b8eeffefbb5
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 79d2c8b506cd42bd04ae4fb95f28fa2b3a07f613
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="add-a-mining-model-to-an-existing-mining-structure"></a>將採礦模型加入至現有的採礦結構
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]加入初始模型之後，您可以加入採礦結構中，加入更多採礦模型。 每一個模型必須包含存在於結構中的資料行，但您可以為每一個採礦模型定義不同的資料行使用方式。 如需如何定義採礦模型資料行的詳細資訊，請參閱 [採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### <a name="to-add-a-mining-model-to-the-structure"></a>若要將採礦模型加入至結構  
  
1.  從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [採礦模型] 功能表項目中，選取 [新增採礦模型]。  
  
     就會開啟 [新增採礦模型] 對話方塊。  
  
2.  在 [模型名稱] 之下，輸入新採礦模型的名稱。  
  
3.  在 [演算法名稱] 之下，選取用來建立採礦模型的演算法。  
  
4.  按一下 **[確定]**。  
  
 新的採礦模型就會出現在 [採礦模型] 索引標籤中。模型會使用已存在於結構中的預設資料行。 如需如何修改資料行的相關資訊，請參閱 [變更採礦模型的屬性](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)。  
  
## <a name="see-also"></a>請參閱  
 [採礦模型工作和使用說明](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
