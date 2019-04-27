---
title: 索引鍵資料行對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.dataitemCollection.f1
helpviewer_keywords:
- DataItem Collection dialog box
ms.assetid: 585f27f2-d5eb-4516-b29a-2084010b7d51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c67966895699c34d58a0527ea27c06e7cc05ed5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729676"
---
# <a name="key-columns-dialog-box-analysis-services---multidimensional-data"></a>索引鍵資料行對話方塊 (Analysis Services - 多維度資料)
  使用 [索引鍵資料行] 對話方塊，即可變更屬性 (Attribute) 的 **KeyColumns** 屬性 (Property)。 如需詳細資訊，請參閱 [修改屬性 (Attribute) 的 KeyColumn 屬性 (Property)](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)。  
  
 **若要顯示 [索引鍵資料行] 對話方塊**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，選取屬性 (Attribute)，然後在 [屬性] 視窗中，按一下與該屬性 (Attribute) 之 **KeyColumns** 屬性 (Property) 相關聯的省略符號按鈕 (**...**)。  
  
## <a name="options"></a>選項。  
 **來源資料表**  
 選取您想要選取其索引鍵資料行的來源資料表。 您可以從 [資料來源檢視] 中所有資料表的清單中，選取來源資料表。  
  
 **可用的資料行**  
 選取您想要當做索引鍵資料行使用的資料行。 您可以從指定之 [來源資料表] 的資料行清單中選取尚未選取成索引鍵資料行的資料行。  
  
 若要將選取的資料行加入**索引鍵資料行**清單中，按一下**>**  按鈕。  
  
 **索引鍵資料行**  
 定義選取之索引鍵資料行的順序。 索引鍵資料行的順序在定義正確的複合索引鍵時很重要。 若要排序或重新排序索引鍵資料行的清單，請選取資料行，然後按一下 [向上] 或 [向下] 按鈕。  
  
 若要移除的資料行**索引鍵資料行**清單中，選取的資料行，然後按一下**\<**  按鈕。  
  
 **向上**  
 按一下即可將 [索引鍵資料行] 中選取的資料行向上移動一個位置。  
  
> [!NOTE]  
>  只有當清單包含一個以上的資料行而且選取了資料行時，才會啟用此選項。  
  
 **向下**  
 按一下即可將 [索引鍵資料行] 中選取的資料行向下移動一個位置。  
  
> [!NOTE]  
>  只有當清單包含一個以上的資料行而且選取了資料行時，才會啟用此選項。  
  
 **>**  
 按一下即可將新資料行加入 [索引鍵資料行] 中列出之資料行的結尾處。  
  
 **<**  
 按一下即可從 [索引鍵資料行] 中列出的資料行中移除選取的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
