---
title: 第 13 課： 在 Excel 中進行分析 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a59a91b86da12dc9df4b9d3ce2b65ef456439627
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37971670"
---
# <a name="lesson-12-analyze-in-excel"></a>第 12 課： 在 Excel 中進行分析
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將使用 SSDT 中的 Excel 功能中進行分析 來開啟 Microsoft Excel、 自動建立資料來源連接至模型工作區中，以及自動將樞紐分析表加入工作表。 [在 Excel 中進行分析] 功能的目的在於提供快速簡便的方法，讓您在部署模型之前測試模型設計的效率。 在本課中，您將不會執行任何資料分析。 本課程的目的在於讓您 (也就是模型作者) 熟悉可以用來測試模型設計的工具。 不同於使用中進行分析，在 Excel 功能，可供模型作者，使用者將使用用戶端報表應用程式，例如 Excel 或 Power BI 來連線及瀏覽已部署的模型資料。  
  
若要完成這一課，Excel 必須安裝在與 SSDT 相同的電腦上。 如需詳細資訊，請參閱 [[在 Excel 中進行分析]](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)所在電腦上安裝 Excel。  
  
完成本課程的估計時間： **20 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 11 課： 建立角色](../analysis-services/lesson-11-create-roles.md)。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>使用預設和網際網路銷售檢視方塊瀏覽  
在這些首要工作中，您會瀏覽您的模型使用這兩個預設檢視方塊，其中包含所有模型物件，以及使用 網際網路銷售檢視方塊您稍早。 網際網路銷售檢視方塊不包括 Customer 資料表物件。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>若要使用預設檢視方塊瀏覽  
  
1.  按一下 **模型**功能表 >**在 Excel 中的進行分析**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊中，按一下 [確定]。  
  
    Excel 將會開啟，並顯示一個新的活頁簿。 系統會使用目前的使用者帳戶建立資料來源連接，並將預設檢視方塊用於定義可檢視的欄位。 樞紐分析表會自動加入至工作表。  
  
3.  在 Excel 中，在**樞紐分析表欄位清單**，請注意**DimDate**並**FactInternetSales**量值群組會出現，以及**DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，並**FactInternetSales**所有依個別資料行的資料表會出現。  
  
4.  關閉 Excel 而不儲存活頁簿。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>若要使用網際網路銷售檢視方塊瀏覽  
  
1.  按一下 **模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  於 [在 Excel 中進行分析] 對話方塊中，將 [目前的 Windows 使用者] 維持在選取狀態，並在 [檢視方塊] 下拉式清單方塊中，選取 [網際網路銷售]，然後按一下 [確定]。 
    
    ![做為表格式-lesson12-檢視方塊](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  在 Excel 中，在**樞紐分析表欄位**，注意 DimCustomer 資料表已從欄位清單中排除。  
    
    ![為表格式-lesson12-欄位](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  關閉 Excel 而不儲存活頁簿。  
  
## <a name="browse-by-using-roles"></a>使用角色來瀏覽  
角色是任何表格式模型不可或缺的一部分。 而不需要至少一個角色的使用者新增為成員，使用者將無法存取，並使用您的模型來分析資料。 [在 Excel 中進行分析] 功能提供您一個用來測試已定義之角色的方式。  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>若要使用銷售經理 」 使用者角色瀏覽  
  
1.  在 SSDT 中，按一下**模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  在**在 Excel 中的進行分析**對話方塊中，於**指定的使用者名稱或要用來連接至模型角色**，選取**角色**，然後在下拉式清單方塊中，選取  **銷售經理**，然後按一下**確定**。  
  
    Excel 將會開啟，並顯示一個新的活頁簿。 自動建立樞紐分析表。 [樞紐分析表欄位清單] 包含新模型中所有可用的資料欄位。  
      
3.  關閉 Excel 而不儲存活頁簿。  
  
## <a name="whats-next"></a>下一步
移至下一個課程︰[第 13 課： 部署](../analysis-services/lesson-13-deploy.md)。

  
  
  
