---
title: 將屬性加入維度 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 02773eadf282fe9ac25fa96543a86c5d3e77da4c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34020995"
---
# <a name="attribute-properties---add-an--attribute-to-a-dimension"></a>屬性內容-將屬性加入維度中
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，您可以手動或自動將屬性加入至維度中。  
  
 若要自動建立屬性，在 **之維度設計師的** [維度結構] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]索引標籤上，選取您要對應到屬性的資料行，然後從 **[資料來源檢視]** 窗格中將該資料行拖曳至 **[屬性]** 窗格中。 這樣會建立一個對應到該資料行的屬性，並將資料行的相同名稱指定給屬性。 如果已有使用該名稱的屬性， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會對第一個重複名稱加入從 "1" 開始的序號後置詞。  
  
 若要手動建立屬性，請將 **[屬性]** 窗格設為方格檢視。 在方格中的最後一個資料列的 名稱 欄中，按一下  **\<新屬性 >** 項目。 輸入新屬性的名稱。 這樣子所建立的屬性，不對應到其所有屬性均為預設值的資料行。 您可以在 **的** [屬性] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 視窗中，設定新屬性的 **KeyColumns** 屬性來設定對應。  
  
 如需詳細資訊，請參閱 [自動定義新屬性](../../analysis-services/multidimensional-models/attribute-properties-define-a-new-attribute-automatically.md)、 [繫結屬性與名稱資料行](../../analysis-services/multidimensional-models/attribute-properties-bind-an-attribute-to-a-name-column.md)及 [修改屬性 (attribute) 的 KeyColumn 屬性 (property)](../../analysis-services/multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)中，您可以手動或自動將屬性加入至維度中。  
  
## <a name="see-also"></a>另請參閱  
 [維度屬性 （Property） 參考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
