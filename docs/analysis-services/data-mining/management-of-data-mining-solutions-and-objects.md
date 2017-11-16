---
title: "資料採礦方案與物件的管理 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], managing
- managing mining models
ms.assetid: 06fc61dd-925c-4347-8677-7046ee5d2f6f
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4154a0e542ed8e2bc6799dbc3f3c9ecb25ad5f4e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="management-of-data-mining-solutions-and-objects"></a>資料採礦方案與物件的管理
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供可用於管理現有採礦結構和採礦模型的用戶端工具。 本節說明可以利用每種環境執行的管理作業。  
  
 除了這些工具以外，您也可以透過下列方式來管理資料採礦物件：程式設計方式、使用 AMO，或使用其他連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的用戶端，例如適用於 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007 的資料採礦增益集。  
  
## <a name="in-this-section"></a>本章節內容  
 [移動資料採礦物件](../../analysis-services/data-mining/moving-data-mining-objects.md)  
  
 [處理需求和考量 &#40;資料採礦&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
 [使用 SQL Server Profiler 監視資料採礦 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/using-sql-server-profiler-to-monitor-data-mining-analysis-services-data-mining.md)  
  
## <a name="location-of-data-mining-objects"></a>資料採礦物件的位置  
 已經處理的採礦結構和模型會儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的執行個體中。  
  
 如果在開發資料採礦物件時，以 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [即時] **模式建立** 資料庫的連接，則您建立的任何物件就會在您作業時立即加入至伺服器。 不過，如果在 **[離線]** 模式 (也就是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中作業時的預設值) 中設計資料採礦物件，則您建立的採礦物件在部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的執行個體之前，都只是中繼資料容器。 因此，只要您對物件進行變更，就必須將物件重新部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 如需資料採礦架構的詳細資訊，請參閱[實體架構 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  有些用戶端 (例如適用於 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007 的資料採礦增益集) 也可讓您建立工作階段採礦模型和採礦結構，這些用戶端會使用執行個體的連接，但只會將採礦結構和模型儲存在工作階段持續時間的伺服器中。 您仍可以透過用戶端管理這些模型，方法與您管理儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的結構和模型相同，但是在您中斷與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的連接之後，並不會保存這些物件。  
  
## <a name="managing-data-mining-objects-in-sql-server-data-tools"></a>使用 SQL Server 資料工具管理資料採礦物件  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供一些功能，使資料採礦物件的建立、瀏覽和編輯都更為簡易。  
  
 以下連結提供有關如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]修改資料採礦物件的資訊：  
  
-   [編輯用於採礦結構的資料來源檢視](../../analysis-services/data-mining/edit-the-data-source-view-used-for-a-mining-structure.md)  
  
-   [變更採礦結構的屬性](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)  
  
-   [變更採礦模型的屬性](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)  
  
-   [檢視或變更模型旗標 &#40;資料採礦&#41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)  
  
-   [檢視或變更演算法參數](../../analysis-services/data-mining/view-or-change-algorithm-parameters.md)  
  
 通常，您將使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 當做開發新專案以及加入至現有專案的工具，然後管理已使用類似 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的工具進行部署的專案和物件。  
  
 但是，您可以直接修改已使用 **Immediate** 選項部署到 ssASnoversion 執行個體並且在線上模式下連接到伺服器的物件。 如需詳細資訊，請參閱 [在連線模式下連接至 Analysis Services 資料庫](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)。  
  
> [!WARNING]  
>  採礦結構或採礦模型的所有變更 (包括類似名稱或描述等中繼資料的變更) 都需要重新處理結構或模型。  
  
 如果您沒有用於建立資料採礦專案或物件的方案檔，您可使用 Analysis Services 匯入精靈從伺服器匯入現有的專案、修改物件，然後使用 **Incremental** 選項重新部署。 如需詳細資訊，請參閱 [使用 Analysis Services 匯入精靈匯入資料採礦專案](../../analysis-services/data-mining/import-a-data-mining-project-using-the-analysis-services-import-wizard.md)。  
  
## <a name="managing-data-mining-objects-in-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理資料採礦物件  
 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中撰寫指令碼、處理或刪除採礦結構及採礦模型。 您只能使用物件總管檢視有限的屬性集；不過，您可以藉由開啟 **[DMX 查詢]** 視窗並選取採礦結構，以檢視有關採礦模型的其他中繼資料。  
  
-   [在 SQL Server Management Studio 中建立 DMX 查詢](../../analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
## <a name="managing-data-mining-objects-programmatically"></a>以程式設計方式管理資料採礦物件  
 您可以使用下列程式語言，建立、改變、處理和刪除資料採礦物件。 每種語言是針對不同的工作所設計，因此，您可以執行的作業類型可能會有限制。 例如，資料採礦物件的某些屬性無法使用資料採礦延伸模組 (DMX) 變更，因此，您必須使用 XMLA 或 AMO。  
  
### <a name="analysis-management-objects-amo"></a>分析管理物件 (AMO)  
 分析管理物件 (AMO) 是根據 XMLA 所建立的物件模型，可讓您完全控制資料採礦物件。 您可以藉由使用 AMO 來建立、部署和監視採礦結構和採礦模型  
  
-   [AMO 概念和物件模型](../../analysis-services/multidimensional-models/analysis-management-objects/amo-concepts-and-object-model.md)  
  
-   <xref:Microsoft.AnalysisServices>  
  
 **限制** ：無。  
  
### <a name="data-mining-extensions-dmx"></a>資料採礦延伸模組 (DMX)  
 資料採礦延伸模組 (DMX) 可搭配其他的命令介面 (例如 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 或 ADOMD.Net) 來建立、刪除和查詢採礦結構和採礦模型。  
  
-   [資料採礦延伸模組 &#40;DMX&#41; 資料定義陳述式](../../dmx/dmx-statements-data-definition.md)  
  
 **限制** ：有些屬性無法使用 DMX 變更。  
  
### <a name="xml-for-analysis-xmla"></a>XML for Analysis (XMLA)  
 XML for Analysis (XMLA) 是適用於所有 Analysis Services 的資料定義語言。 XMLA 讓您能夠控制大多數的資料採礦物件和伺服器作業。 用戶端和伺服器之間的所有管理作業都可以使用 XMLA 執行。 為了便利起見，您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 來包裝 XML。  
  
 **限制** [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會產生一些僅支援內部使用而不能用於 XMLA DDL 指令碼的 XML 陳述式。  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services Developer 文件](../../analysis-services/analysis-services-developer-documentation.md)  
  
  

