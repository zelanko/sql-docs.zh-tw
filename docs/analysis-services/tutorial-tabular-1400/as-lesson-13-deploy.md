---
title: Analysis Services 教學課程第 13 課： 部署 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8ed155c0d3621c59e844e30d10dc7117e587a8f9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="deploy"></a>部署

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您可以設定部署屬性;指定要部署至的伺服器和模型的名稱。 然後將模型部署到伺服器。 部署模型之後，使用者可以使用報表用戶端應用程式連線到它。 若要進一步了解，請參閱[部署至 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)和[表格式模型方案部署](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。  
  
完成本課程的估計時間： **5 分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 然後再執行工作，在這一課，您應已完成上一課：[第 12 課： 在 Excel 中分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)。  

> [!IMPORTANT]  
> 如果部署到 Azure Analysis Services，您必須擁有[系統管理員權限](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins)serever 上。  

> [!IMPORTANT]  
> 如果您在內部部署 SQL Server 上安裝 AdventureWorksDW 範例資料庫，而且您要將您的模型部署至 Azure Analysis Services 伺服器，[在內部部署資料閘道](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)需要。
  
## <a name="deploy-the-model"></a>部署模型  
  
#### <a name="to-configure-deployment-properties"></a>若要設定部署屬性  

  
1.  在**方案總管 中**，以滑鼠右鍵按一下**AW Internet Sales**專案，然後再按一下**屬性**。  
  
2.  在**AW Internet Sales 屬性頁**對話方塊的 **部署伺服器**，請在**伺服器**屬性中，輸入完整的伺服器名稱。 如果連接到 Azure Analysis Services，則伺服器名稱必須包括完整的 URL。

    ![做為 lesson13-部署-屬性](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  在**資料庫**屬性中，輸入**Adventure Works Internet Sales**。  
  
4.  在**模型名稱**屬性中，輸入**Adventure Works Internet Sales Model**。  
  
5.  確認您的選取，然後按一下 [確定]。  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>若要部署 Adventure Works Internet Sales
  
1.  在**方案總管 中**，以滑鼠右鍵按一下**AW Internet Sales**專案 >**建置**。  

2.  以滑鼠右鍵按一下**AW Internet Sales**專案 >**部署**。

    當部署至 Azure Analysis Services，您可能會提示您輸入您的帳戶。 輸入您的組織帳戶和密碼，例如nancy@adventureworks.com。此帳戶必須是系統管理員中，在伺服器上。
  
    [部署] 對話方塊隨即出現，並顯示中繼資料，以及包含在模型中每個資料表的部署狀態。  
    
    ![as-lesson13-deploy-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. 當部署順利完成時，就可以按一下 [關閉]。  
  

這一課說明部署從 SSDT 的表格式模型最常見而且最簡單的方法。 進階的部署選項，例如 「 部署精靈 」，或使用 XMLA 和 AMO 自動化會提供更大的彈性、 一致性和排程的部署。 若要進一步了解，請參閱[表格式模型方案部署](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。

## <a name="conclusion"></a>結論  
恭喜！ 您完成撰寫和部署您的第一個 Analysis Services 表格式模型。 本教學課程已幫助您完成建立表格式模型最常執行的工作。 現在您已部署了 Adventure Works Internet Sales Model，就可以使用 SQL Server Management Studio 管理此模型，並且建立處理序指令碼及備份計畫。 使用者現在也可以連線至使用報表用戶端應用程式，例如 Microsoft Excel 或 Power BI 模型。  

![做為 lesson13 ssms](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>下一步
[使用 Power BI Desktop 連接](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[補充課程-動態安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[補充課程-詳細資料列](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[補充課程-不完全階層](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
