---
title: 翻譯詳細資料（翻譯索引標籤，維度設計師）（Analysis Services 多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.translations.translationpane.tranlationdetails.f1
ms.assetid: 0aa61df3-f2b0-4703-a63b-124da672dcc3
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4a3d7934cb3bff570a2060becde6715bec88f02f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938309"
---
# <a name="translation-details-translations-tab-dimension-designer-analysis-services---multidimensional-data"></a>翻譯詳細資料 (翻譯索引標籤，維度設計師) (Analysis Services - 多維度資料)
  在 [維度設計師] 的 **[翻譯]** 索引標籤中使用 **[翻譯詳細資料]** 窗格，即可定義和管理目前所選取維度的翻譯。  
  
 **顯示翻譯詳細資料窗格**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案，然後開啟所需的維度。  
  
2.  按一下 **[翻譯]** 索引標籤。  
  
## <a name="options"></a>選項。  
 **預設語言**  
 以預設語言設定維度物件的名稱。  
  
 **物件類型**  
 顯示將翻譯的屬性。 只有已指定值的物件和屬性可以翻譯。 下列屬性可被翻譯：  
  
-   維度  
  
     `Caption` 和 `AttributeAllMember` 屬性  
  
-   屬性  
  
     `Caption`、`AttributeHierarchyDisplayFolder` 和 `NamingTemplate` 屬性  
  
    > [!NOTE]  
    >  `NamingTemplate` 屬性 (Property) 僅適用於父屬性 (Attribute)。  
  
-   階層  
  
     `Caption` 和 `AllMemberName` 屬性  
  
-   層級  
  
     `Caption` 屬性  
  
 **\<Language>**  
 以選取的語言鍵入或選取維度物件的屬性值。 按一下省略符號按鈕 (**...**) 會依據所編輯的屬性開啟其他對話方塊：  
  
-   `NamingTemplate` 屬性  
  
     顯示 [[層級命名範本] 對話方塊 &#40;Analysis Services - 多維度資料&#41;](level-naming-template-dialog-box-analysis-services-multidimensional-data.md)。  
  
-   `Caption` 屬性 (Property) (適用於屬性 (Attribute))  
  
     顯示 [[屬性資料翻譯] 對話方塊 &#40;Analysis Services - 多維度資料&#41;](attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md)。  
  
## <a name="shortcut-menu"></a>快速鍵功能表  
 以滑鼠右鍵按一下 [翻譯詳細資料]**** 窗格中的翻譯，即可顯示提供下列選項的捷徑功能表：  
  
 **新翻譯**  
 選取即可顯示 [選取語言]**** 對話方塊並建立新的翻譯。 翻譯將會在 **[翻譯詳細資料]** 方格中顯示為新的資料行。  
  
 **刪除翻譯**  
 選取以刪除選取的翻譯。  
  
> [!NOTE]  
>  唯有在資料格上按一下滑鼠右鍵來刪除翻譯時，才會啟用此選項。  
  
 **新增標題資料行**  
 在 [翻譯詳細資料]**** 方格中修改屬性時，選取即可顯示 [屬性資料翻譯]**** 對話方塊，並定義新的標題資料行。 若要啟用此選項，必須在 **[翻譯詳細資料]** 方格中選取屬性之翻譯資料行中的資料格。  
  
> [!NOTE]  
>  唯有在資料格上按一下滑鼠右鍵來刪除屬性的翻譯資料行時，才會啟用此選項。  
  
 **編輯標題資料行**  
 在 [翻譯詳細資料]**** 方格中修改屬性時，選取即可顯示 [屬性資料翻譯]**** 對話方塊，並修改現有的標題資料行。  
  
> [!NOTE]  
>   唯有選取 **[翻譯詳細資料]** 方格中的翻譯資料行中、包含屬性標題資料行的資料格時，才會啟用此選項。  
  
 **刪除標題資料行**  
 選取即可刪除 [翻譯詳細資料]**** 方格中所選取屬性的標題資料行。  
  
> [!NOTE]  
>  唯有在翻譯資料行中，以滑鼠右鍵按一下包含屬性標題資料行的資料格時，才會啟用此選項。  
  
 **顯示所有屬性**  
 選取即可切換顯示所選取維度已定義的所有屬性，包括已停用屬性階層的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [翻譯 &#40;維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
