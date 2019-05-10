---
title: 第 13 課：部署 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c20a0367612aee48c1a58e9cde8ba1a44d3fafc
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404800"
---
# <a name="lesson-13-deploy"></a>第 13 課：部署
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將設定部署屬性，指定於內部部署或 Azure 的伺服器執行個體，以及模型的名稱。 您接著會將模型部署至該執行個體。 部署您的模型之後，使用者可以使用報表用戶端應用程式連線到它。 若要深入了解部署，請參閱[表格式模型方案部署](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)並[部署至 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)。  
  
估計的時間才能完成這一課：**5 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 12 課：在 Excel 中分析](lesson-12-analyze-in-excel.md)。  
  
## <a name="deploy-the-model"></a>部署模型  
  
#### <a name="to-configure-deployment-properties"></a>若要設定部署屬性  
  
1.  在 **方案總管**，以滑鼠右鍵按一下**AW 網際網路銷售**專案，然後再按一下**屬性**。  
  
2.  在  **AW 網際網路銷售屬性頁**對話方塊的 **部署伺服器**，請在**Server**屬性，輸入 Azure Analysis Services 伺服器的名稱或在內部部署伺服器執行個體以表格式模式執行。 這會是您的模型將會部署到伺服器執行個體。  

    ![aas-deploy-deployment-server-property](media/aas-deploy-deployment-server-property.png)
 
    > [!IMPORTANT]  
    > 您必須在遠端 Analysis Services 執行個體才能對它進行部署中具有管理員權限。  
  
3.  在 **資料庫**屬性中，輸入**Adventure Works Internet Sales**。  
  
4.  在 **模型名稱**屬性中，輸入**Adventure Works Internet Sales Model**。  
  
5.  確認您的選取，然後按一下 [確定]。  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>若要部署 Adventure Works Internet Sales 表格式模型  
  
1.  在 **方案總管**，以滑鼠右鍵按一下**AW 網際網路銷售**專案 >**建置**。  

2.  以滑鼠右鍵按一下**AW 網際網路銷售**專案 >**部署**。

    部署到 Azure Analysis Services 時，將可能會提示您輸入您的帳戶。 輸入您的組織帳戶和 passsword，例如nancy@adventureworks.com。 此帳戶必須位於伺服器執行個體上系統管理員。
  
    [部署] 對話方塊隨即出現，並且顯示中繼資料以及模型中每個資料表的部署狀態。  
    
    ![aas-deploy-status](media/aas-deploy-status.png)
  
3. 當部署順利完成時，就可以按一下 [關閉]。  
  
## <a name="conclusion"></a>結論  
恭喜您！ 您完成撰寫和部署第一個 Analysis Services 表格式模型。 本教學課程已幫助您完成建立表格式模型最常執行的工作。 現在您已部署了 Adventure Works Internet Sales Model，就可以使用 SQL Server Management Studio 管理此模型，並且建立處理序指令碼及備份計畫。 使用者現在也可以連接到使用 Microsoft Excel 或 Power BI 等報表用戶端應用程式模型中。  

![as-tabular-lesson13-ssms](media/as-tabular-lesson13-ssms.png)
  
  
## <a name="see-also"></a>另請參閱  
[DirectQuery 模式](../tabular-models/directquery-mode-ssas-tabular.md)  
[設定預設的資料模型和部署屬性](../tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[表格式模型資料庫](../tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  ## <a name="whats-next"></a>下一步
*  [補充課程-使用資料列篩選實作動態安全性](supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)。

*  [補充課程-Power View 報表的設定報表屬性](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md)。
