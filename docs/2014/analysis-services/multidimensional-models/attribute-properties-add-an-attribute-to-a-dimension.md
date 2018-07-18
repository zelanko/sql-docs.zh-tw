---
title: 將屬性加入維度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- adding attributes
- automatic attribute creation
- attributes [Analysis Services], creating
- attributes [Analysis Services], adding
- manual attribute creation [Analysis Services]
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25bbd679cd27aafd2fb71986aac1991556b3c890
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237758"
---
# <a name="add-an--attribute-to-a-dimension"></a>將屬性加入維度中
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，您可以手動或自動將屬性加入至維度中。  
  
 若要自動建立屬性，在 **之維度設計師的** [維度結構] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]索引標籤上，選取您要對應到屬性的資料行，然後從 **[資料來源檢視]** 窗格中將該資料行拖曳至 **[屬性]** 窗格中。 這樣會建立一個對應到該資料行的屬性，並將資料行的相同名稱指定給屬性。 如果已有使用該名稱的屬性， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會對第一個重複名稱加入從 "1" 開始的序號後置詞。  
  
 若要手動建立屬性，請將 **[屬性]** 窗格設為方格檢視。 在方格中的最後一個資料列的 [名稱] 欄中，按一下**\<新屬性 >** 項目。 輸入新屬性的名稱。 這樣子所建立的屬性，不對應到其所有屬性均為預設值的資料行。 您可以在 **的** [屬性] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 視窗中，設定新屬性的 **KeyColumns** 屬性來設定對應。  
  
 如需詳細資訊，請參閱 [自動定義新屬性](attribute-properties-define-a-new-attribute-automatically.md)、 [手動定義新屬性](../define-a-new-attribute-manually.md)、 [繫結屬性與名稱資料行](attribute-properties-bind-an-attribute-to-a-name-column.md)及 [修改屬性 (attribute) 的 KeyColumn 屬性 (property)](attribute-properties-modify-the-keycolumn-property.md)。  
  
## <a name="see-also"></a>另請參閱  
 [維度屬性內容參考](dimension-attribute-properties-reference.md)  
  
  
