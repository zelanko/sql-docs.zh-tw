---
title: Analysis Services 教學課程第 12 課：在 Excel 中進行分析 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: efd71653e723344e9175d9ab1529fafd610901df
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685426"
---
# <a name="analyze-in-excel"></a>在 Excel 中分析

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您使用分析有關在 Excel 中開啟 Microsoft Excel、 自動建立的連接至模型工作區中，並自動將樞紐分析表加入工作表。 [在 Excel 中進行分析] 功能的目的在於提供快速簡便的方法，讓您在部署模型之前測試模型設計的效率。 在本課程中不執行任何資料分析。 本課程的目的在於讓您 (也就是模型作者) 熟悉可以用來測試模型設計的工具。   
  
若要完成這一課，Excel 必須安裝在 Visual Studio 的同一部電腦上。
  
完成本課程的估計時間：**5 分鐘**  
  
## <a name="prerequisites"></a>先決條件  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 執行工作之前在這一課，您應已完成上一課：[第 11 課：建立角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>使用預設和網際網路銷售檢視方塊瀏覽  

在這些首要工作中，您瀏覽您的模型使用這兩個預設檢視方塊，其中包含所有模型物件，以及使用 網際網路銷售檢視方塊您稍早。 網際網路銷售檢視方塊不包括 Customer 資料表物件。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>若要使用預設檢視方塊瀏覽  
  
1.  按一下 **模型**功能表 >**在 Excel 中的進行分析**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊中，按一下 [確定]。  
  
    Excel 會開啟新的活頁簿。 系統會使用目前的使用者帳戶建立資料來源連接，並將預設檢視方塊用於定義可檢視的欄位。 樞紐分析表會自動加入至工作表。  
  
3.  在 Excel 中，在**樞紐分析表欄位清單**，請注意**DimDate**並**FactInternetSales**量值群組會出現。 **DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**，**DimProductSubcategory**，並**FactInternetSales**與其各自資料行的資料表也會出現。  
  
4.  關閉 Excel 而不儲存活頁簿。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>若要使用網際網路銷售檢視方塊瀏覽  
  
1.  按一下 **模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊中，將 [目前的 Windows 使用者] 維持在選取狀態，並在 [檢視方塊] 下拉式清單方塊中，選取 [網際網路銷售]，然後按一下 [確定]。 
    
    ![as-lesson12-perspective](../tutorial-tabular-1400/media/as-lesson12-perspective.png)
    
3.  在 Excel 中，在**樞紐分析表欄位**，注意 DimCustomer 資料表已從欄位清單中排除。  
    
    ![as-lesson12-fields](../tutorial-tabular-1400/media/as-lesson12-fields.png)
    
4.  關閉 Excel 而不儲存活頁簿。  
  
## <a name="browse-by-using-roles"></a>使用角色來瀏覽  

角色是任何表格式模型中很重要的一部分。 而不需要至少一個角色的使用者新增為成員，使用者無法存取，並使用您的模型來分析資料。 [在 Excel 中進行分析] 功能提供您一個用來測試已定義之角色的方式。  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>若要使用銷售經理 」 使用者角色瀏覽  
  
1.  在 SSDT 中，按一下**模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  在**指定使用者名稱或要用來連接至模型角色**，選取**角色**，然後在下拉式清單方塊中，選取**銷售經理**，然後按一下  **確定**。  
  
    Excel 會開啟新的活頁簿。 自動建立樞紐分析表。 樞紐分析表欄位清單包含所有可用的資料欄位中新的模型。  
      
3.  關閉 Excel 而不儲存活頁簿。  
  
## <a name="whats-next"></a>下一步

請移至下一課：[第 13 課：部署](../tutorial-tabular-1400/as-lesson-13-deploy.md)。

  
  
  
