---
title: 定義成員群組 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a23b6fa72baeee354892c254f9b000ee12a1c9ea
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="attribute-properties---define-member-groups"></a>屬性內容-定義成員群組
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果屬性有大量成員，您可以選擇將這些成員分組成值區，減少使用者在階層中瀏覽資料時所看到的成員數目。 您也可以決定成員分組的值區數目和設定值區的命名配置。 如需詳細資訊，請參閱 [Group Attribute Members &#40;Discretization&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md) (群組屬性成員 (分隔))。  
  
 您可藉由設定 **[DiscretizationMethod]** 屬性來群組成員，這個屬性是透過 **中的** [屬性] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]視窗來加以存取。  
  
 當您建立成員群組時，要等到您處理該維度之後，使用者才能看到您所做的變更。 如需詳細資訊，請參閱[處理多維度模型 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
### <a name="to-create-member-groups"></a>若要建立成員群組  
  
1.  開啟您要使用的維度。 依預設，會開啟 **[維度結構]** 索引標籤。  
  
2.  在 [屬性] 中，以滑鼠右鍵按一下您要將其成員分組的屬性，然後按一下 [屬性]。  
  
3.  從 [DiscretizationMethod] 旁邊的下拉式清單中，選取將成員分組的方法。 如需 **DiscretizationMethod** 設定的詳細資訊，請參閱 [Group Attribute Members &#40;Discretization&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md) (群組屬性成員 (分隔))。  
  
  
