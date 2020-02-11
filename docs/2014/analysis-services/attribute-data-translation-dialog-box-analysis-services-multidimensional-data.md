---
title: 屬性資料翻譯對話方塊（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.dimensionstoragesettings.f1
helpviewer_keywords:
- Attribute Data Translation dialog box
ms.assetid: bed286de-1e9b-49de-b09e-3cd076aba152
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2304f664178ab1f5d3718cccdcb4b1775a72948e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66063070"
---
# <a name="attribute-data-translation-dialog-box-analysis-services---multidimensional-data"></a>屬性資料翻譯對話方塊 (Analysis Services - 多維度資料)
  使用 [屬性資料翻譯]**** 對話方塊，即可設定包含翻譯標題資料的資料行，以及要用於翻譯資料的定序和排序次序。 您可依下列方式顯示 [屬性資料翻譯]**** 對話方塊：  
  
-   從 [維度設計師]**** 之 [翻譯]**** 索引標籤上的 [工具列]**** 窗格，按一下 [新增標題資料行]**** 或 [編輯標題資料行]****。  
  
-   以滑鼠右鍵按一下 [維度設計師]**** 之 [翻譯]**** 索引標籤上的 [翻譯詳細資料]**** 窗格，然後選取 [新增標題資料行]**** 或 [編輯標題資料行]****。  
  
## <a name="options"></a>選項。  
 **Attribute**  
 顯示選取的屬性。  
  
 **語言**  
 顯示選取的語言。  
  
 **已翻譯標題**  
 設定所選屬性的目前已翻譯標題。  
  
 **翻譯資料行**  
 設定儲存翻譯標題資料的資料行。 只能選取一個資料行。 將會顯示主維度資料表所參考的所有相關資料表。  
  
 **定序指示項**  
 設定所選屬性的定序指示項。 依預設，會選取目前的 Windows 定序。 按一下向下箭頭即可從可用的定序中選取定序。  
  
 **二**  
 選取此選項，即可根據為每個字元定義的位元模式來排序和比較資料。 二進位排序順序有區分大小寫，亦即小寫優先於大寫，而且有區分腔調字。 這是最快的排序順序。  
  
 如果沒有選取此選項， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會遵循相關聯之語言或字母字典中所定義的排序和比較規則。  
  
> [!NOTE]  
>  如果選取此選項，會停用 [區分大小寫]****、[區分腔調字]****、[區分假名]**** 和 [區分全半形]**** 等選項。  
  
 **區分大小寫**  
 選取此選項，即可根據為關聯之語言或字母提供的字典規則來排序和比較資料，以及區別大寫和小寫字母。  
  
 如果未選取，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將大小寫字母視為相同。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]未選取 [區分**大小寫**] 時，不會定義小寫字母是否會以較低或較高的方式排序。  
  
 **區分腔調字**  
 選取此選項，即可根據為關聯之語言或字母提供的字典規則來排序和比較資料，以及區別有腔調和無腔調字元。 例如，'a' 不等於 'á'。  
  
 如果未選取， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將有腔調與無腔調的字母視為相同。  
  
 **區分假名**  
 選取此選項，即可根據為關聯之語言或字母提供的字典規則來排序和比較資料，以及區別兩種日文假名字元：平假名和片假名。  
  
 如果未選取， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將平假名與片假名字元視為相同。  
  
 **區分全半形**  
 選取此選項，即可根據為關聯之語言或字母提供的字典規則來排序和比較資料，以及區別單一位元組字元 (半形) 和使用雙位元組字元 (全形) 表示的相同字元。  
  
 如果未選取， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會將相同字元的單一位元組與雙位元組表示方式視為相同。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的設計工具和對話方塊 &#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [翻譯詳細資料 &#40;[翻譯] 索引標籤、[維度設計師]&#41; &#40;Analysis Services 多維度資料&#41;](translation-details-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
