---
title: 屬性 （維度結構索引標籤，維度設計師） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.attributespane.f1
ms.assetid: 627eaa08-7638-4edd-bdfa-0d8175a7cde5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 522bffc53240a7456ee77911b4f3044ffe0f231c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48229808"
---
# <a name="attributes-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>屬性 (維度結構索引標籤，維度設計師) (Analysis Services - 多維度資料)
  使用此窗格即可管理與選取之維度相關聯的屬性。 您可以將屬性從這個窗格拖曳到 **[階層]** 窗格，以便建立階層和層級。 如需詳細資訊，請參閱 <<c0> [ 階層&#40;維度結構索引標籤，維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)。</c0>  
  
 若要建立屬性，在清單模式、樹狀模式或檢視模式時，請將資料行從 **[資料來源檢視]** 窗格拖曳到 **[屬性]** 窗格。 若要移除屬性，請選取快速鍵功能表中的 **[刪除]** 。  
  
 **若要顯示 [屬性] 窗格**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案，然後開啟所需的維度。  
  
2.  如果沒有選取，請按一下 **[維度結構]** 索引標籤。  
  
## <a name="options"></a>選項。  
 **屬性**  
 顯示選取之維度可以使用的屬性。 可以在下列模式中檢視此選項：  
  
-   清單模式  
  
     使用此模式即可建立和修改階層。 若要在清單模式中檢視屬性，請選取快速鍵功能表中的 **[顯示屬性於]** ，然後按一下 **[清單]**。  
  
-   樹狀模式  
  
     使用此模式即可建立和修改階層。 若要在樹狀模式中檢視屬性，請選取快速鍵功能表中的 **[顯示屬性於]** ，然後按一下 **[樹狀]**。  
  
-   方格模式  
  
     使用此模式即可手動建立維度，或修改屬性 (Attribute) 的屬性 (Property)。 若要在方格模式中檢視屬性，請選取快速鍵功能表中的 **[顯示屬性於]** ，然後按一下 **[方格]**。  
  
## <a name="grid-mode-options"></a>方格模式選項  
 在方格模式中檢視屬性時，您有權存取下表列出的資料行。  
  
 **名稱**  
 顯示屬性的名稱。  
  
 **Usage**  
 設定選取之屬性的使用方式。 按一下向下箭號，即可從下列選擇中選取：  
  
|值|描述|  
|-----------|-----------------|  
|一般|識別一般屬性。|  
|索引鍵|識別維度的索引鍵屬性。 這會對應至維度的分葉成員。 每維度只能有一個索引鍵屬性。 若要修改，請在 [屬性] 窗格中按一下 [KeyColumns] 屬性旁的省略符號按鈕 (**...**)。|  
|父系|代表父子式關聯性的父屬性。 此關聯性中的子屬性必須永遠為索引鍵屬性。|  
|AccountType|代表帳戶類型屬性。 當量值的彙總函式設定為「依帳戶」時，會由伺服器或引擎使用此屬性。|  
  
 **型別**  
 設定屬性的類型。 按一下向下箭號，即可從可用的選擇中選取。  
  
 **索引鍵資料行**  
 顯示基礎資料行的資料類型。 建立新屬性時，按一下向下箭號，即可從可用的選擇中選取。  
  
 **名稱資料行**  
 顯示基礎資料行的位置。 建立新屬性時，按一下向下箭號，即可在 **[與索引鍵相同]** 和 **[分隔資料行]** 之間選取。 如果選擇 **[分隔資料行]** ，則 **[屬性]** 窗格中的 **[NameColumn]** 屬性 (Property) 會設定儲存用於屬性 (Attribute) 之名稱的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [維度結構&#40;維度設計工具&#41; &#40;Analysis Services-多維度資料&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [階層&#40;維度結構索引標籤，維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)   
 [工具列&#40;維度結構索引標籤，維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)  
  
  
