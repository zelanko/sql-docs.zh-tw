---
title: 建立方案與資料來源 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0488b231-1045-4169-aabb-c1005d86ca30
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2f089f487586b6def3d2ddd4eecdbbde1532952b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020597"
---
# <a name="creating-a-solution-and-data-source-intermediate-data-mining-tutorial"></a>建立方案與資料來源 (中繼資料採礦教學課程)
  若要使用資料採礦，您必須先在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中使用 **[Analysis Services 多維度和資料採礦專案]** 範本建立專案。 當您開啟範本時，它會自動將您進行資料採礦可能需要的所有結構描述載入設計師中：資料來源、採礦結構和資料模型，甚至是 Cube (如果您的採礦結構使用多維度資料)。  
  
 當您使用建立專案時，直到部署方案之前，方案都會儲存為本機檔案。 當您部署方案時， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會尋找專案屬性中指定的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器，並且用專案的名稱建立新的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 預設會針對新專案使用 **localhost** 執行個體。 如果您要使用具名執行個體，或者如果為預設執行個體指定了不同名稱，您必須將專案的部署資料庫屬性變更到您要建立資料採礦物件的位置。  
  
 如需詳細資訊[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]專案，請參閱[建立 Analysis Services 專案&#40;SSDT&#41;](../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)。  
  
### <a name="to-create-a-new-analysis-services-project-for-this-tutorial"></a>為這個教學課程建立新的 Analysis Services 專案  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
2.  在 [檔案]  功能表中，指向 [新增] ，然後按一下 [專案] 。  
  
3.  從 **[已安裝的範本]** 窗格選取 **[Analysis Services 多維度和資料採礦專案]** 。  
  
4.  在 [名稱]  方塊中，將新專案命名為 **DM Intermediate**。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored-optional"></a>變更用於存放資料採礦物件的執行個體 (選擇性)  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，按一下 **[專案]** 功能表上的 **[屬性]**。  
  
2.  在 [屬性頁]  窗格的左側，按一下 [部署] 。  
  
3.  確認 **[伺服器]** 的名稱為 **[localhost]**。 如果您要使用不同的執行個體，請輸入執行個體的名稱。 如果您要使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的具名執行個體，請輸入電腦名稱，再輸入執行個體名稱。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-deployment-properties-for-a-project-optional"></a>變更專案的部署屬性 (選擇性)  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 **[屬性]**。  
  
     -或-  
  
     在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中的 **[專案]** 功能表上，選取 **[屬性]**。  
  
2.  在 [屬性頁]  窗格的左側，按一下 [部署] 。  
  
     在 **[選項]** 窗格中，選取 **[部署模式]**，然後將選項設為 **[全部部署]** 以進行覆寫，或是設為 **[只部署變更]** 以更新物件或加入物件。  
  
## <a name="creating-a-data-source"></a>建立資料來源  
 在基本資料採礦教學課程中，您已建立一個 *「資料來源」* (Data source)，其中存放 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫的連接資訊。 請遵循相同的步驟，建立此方案的 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料來源。  
  
#### <a name="to-create-a-data-source"></a>建立資料來源  
  
-   [建立資料來源&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
 單一資料來源可以支援多個資料來源檢視，而且每一個資料來源檢視可以包含多個資料表。 不過，由於資料來源和資料來源檢視會連同您建立的資料採礦模型一起部署到您的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，因此最佳做法是只將各資料採礦模型或模型群組所需的必要資料表加入每個資料來源檢視中。  
  
 在下列課程中，您將加入資料來源檢視，以支援每一個新的案例。 只有購物籃和時序群集課程使用相同的資料來源檢視；否則，每個案例都會使用不同的資料來源檢視，因此課程都各自獨立，而且可以分開完成。  
  
|狀況|資料來源檢視中包含的資料|  
|--------------|-------------------------------------------|  
|[第 2 課：建立預測狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)|不同區域自行車型號的每月銷售報表，收集為單一檢視。|  
|[第 3 課：建立購物籃狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)|一個包含客戶訂單清單的資料表，和一個顯示每個客戶個別購買情況的巢狀資料表。|  
|[第 4 課：建立時序群集案例&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)|用於購物籃分析的相同資料，其中加入了識別碼，用來顯示項目購買的順序。|  
|[第 5 課：建立類神經網路和羅吉斯迴歸模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)|單一資料表，其中包含來自客服中心的一些初步效能追蹤資料。|  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：建立預測狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦專案](../../2014/analysis-services/data-mining/data-mining-projects.md)   
 [多維度模型中的資料來源檢視](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
