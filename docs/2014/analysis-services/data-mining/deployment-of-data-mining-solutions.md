---
title: 資料採礦方案的部署 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], deploying
- deploying [Analysis Services], production environments
- deploying [Analysis Services - data mining]
- solutions [Analysis Services], deploying
- models [Analysis Services], data mining
ms.assetid: d83effc7-437d-42e9-8ac3-b65f79e27043
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50cd0b4e2336b20ab12b8c5e6fda6615af03abd5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722686"
---
# <a name="deployment-of-data-mining-solutions"></a>部署資料採礦方案
  資料採礦程序的最後一個步驟就是將模型部署到實際執行環境。 部署作業非常重要，因為可將模型提供給使用者，好讓您可以執行以下任何工作：  
  
-   使用模型來建立預測，並做出商業決策。 如需工具的資訊可用來建立查詢，請參閱 <<c0> [ 資料採礦查詢介面](data-mining-query-tools.md)。  
  
-   直接將資料採礦功能內嵌於應用程式中。 您可以包括分析管理物件 (AMO) 或含有一組物件的組件，讓應用程式用來建立、改變、處理以及刪除採礦結構和採礦模型。  
  
-   建立報表，好讓使用者要求預測、檢視趨勢或比較模型。  
  
 本節提供有關部署選項的詳細資訊。  
  
 [部署資料採礦方案的需求](#bkmk_Reqs)  
  
 [部署關聯式方案](#bkmk_RelationalSltn)  
  
 [部署多維度方案](#bkmk_MDSltn)  
  
 [相關資源](#bkmk_Resources)  
  
## <a name="in-this-section"></a>本節內容  
 [將資料採礦方案部署到舊版的 SQL Server](deploy-a-data-mining-solution-to-previous-versions-of-sql-server.md)  
  
 [匯出及匯入資料採礦物件](export-and-import-data-mining-objects.md)  
  
##  <a name="bkmk_Reqs"></a> 部署資料採礦方案的需求  
 部署方案的目標 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體必須在支援多維度物件和資料採礦物件的模式下執行；也就是說，您不能將資料採礦物件部署到裝載表格式模型或 PowerPivot 資料的執行個體。  
  
 因此，當您在 Visual Studio 中建立資料採礦方案時，請務必使用 [Analysis Services 多維度和資料採礦專案] 範本。  
  
 當您部署方案時，用於資料採礦的物件會在指定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體中建立 (位於與方案檔同名的資料庫中)。  
  
###  <a name="bkmk_RelationalSltn"></a> 部署關聯式方案  
 當您部署關聯式資料採礦方案時，將會在新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中建立必要的資料採礦物件，而且預設會處理這些物件。 您可以使用 [處理選項] 組態屬性來變更處理選項。 如需詳細資訊，請參閱[設定 Analysis Services 專案屬性 &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md)。  
  
 根據預設，每次只會部署累加變更。 換句話說，您可以修改採礦模型，而且當您重新部署專案時，只會更新該採礦模型。 但是，如果您有多個用戶端正在編輯 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，這可能會導致錯誤發生。 若要變更預設部署模式，好讓您部署方案時重新整理整個資料庫，請變更 [部署模式] 屬性  
  
 在關聯式資料採礦方案中，必須部署的物件只有資料來源定義、任何已使用的資料來源檢視、採礦結構，以及所有相依的採礦模型。  
  
###  <a name="bkmk_MDSltn"></a> 部署多維度方案  
 當您部署多維度資料採礦方案時，這個方案會在與來源 Cube 相同的資料庫中建立您的資料採礦物件。  
  
 當您處理採礦結構或採礦模型時，您也必須處理來源 Cube。 因此，部署使用 OLAP 採礦模型的方案比起關聯式資料採礦方案需要更長的時間。  
  
 通常資料採礦物件也會使用 Cube 所使用的相同資料來源和資料來源檢視。 但是，您可以加入專門以資料採礦為目標的資料來源和資料來源檢視。 例如，通常 Cube 不會包含有關潛在客戶的資料或是多維度物件中未使用的外部資料。  
  
##  <a name="bkmk_Resources"></a> 相關資源  
 [移動資料採礦物件](moving-data-mining-objects.md)  
  
 如果您的模型只以關聯式資料為根據，則使用 DMX 匯出和匯入物件是最方便的移動模型方式。  
  
 [移動 Analysis Services 資料庫](../multidimensional-models/move-an-analysis-services-database.md)  
  
 當模型使用 Cube 當做資料來源時，請參考本主題，以取得有關如何移動模型及其支援 Cube 資料的詳細資訊。  
  
 [部署 Analysis Services 專案 &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
 提供有關 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署的一般資訊，並描述可當作專案組態之一部分設定的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型物件處理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [資料採礦查詢介面](data-mining-query-tools.md)   
 [處理需求和考量 (資料採礦)](processing-requirements-and-considerations-data-mining.md)  
  
  
