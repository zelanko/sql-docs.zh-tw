---
title: 層級命名範本對話方塊（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.levelnamingtemplatedialog.f1
helpviewer_keywords:
- Level Naming Template dialog box
ms.assetid: 96cad715-213e-4eac-9003-130a2f5fc985
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: febaae6051e8428d3fed2bb6533ce2c4d972950f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078063"
---
# <a name="level-naming-template-dialog-box-analysis-services---multidimensional-data"></a>層級命名範本對話方塊 (Analysis Services - 多維度資料)
  使用 ** 中的 [層級命名範本]**[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 對話方塊，即可建構維度中之父屬性的層級命名範本。 如需層級命名範本的詳細資訊，請參閱 [NamingTemplate 元素 &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/namingtemplate-element-assl)。 您可以在 [**維度設計師**] 之 [**翻譯] 索引**標籤上的 [**翻譯詳細資料**] `NamingTemplate`窗格中，按一下屬性翻譯值的省略號按鈕（**...**），以顯示 [**層級命名範本**] 對話方塊。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**定義層級範本**|顯示您可在其中設計父屬性之層級階層的方格。 方格包含下列資料行：<br /><br /> **層級**：顯示在 [**名稱**] 中指定之名稱所用層級的序數位置。 若要為層級加入新的命名範本，請在 [層級]**** 中包含星號 (\*) 的資料列上選取 [名稱]****。<br /><br /> **名稱**：包含用於 [**層級**] 中所指出之層級的命名範本。 若要在命名範本中為層級序數位置加入預留位置，請加入單一星號 (*)。 若要新增星號做為命名範本所建立之名稱的一部分，請加入兩個\*\*星號（）。|  
|**全部清除**|選取即可移除 [定義層級範本]**** 中的所有資料列。|  
|**結果**|顯示對話方塊所建構的層級命名範本。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的設計工具和對話方塊 &#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [翻譯 &#40;維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
