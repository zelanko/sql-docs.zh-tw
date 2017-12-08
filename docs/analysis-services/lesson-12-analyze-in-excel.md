---
title: "第 13 課： 在 Excel 中分析 |Microsoft 文件"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c7360a1b13ae19ab6f19e4b6344056a8d9b55d3d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-12-analyze-in-excel"></a>第 12 課： 在 Excel 中進行分析
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將使用在 SSDT 中的 excel 中進行分析 開啟 Microsoft Excel、 自動建立資料來源連接至模型工作空間，並自動將樞紐分析表加入工作表。 [在 Excel 中進行分析] 功能的目的在於提供快速簡便的方法，讓您在部署模型之前測試模型設計的效率。 在本課中，您將不會執行任何資料分析。 本課程的目的在於讓您 (也就是模型作者) 熟悉可以用來測試模型設計的工具。 不像在 Excel 功能，適用於模型作者，使用中進行分析 使用者將會使用用戶端報表應用程式，例如 Excel 或 Power BI 連接到並瀏覽部署模型資料。  
  
若要完成本課程中，必須在與 SSDT 相同的電腦上安裝 Excel。 如需詳細資訊，請參閱 [[在 Excel 中進行分析]](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)所在電腦上安裝 Excel。  
  
完成本課程的估計時間： **20 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 然後再執行工作，在這一課，您應已完成上一課：[第 11 課： 建立角色](../analysis-services/lesson-11-create-roles.md)。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>使用預設和網際網路銷售檢視方塊瀏覽  
在這些首要工作，您將會瀏覽您的模型使用這兩個預設檢視方塊，其中包含所有模型物件，並使用 網際網路銷售檢視方塊您稍早。 網際網路銷售檢視方塊不包括 Customer 資料表物件。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>若要使用預設檢視方塊瀏覽  
  
1.  按一下**模型**功能表 >**在 Excel 中的進行分析**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊中，按一下 [確定]。  
  
    Excel 將會開啟，並顯示一個新的活頁簿。 系統會使用目前的使用者帳戶建立資料來源連接，並將預設檢視方塊用於定義可檢視的欄位。 樞紐分析表會自動加入至工作表。  
  
3.  在 Excel 中，在**樞紐分析表欄位清單**，請注意**DimDate**和**FactInternetSales**量值群組會出現，並將**DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，和**FactInternetSales**所有其個別資料行的資料表會出現。  
  
4.  關閉 Excel 而不儲存活頁簿。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>若要使用網際網路銷售檢視方塊瀏覽  
  
1.  按一下**模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊中，將 [目前的 Windows 使用者] 維持在選取狀態，並在 [檢視方塊] 下拉式清單方塊中，選取 [網際網路銷售]，然後按一下 [確定]。 
    
    ![做為表格式-lesson12-檢視方塊](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  在 Excel 中，在**樞紐分析表欄位**，請注意 DimCustomer 資料表從欄位清單中排除。  
    
    ![做為表格式-lesson12-欄位](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  關閉 Excel 而不儲存活頁簿。  
  
## <a name="browse-by-using-roles"></a>使用角色瀏覽  
角色是任何表格式模型不可或缺的一部分。 若沒有至少一個角色的使用者新增為成員，使用者將無法存取並分析資料，使用您的模型。 [在 Excel 中進行分析] 功能提供您一個用來測試已定義之角色的方式。  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>若要使用銷售經理使用者角色瀏覽  
  
1.  在 SSDT 中，按一下 **模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  在**在 Excel 中的進行分析**對話方塊中，於**指定使用者名稱或要用來連接至模型角色**，選取**角色**，然後在下拉式清單方塊中，選取  **銷售經理**，然後按一下 **確定**。  
  
    Excel 將會開啟，並顯示一個新的活頁簿。 自動建立樞紐分析表。 [樞紐分析表欄位清單] 包含新模型中所有可用的資料欄位。  
      
3.  關閉 Excel 而不儲存活頁簿。  
  
## <a name="whats-next"></a>下一步
移至下一課： [13 課： 部署](../analysis-services/lesson-13-deploy.md)。

  
  
  
