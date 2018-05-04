---
title: 第 14 課： 部署 |Microsoft 文件
ms.custom: ''
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 146ed0ded54d73fe523b49389d876e103d3a9c44
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-13-deploy"></a>第 13 課： 部署
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將設定部署屬性;指定內部部署或 Azure 的伺服器執行個體，以及模型的名稱。 然後您將模型部署至該執行個體中。 部署模型之後，使用者可以使用報表用戶端應用程式連線到它。 若要了解有關部署的詳細資訊，請參閱[表格式模型方案部署](../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)和[部署至 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)。  
  
完成本課程的估計時間： **5 分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소  
本主題是表格式模型教學課程的一部分，必須依序完成。 然後再執行工作，在這一課，您應已完成上一課：[第 12 課： 在 Excel 中分析](../analysis-services/lesson-12-analyze-in-excel.md)。  
  
## <a name="deploy-the-model"></a>部署模型  
  
#### <a name="to-configure-deployment-properties"></a>若要設定部署屬性  
  
1.  在**方案總管 中**，以滑鼠右鍵按一下**AW Internet Sales**專案，然後再按一下**屬性**。  
  
2.  在**AW Internet Sales 屬性頁**對話方塊的 **部署伺服器**，請在**伺服器**屬性中，輸入 Azure Analysis Services 伺服器的名稱或在內部部署伺服器執行個體以表格式模式執行。 這會是您的模型將會部署到伺服器執行個體。  

    ![aas-部署-部署-伺服器-屬性](../analysis-services/media/aas-deploy-deployment-server-property.png)
 
    > [!IMPORTANT]  
    > 系統管理員權限必須在遠端 Analysis Services 執行個體中才能部署它。  
  
3.  在**資料庫**屬性中，輸入**Adventure Works Internet Sales**。  
  
4.  在**模型名稱**屬性中，輸入**Adventure Works Internet Sales Model**。  
  
5.  確認您的選取，然後按一下 [確定]。  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>若要部署 Adventure Works Internet Sales 表格式模型  
  
1.  在**方案總管 中**，以滑鼠右鍵按一下**AW Internet Sales**專案 >**建置**。  

2.  以滑鼠右鍵按一下**AW Internet Sales**專案 >**部署**。

    當部署至 Azure Analysis Services，將可能會提示您輸入您的帳戶。 輸入您的組織帳戶和 passsword，例如nancy@adventureworks.com。此帳戶必須是系統管理員中，伺服器執行個體上。
  
    [部署] 對話方塊隨即出現，並且顯示中繼資料以及模型中每個資料表的部署狀態。  
    
    ![aas 部署狀態](../analysis-services/media/aas-deploy-status.png)
  
3. 當部署順利完成時，就可以按一下 [關閉]。  
  
## <a name="conclusion"></a>結論  
恭喜！ 您完成撰寫和部署您的第一個 Analysis Services 表格式模型。 本教學課程已幫助您完成建立表格式模型最常執行的工作。 現在您已部署了 Adventure Works Internet Sales Model，就可以使用 SQL Server Management Studio 管理此模型，並且建立處理序指令碼及備份計畫。 使用者現在也可以連線至使用報表用戶端應用程式，例如 Microsoft Excel 或 Power BI 模型。  

![做為表格式-lesson13-ssms](../analysis-services/media/as-tabular-lesson13-ssms.png)
  
  
## <a name="see-also"></a>另請參閱  
[DirectQuery 模式](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)  
[設定預設的資料模型和部署屬性](../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[表格式模型資料庫](../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  ## <a name="whats-next"></a>下一步
*  [補充課程-使用資料列篩選實作動態安全性](../analysis-services/supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)。

*  [補充課程-設定 Power View 報表的報表屬性](../analysis-services/supplemental-lesson-configure-reporting-properties-for-power-view-reports.md)。
