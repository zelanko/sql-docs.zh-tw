---
title: 部署 Analysis Services 專案 |Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3d6fe74ecf361392da9000286427679194e15de9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65404040"
---
# <a name="lesson-2-5---deploying-an-analysis-services-project"></a>課程 2-5-部署 Analysis Services 專案
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

若要檢視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程專案之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程 Cube 中物件的 Cube 和維度資料，您必須將此專案部署到指定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，然後處理 Cube 及其維度。 「部署」 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體中建立已定義的物件。 「處理」 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體中的物件會將資料從基礎資料來源複製到 Cube 物件中。 如需詳細資訊，請參閱[部署 Analysis Services 專案 &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md) 和[設定 Analysis Services 專案屬性 &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md)。  
  
在開發過程的這個階段中，您通常會將 Cube 部署到開發伺服器上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 一旦您完成開發商業智慧專案之後，通常會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈，將此專案從開發伺服器部署到實際伺服器。 如需詳細資訊，請參閱[多維度模型方案部署](../multidimensional-models/multidimensional-model-solution-deployment.md)[使用部署精靈部署模型方案](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)。  
  
在下列工作中，您會檢閱 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程專案的部署屬性，然後將專案部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的本機執行個體。  
  
### <a name="to-deploy-the-analysis-services-project"></a>若要部署 Analysis Services 專案  
  
1.  在方案總管中，以滑鼠右鍵按一下 [Analysis Services Tutorial] 專案，然後按一下 [屬性]。  
  
    此時會出現 [Analysis Services Tutorial Property Pages (Analysis Services Tutorial 屬性頁)] 對話方塊，其中顯示「使用中 (開發)」組態的屬性。 您可以定義多個組態，每一個組態都有不同的屬性。 例如，開發人員可能會想要設定相同專案部署到不同開發電腦上，並使用不同的部署屬性，例如不同的資料庫名稱或處理屬性。 請注意 [輸出路徑] 屬性的值。 這個屬性指定建置專案時儲存 XMLA 部署指令碼的位置。 這些指令碼是用來將專案中的物件部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體。  
  
2.  在左窗格的 [組態屬性] 節點中，按一下 [部署]。  
  
    檢閱專案的部署屬性。 依預設， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案範本設定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案以累加方式將所有專案部署到本機電腦上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預設執行個體中，建立與專案相同名稱的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，以及在部署之後使用預設處理選項來處理物件。 如需詳細資訊，請參閱 [設定 Analysis Services 專案屬性 &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md)。  
  
    > [!NOTE]  
    > 如果您想要將專案部署至的具名執行個體[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的本機電腦上，或遠端伺服器上的執行個體中，變更**伺服器**屬性，以適當的執行個體名稱，例如\< *ServerName**>\\<** 執行個體名稱 * * >*。  
  
3.  按一下 [確定] 。  
  
4.  在方案總管中，以滑鼠右鍵按一下 [Analysis Services Tutorial] 專案，然後按一下 [部署]。 您可能需要稍等一下。  
  
    > [!NOTE]  
    > 如果部署期間遇到錯誤，請使用 SQL Server Management Studio 檢查資料庫權限。 您為資料來源連接所指定的帳戶必須有 SQL Server 執行個體的登入。 按兩下登入以檢視 [使用者對應] 屬性。 此帳戶必須有 **AdventureWorksDW2012** 資料庫的 db_datareader 權限。  
  
    [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會先建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程專案，然後使用部署指令碼將該專案部署到指定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 部署的進度會顯示在兩個視窗：**輸出**視窗和**部署進度-Analysis Services 教學課程**視窗。  
  
    如有必要，請按一下 [檢視] 功能表上的 [輸出]，開啟 [輸出] 視窗。 [輸出] 視窗會顯示整體部署進度。 **部署進度-Analysis Services 教學課程**視窗會顯示部署期間所執行的每個步驟的相關詳細資料。 如需詳細資訊，請參閱[建立 Analysis Services 專案 &#40;SSDT&#41;](../multidimensional-models/build-analysis-services-projects-ssdt.md) 和[部署 Analysis Services 專案 &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md)。  
  
5.  檢閱的內容**輸出**視窗和**部署進度-Analysis Services 教學課程**視窗，以確認已建立 cube，部署，並沒有錯誤處理。  
  
6.  若要隱藏 [部署進度 - Analysis Services Tutorial] 視窗，請按一下視窗工具列上的 [自動隱藏] 圖示 (看起來像圖釘)。  
  
7.  若要隱藏 [輸出] 視窗，請按一下視窗工具列上的 [自動隱藏] 圖示。  
  
您已順利部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程 Cube 到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的本機執行個體，然後處理已部署的 Cube。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[瀏覽 Cube](lesson-2-6-browsing-the-cube.md)  
  
## <a name="see-also"></a>另請參閱  
[部署 Analysis Services 專案 &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
[設定 Analysis Services 專案屬性 &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  
  
