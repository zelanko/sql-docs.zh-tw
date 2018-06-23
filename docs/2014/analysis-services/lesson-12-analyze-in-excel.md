---
title: 第 13 課： 在 Excel 中分析 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: b1dea62cbd78ca375a52adb7f1e6fd2285ff35e4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035106"
---
# <a name="lesson-13-analyze-in-excel"></a>第 13 課：在 Excel 中進行分析
  在這一課，您將使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的 [在 Excel 中進行分析] 功能來開啟 Microsoft Excel、自動建立模型工作空間的資料來源連接，以及自動將樞紐分析表加入至工作表。 [在 Excel 中進行分析] 功能的目的在於提供快速簡便的方法，讓您在部署模型之前測試模型設計的效率。 在本課中，您將不會執行任何資料分析。 本課程的目的在於讓您 (也就是模型作者) 熟悉可以用來測試模型設計的工具。 不像使用 [在 Excel 中進行分析] 功能，使用者將使用用戶端報表應用程式 (例如 Excel 或 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]) 連接與瀏覽已部署的模型資料。  
  
 為了完成這一課，您必須在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 所在電腦上安裝 Excel。 如需詳細資訊，請參閱[在 Excel 中進行分析 &#40;SSAS 表格式&#41;](tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
 完成本課程的估計時間：**20 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
 本主題是表格式模型教學課程的一部分，必須依序完成。 在執行本課中的工作之前，您應已完成上一課：[第 11 課：建立資料分割](lesson-10-create-partitions.md)。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>使用預設和網際網路銷售檢視方塊瀏覽  
 在這些首要工作中，您將使用預設檢視方塊 (包含所有模型物件) 以及您在第 8 課：「建立檢視方塊」中建立的網際網路銷售檢視方塊來瀏覽模型。 網際網路銷售檢視方塊不包括 Customer 資料表物件。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>若要使用預設檢視方塊瀏覽  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[在 Excel 中進行分析]**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊中，按一下 [確定]。  
  
     Excel 將會開啟，並顯示一個新的活頁簿。 系統會使用目前的使用者帳戶建立資料來源連接，並將預設檢視方塊用於定義可檢視的欄位。 樞紐分析表會自動加入到工作表中。  
  
3.  在 Excel 中，在**樞紐分析表欄位清單**，請注意**日期**和**Internet Sales**量值會出現，並將**客戶**， **日期**， **Geography**，**產品**，**產品類別目錄**，**產品子類別目錄**，和**Internet Sales**所有其個別資料行的資料表會出現。  
  
4.  關閉 Excel 而不儲存活頁簿。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>若要使用網際網路銷售檢視方塊瀏覽  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[在 Excel 中進行分析]**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊中，將 [目前的 Windows 使用者] 維持在選取狀態，並在 [檢視方塊] 下拉式清單方塊中，選取 [網際網路銷售]，然後按一下 [確定]。 Excel 便會開啟。  
  
3.  在 Excel 的 [樞紐分析表欄位清單] 中，注意 Customer 資料表已從欄位清單中排除。  
  
## <a name="browse-using-roles"></a>使用角色瀏覽  
 角色是任何表格式模型不可或缺的一部分。 如果沒有至少一個角色 (使用者會以成員形式加入角色中)，使用者將無法使用模型存取並分析資料。 [在 Excel 中進行分析] 功能提供您一個用來測試已定義之角色的方式。  
  
#### <a name="to-browse-by-using-the-internet-sales-manager-user-role"></a>若要使用 Internet Sales Manager 使用者角色瀏覽  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[在 Excel 中進行分析]**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊的 [指定要用來連接到模型的使用者名稱或角色] 中，選取 [角色]，並在下拉式清單方塊中，選取 [Internet Sales Manager (網際網路銷售經理)]，然後按一下 [確定]。  
  
     Excel 將會開啟，並顯示一個新的活頁簿。 樞紐分析表會自動建立。 [樞紐分析表欄位清單] 包含新模型中所有可用的資料欄位。  
  
## <a name="next-steps"></a>後續步驟  
 若要繼續進行本教學課程，請前往下一課：[第 14 課：部署](lesson-13-deploy.md)。  
  
  