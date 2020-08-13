---
title: 為 Analysis Services 定義 MDX 查詢設計工具的參數 | Microsoft Docs
description: 了解如何在 Analysis Services 的多維度運算式 (MDX) 查詢設計工具中定義查詢參數。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], MDX
- Multidimensional Expressions [Reporting Services]
- Data Mining Prediction [Reporting Services]
- MDX [Reporting Services], defining parameters
- DMX [Reporting Services]
ms.assetid: 4ad1e5bc-f510-4752-b4f6-589e55317a90
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 72fe1a64e1aa474d0aa0233e8065cf351acfe432
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458193"
---
# <a name="define-parameters-in-the-mdx-query-designer-for-analysis-services"></a>在 Analysis Services 的 MDX 查詢設計工具中定義參數
  若要將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源的 MDX 查詢參數化，您必須將查詢參數加入查詢中。 在 MDX 查詢設計工具中，您可以透過指定篩選，在 [設計] 模式和 [查詢] 模式中加入查詢參數。 在您使用查詢參數來定義查詢之後，Reporting Services 會自動建立報表參數和資料集來提供有效值的清單。 如此可讓使用者指定直接傳遞給查詢的值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-define-a-query-parameter-in-mdx-in-design-mode"></a>在設計模式下定義 MDX 中的查詢參數  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源類型建立的資料集，然後按一下 [查詢]。 MDX 查詢設計工具會在 [設計] 模式中開啟。  
  
2.  將維度拖曳到篩選區域，然後將它放在 **[維度]** 資料行的第一個資料格上。  
  
3.  在 **[階層]** 資料行中，從下拉式清單選擇一個值。  
  
4.  在 **[運算子]** 資料行中，從下拉式清單選擇一個運算子。  
  
5.  在 **[篩選運算式]** 資料行中，從下拉式清單選取個別值，或是按一下 **[全部]** 成員來選擇所有的值。  
  
6.  在 **[參數]** 資料行中，選取可建立報表參數的核取方塊。  
  
7.  按一下 **[執行]** 。  
  
     在您執行查詢之後，按一下工具列上的 **[設計]** 可切換至 [查詢] 模式，以檢視已經建立的 MDX 查詢。 如果您想要繼續使用 [設計] 模式來開發查詢，請不要在 [查詢] 模式中變更查詢文字。 按一下 **[設計]** 可切換回到 [設計] 模式。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     在 [報表資料] 窗格中，展開 [參數] 節點來顯示之前自動為篩選建立的報表參數。  
  
     若要檢視可為報表參數提供可用值的資料集，請以滑鼠右鍵按一下 [報表資料] 窗格中的空白區，然後按一下 **[顯示隱藏的資料集]**。 [報表資料] 窗格會顯示報表中的所有資料集。  
  
### <a name="to-define-a-query-parameter-in-mdx-in-query-mode"></a>在查詢模式下定義 MDX 中的查詢參數  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源類型建立的資料集，然後按一下 [查詢]。 MDX 查詢設計工具會在 [設計] 模式中開啟。  
  
2.  在工具列上按一下 **[設計]** ，切換至 [查詢] 模式。  
  
3.  在 MDX 查詢設計工具的工具列上，按一下 [查詢參數] (![[查詢參數] 對話方塊圖示](../../reporting-services/report-data/media/iconqueryparameter.gif "[查詢參數] 對話方塊圖示"))。 [查詢參數] 對話方塊隨即開啟。  
  
4.  在 [參數] 資料行中，按一下 [ **\<Enter Parameter>** ]，然後鍵入參數的名稱。  
  
5.  在 [維度] 資料行中，從下拉式清單選擇一個值。  
  
6.  在 **[階層]** 資料行中，從下拉式清單選擇一個值。  
  
7.  在 **[多個值]** 資料行中，選取可建立多值參數的核取方塊。  
  
8.  在 **[預設值]** 資料行中，從下拉式清單選取單一值或多個值 (視您在步驟 5 的選擇而定)。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 在查詢設計工具工具列上，按一下 **[執行]** 。  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     在 [報表資料] 窗格中，展開 [參數] 節點來顯示之前自動為篩選建立的報表參數。  
  
     若要檢視可為報表參數提供可用值的資料集，請以滑鼠右鍵按一下 [報表資料] 窗格中的空白區，然後按一下 **[顯示隱藏的資料集]**。 [報表資料] 窗格會顯示報表中的所有資料集。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)   
 [Analysis Services MDX 查詢設計工具使用者介面](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
  
