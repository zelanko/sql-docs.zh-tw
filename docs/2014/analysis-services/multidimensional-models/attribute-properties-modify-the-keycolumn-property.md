---
title: 修改屬性（Attribute）的 KeyColumn 屬性（Property） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- binding attributes [Analysis Services]
- attributes [Analysis Services], binding
- key columns [Analysis Services]
ms.assetid: a2643be4-8123-4cc3-baf9-e5ec54a1669d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5c5effed34dda946d3c65028aa5834f4fbddf7cd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077244"
---
# <a name="modify-the-keycolumn-property-of-an-attribute"></a>修改屬性 (attribute) 的 KeyColumn 屬性 (property)
  您可以修改屬性 (Attribute) 的 **KeyColumns** 屬性 (Property)。 例如，您可能要為屬性指定複合索引鍵，而不是單一索引鍵。  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>修改屬性 (Attribute) 的 KeyColumns 屬性 (Property)  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟您要在其中修改 **KeyColumns** 屬性的專案。  
  
2.  執行下列其中一個程序，開啟 [維度設計師]：  
  
    -   在**方案總管**中，以滑鼠右鍵按一下 [維度]**** 資料夾中的維度，然後按一下 [開啟]**** 或 [檢視表設計工具]****。  
  
         -或-  
  
    -   在 [Cube 設計師] 的 [ **Cube 結構**] 索引標籤上，展開 [**維度**] 窗格中的 Cube 維度，然後按一下 [ ** \<編輯維度>**]。  
  
3.  在 [維度結構]**** 索引標籤的 [屬性]**** 窗格中，按一下要修改其 **KeyColumns** 屬性 (Property) 的屬性 (Attribute)。  
  
4.  在 [屬性]**** 視窗中，按一下 **KeyColumns** 屬性的值。  
  
5.  按一下屬性方塊之值資料格中的瀏覽按鈕 **(...)** 。  
  
     [索引鍵資料行]**** 對話方塊隨即開啟。  
  
6.  若要從 [索引鍵資料行]**** 清單中移除現有的索引鍵資料行，請選取資料行，然後按一下 [\<]**** 按鈕。  
  
7.  若要在 [可用的資料行]**** 清單中加入索引鍵資料行，請選取資料行，然後按一下 [>]**** 按鈕。  
  
    > [!NOTE]  
    >  如果您要定義數個索引鍵資料行，這些資料行出現在 [索引鍵資料行]**** 清單中的順序會影響顯示順序。 例如，月份屬性有兩個索引鍵資料行：月和年。 如果年份資料行出現在月份資料行前的清單中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將會先依照年份排序，然後再依照月份排序。 如果月份資料行出現在年份資料行前， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將會先依照月份排序，然後再依照年份排序。  
  
8.  若要變更索引鍵資料行的順序，請選取資料行，然後按一下 [向上]**** 或 [向下]**** 按鈕。  
  
## <a name="see-also"></a>另請參閱  
 [維度屬性 (attribute) 屬性 (property) 參考](dimension-attribute-properties-reference.md)  
  
  
