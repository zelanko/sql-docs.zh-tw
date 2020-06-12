---
title: 索引鍵資料行對話方塊（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.dataitemCollection.f1
helpviewer_keywords:
- DataItem Collection dialog box
ms.assetid: 585f27f2-d5eb-4516-b29a-2084010b7d51
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0758c814a7edce134be01ebf766a12832e942a61
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543700"
---
# <a name="key-columns-dialog-box-analysis-services---multidimensional-data"></a>索引鍵資料行對話方塊 (Analysis Services - 多維度資料)
  使用 [索引鍵資料行]**** 對話方塊，即可變更屬性 (Attribute) 的 **KeyColumns** 屬性 (Property)。 如需詳細資訊，請參閱 [修改屬性 (Attribute) 的 KeyColumn 屬性 (Property)](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)。  
  
 **顯示索引鍵資料行對話方塊**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，選取屬性 (Attribute)，然後在 [屬性]**** 視窗中，按一下與該屬性 (Attribute) 之 **KeyColumns** 屬性 (Property) 相關聯的省略符號按鈕 (**...**)。  
  
## <a name="options"></a>選項  
 **來源資料表**  
 選取您想要選取其索引鍵資料行的來源資料表。 您可以從 [資料來源檢視] 中所有資料表的清單中，選取來源資料表。  
  
 **可用的資料行**  
 選取您想要當做索引鍵資料行使用的資料行。 您可以從指定之 [來源資料表]**** 的資料行清單中選取尚未選取成索引鍵資料行的資料行。  
  
 若要將選取的資料行加入至 [索引**鍵資料行**] 清單，請按一下該 **>** 按鈕。  
  
 **索引鍵資料行**  
 定義選取之索引鍵資料行的順序。 索引鍵資料行的順序在定義正確的複合索引鍵時很重要。 若要排序或重新排序索引鍵資料行的清單，請選取資料行，然後按一下 [向上]**** 或 [向下]**** 按鈕。  
  
 若要從 [索引**鍵資料行**] 清單中移除資料行，請選取資料行，然後按一下 **\<** 按鈕。  
  
 **Up**  
 按一下即可將 [索引鍵資料行]**** 中選取的資料行向上移動一個位置。  
  
> [!NOTE]  
>  只有當清單包含一個以上的資料行而且選取了資料行時，才會啟用此選項。  
  
 **Down**  
 按一下即可將 [索引鍵資料行]**** 中選取的資料行向下移動一個位置。  
  
> [!NOTE]  
>  只有當清單包含一個以上的資料行而且選取了資料行時，才會啟用此選項。  
  
 **>**  
 按一下即可將新資料行加入 [索引鍵資料行]**** 中列出之資料行的結尾處。  
  
 **<**  
 按一下即可從 [索引鍵資料行]**** 中列出的資料行中移除選取的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的設計工具和對話方塊 &#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
