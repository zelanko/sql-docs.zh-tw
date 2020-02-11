---
title: 資料定義查詢（資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 49e02de1-4ffa-401c-8eee-471a9c25b86a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a67cadab4ee67bb3f81776ccb658c66fe6a67d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085155"
---
# <a name="data-definition-queries-data-mining"></a>資料定義查詢 (資料採礦)
  如果是資料採礦， *「資料定義查詢」* (Data Definition Query) 類別目錄表示執行以下作業的 DMX 陳述式或 XMLA 命令：  
  
-   建立、更改或操作資料採礦物件，例如模型。  
  
-   定義要用於定型或預測的資料來源。  
  
-   匯出或匯入採礦模型和採礦結構。  
  
 [建立資料定義查詢](#bkmk_Create)  
  
-   [SQL Server Data Tools 中的資料定義查詢](#bkmk_ssdt)  
  
-   [SQL Server Management Studio 中的資料定義查詢](#bkmk_SSMS)  
  
 [編寫資料定義語句的腳本](#bkmk_Scripts)  
  
 [編寫資料定義語句的腳本](#bkmk_Export)  
  
##  <a name="bkmk_Create"></a>建立資料定義查詢  
 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用預測查詢產生器或是在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用 DMX 查詢視窗來建立資料定義查詢 (陳述式)。 DMX 中的資料定義陳述式是 Analysis Services 資料定義語言 (DDL) 的一部分。  
  
 如需特定資料定義陳述式之語法的詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 參考](/sql/dmx/data-mining-extensions-dmx-reference)。  
  
###  <a name="bkmk_ssdt"></a>SQL Server Data Tools 中的資料定義查詢  
 資料採礦精靈是 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中用來執行以下操作的慣用工具：建立及修改採礦模型和採礦結構，以及定義用於預測查詢和定型的資料來源。  
  
 但是，如果您想要知道精靈傳送哪些陳述式到伺服器來建立資料結構或採礦模型，您可以使用 SQL Server Profiler 擷取資料定義陳述式。 如需詳細資訊，請參閱 [Use SQL Server Profiler to Monitor Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md)。  
  
 若要檢視用來定義定型或預測中所使用之資料來源的陳述式，您可以使用預測查詢產生器中的 **[SQL 檢視]** 。 有時候使用預測查詢產生器來建立用於定型和測試模型的基本查詢會很有用處，這樣可建立正確的語法。 然後您可以切換到 **[SQL 檢視]** 並手動編輯查詢。 如需詳細資訊，請參閱 [Manually Edit a Prediction Query](manually-edit-a-prediction-query.md)。  
  
###  <a name="bkmk_SSMS"></a>SQL Server Management Studio 中的資料定義查詢  
 如果是資料採礦物件，您可以使用資料定義查詢來執行以下動作：  
  
-   使用 [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx) 來建立特定類型的模型，例如叢集模型或決策樹模型。  
  
-   使用 [ALTER MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx)，藉由加入模型或變更資料行來更改現有的採礦結構。 請注意，您不能使用 DMX 更改採礦模型，您只能在現有的結構中加入新的模型。  
  
-   建立採礦模型的複本，然後使用 [SELECT INTO &#40;DMX&#41;](/sql/dmx/select-into-dmx) 加以更改。  
  
-   搭配資料來源查詢 (例如 OPENROWSET) 一起使用 [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)，以定義用於定型模型的資料集。  
  
 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供可幫助您建立資料定義查詢的查詢範本。 如需詳細資訊，請參閱 [在 SQL Server Management Studio 中使用 Analysis Services 範本](../instances/use-analysis-services-templates-in-sql-server-management-studio.md)。  
  
 一般來說， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中針對 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 所提供的範本只包含一般語法定義，您必須在 **[查詢]** 視窗中輸入或是使用為了輸入參數所提供的對話方塊來自訂這些語法定義。  
  
 如需如何使用此介面輸入參數的範例，請參閱 [根據範本建立單一預測查詢](create-a-singleton-prediction-query-from-a-template.md)。  
  
###  <a name="bkmk_Scripts"></a>編寫資料定義語句的腳本  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供多種指令碼和程式語言，您可以使用這些語言來建立或更改資料採礦物件或是定義資料來源。  雖然 DMX 是為了加速資料採礦工作所設計，您也可以在指令碼或自訂程式碼中同時使用 XMLA 和 AMO 來操作物件。  
  
 適用於 Excel 的資料採礦增益集也包含許多查詢範本，並提供 [進階查詢編輯器]****，此編輯器可幫助您撰寫複雜的 DMX 陳述式。 您可以互動方式建立查詢，然後切換到 [SQL 檢視] 來擷取 DMX 陳述式。  
  
##  <a name="bkmk_Export"></a>匯出和匯入模型  
 您可以在 DMX 中使用資料定義陳述式來匯出模型的定義以及其必要結構和資料來源，然後將該定義匯入至不同的伺服器。 使用匯出和匯入是在不同的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體之間移動資料採礦模型和採礦結構的最快速且最簡單的方法。 如需詳細資訊，請參閱[資料採礦解決方案和物件的管理](management-of-data-mining-solutions-and-objects.md)。  
  
> [!WARNING]  
>  如果您的模型是根據 Cube 資料來源中的資料，您不能使用 DMX 來匯出模型，而且應該改用備份和還原。  
  
##  <a name="bkmk_Tasks"></a> 相關工作  
 下表提供與資料定義查詢有關之工作的連結。  
  
|||  
|-|-|  
|處理 DMX 查詢的範本。|[在 SQL Server Management Studio 中使用 Analysis Services 範本](../instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|使用預測查詢產生器來設計所有種類的查詢。|[使用預測查詢產生器來建立預測查詢](create-a-prediction-query-using-the-prediction-query-builder.md)|  
|使用 SQL Server Profiler 來擷取查詢定義，並使用追蹤來監視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。|[Use SQL Server Profiler to Monitor Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md)|  
|深入了解針對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]所提供的指令碼語言和程式語言。|[XML for Analysis &#40;XMLA&#41; 參考](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)<br /><br /> [流量分析管理物件 &#40;AMO 進行開發&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|了解如何在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中管理模型。|[匯出及匯入資料採礦物件](export-and-import-data-mining-objects.md)<br /><br /> [匯出 &#40;DMX&#41;](/sql/dmx/export-dmx)<br /><br /> [匯入 &#40;DMX&#41;](/sql/dmx/import-dmx)|  
|深入了解 OPENROWSET 及查詢外部資料的其他方式。|[&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦嚮導 &#40;Analysis Services 資料採礦&#41;](data-mining-wizard-analysis-services-data-mining.md)  
  
  
