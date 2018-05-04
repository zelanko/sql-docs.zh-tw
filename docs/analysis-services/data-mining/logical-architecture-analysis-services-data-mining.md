---
title: 邏輯架構 (Analysis Services-資料採礦) |Microsoft 文件
ms.custom: ''
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], about mining structures
- logical architecture [Data Mining]
- architecture [Analysis Services], mining models
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: 4e0cbf46-cc60-4e91-a292-9a69f29746f0
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2ff8521531c470ed485e20b71d1d0b0dbfbbd9a2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="logical-architecture-analysis-services---data-mining"></a>邏輯架構 (Analysis Services – 資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  資料採礦是涉及多個元件互動的程序。  
  
-   您可以存取 SQL Server 資料庫或任何其他資料來源中的資料來源，以供定型、測試或預測使用。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 Visual Studio 可用來定義資料採礦結構和模型。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]則可用來管理資料採礦物件及建立預測和查詢。  
  
-   當此方案完成時，可將其部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的執行個體。  
  
 其他地方已經描述建立這些方案物件的程序。 如需詳細資訊，請參閱 [資料採礦方案](../../analysis-services/data-mining/data-mining-solutions.md)。  
  
 下列章節描述資料採礦方案中物件的邏輯架構。  
  
 [資料採礦來源資料](#bkmk_SourceData)  
  
 [採礦結構](#bkmk_Structures)  
  
 [採礦模型](#bkmk_Models)  
  
 [自訂資料採礦物件](#bkmk_CustomObjects)  
  
##  <a name="bkmk_SourceData"></a> 資料採礦來源資料  
 資料採礦方案中不會儲存用於資料採礦的資料，而只會儲存繫結。 資料可能位於以舊版的 SQL Server 所建立的資料庫、CRM 系統或甚至一般檔案中。 當您以處理方式來定型結構或模型時，便會建立資料的統計摘要，並將其儲存在快取中，該快取可以保留供之後的作業使用，或是在處理之後加以刪除。 如需詳細資訊，請參閱[採礦結構 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 您會結合 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源檢視 (DSV) 物件中的不同資料，這樣會在資料來源頂端提供抽象層。 您可以在資料表之間指定聯結，或是加入具有多對一關聯性的資料表，以建立巢狀資料表資料行。 這些物件的定義、資料來源和資料來源檢視會儲存在方案內，而且副檔名為 *.ds 和 \*.dsv。 如需建立及使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源和資料來源檢視的詳細資訊，請參閱[支援的資料來源 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)。  
  
 您也可以使用 AMO 或 XMLA 來定義及更改資料來源和資料來源檢視。 如需如何以程式設計方式處理這些物件的詳細資訊，請參閱[邏輯架構概觀 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)。  
  
  
##  <a name="bkmk_Structures"></a> Mining Structures  
 資料採礦結構是定義資料網域 (從中建立採礦模型) 的邏輯資料容器。 單一採礦結構可以支援多個採礦模型。  
  
 當您需要使用資料採礦方案中的資料時，Analysis Services 會從來源讀取資料，並產生彙總與其他資訊的快取。 預設會保存此快取，以便重複使用定型資料來支援其他模型。 如果您需要刪除快取，請將採礦結構物件上的 **CacheMode** 屬性變更為 **ClearAfterProcessing**值。 如需詳細資訊，請參閱 [AMO 資料採礦類別](../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)。  
  
 Analysis Services 也提供將資料分成定型集和測試資料集，以便您可以測試一組代表性、 隨機選取的資料採礦模型的能力。 資料實際上並不會分開儲存，而是以某個屬性來標示結構快取中的案例資料，該屬性指出特定案例是否用於定型或測試。 如果快取遭到刪除，就無法擷取該資訊。  
  
 如需詳細資訊，請參閱[採礦結構 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 資料採礦結構可以包含巢狀資料表。 巢狀資料表會提供有關主要資料表中模型化之案例的詳細資料。 如需詳細資訊，請參閱[巢狀資料表 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  
##  <a name="bkmk_Models"></a> Mining Models  
 在處理之前，資料採礦模型只是中繼資料屬性的組合。 這些屬性會指定採礦結構、指定資料採礦演算法，以及定義對資料處理方法造成影響之參數和篩選設定的集合。 如需詳細資訊，請參閱[採礦模型 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)。  
  
 當您處理模型時，儲存在採礦結構快取中的定型資料會用來產生模式 (根據資料的統計屬性以及演算法和其參數所定義的啟發學習法)。 這就是所謂的「定型」模型。  
  
 定型的結果是包含在「模型內容」中的一組摘要資料，可描述所找到的模式並提供產生預測所根據的規則。 如需詳細資訊，請參閱[採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
 在受限的案例中，模型的邏輯結構也可以匯出到檔案中，該檔案代表根據標準格式 (預測模型標記語言，PMML) 的模型公式與資料繫結。 這個邏輯結構可以匯入到利用 PMML 的其他系統中，然後這樣的模型可用來預測。 如需詳細資訊，請參閱 [了解 DMX Select 陳述式](../../dmx/understanding-the-dmx-select-statement.md)。  
  
  
##  <a name="bkmk_CustomObjects"></a> 自訂資料採礦物件  
 您在資料採礦專案內容中使用的其他物件 (例如精確度圖表或預測查詢) 不會保存在方案中，但是可以使用 ASSL 撰寫指令碼或使用 AMO 來建立。  
  
 此外，您也可以加入以下自訂物件來擴充 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上提供的服務和功能：  
  
 **自訂組件**  
 .NET 組件可以使用任何 CLR 或 COM 相容的語言來定義，然後向 SQL Server 執行個體註冊。 組件檔案會從應用程式定義的位置載入，而且會將複本連同資料儲存在伺服器中。 組件檔案的複本是用在每次啟動服務時載入組件。  
  
 如需詳細資訊，請參閱 [多維度模型組件管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)。  
  
 **自訂預存程序**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料採礦支援使用預存程序來處理資料採礦物件。 您可以建立自己的預存程序來擴充功能，並更輕鬆地處理預測查詢和內容查詢所傳回的資料。  
  
 [定義預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
 執行交叉驗證時支援使用下列預存程序。  
  
 [資料採礦預存程序 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)  
  
 此外， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也包含許多系統預存程序，可在內部用來進行資料採礦。 雖然系統預存程序供內部使用，但是您可能會發現這些是非常實用的捷徑。 Microsoft 保留視需要變更這些預存程序的權利；因此在實際使用上，我們建議您最好使用 DMX、AMO 或 XMLA 建立查詢。  
  
 **建立外掛程式演算法**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供一個機制來建立您自己的演算法，及將演算法當做新的資料採礦服務的伺服器執行個體。  
  
 Analysis Services 會使用 COM 介面與外掛程式演算法通訊。 若要深入了解如何實作新的演算法，請參閱 [外掛程式演算法](../../analysis-services/data-mining/plugin-algorithms.md)。  
  
 您必須先註冊每一個新的演算法，然後才能使用。 若要註冊演算法，請在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的 .ini 檔案中加入演算法的必要中繼資料。 您必須在您打算使用新演算法的每一個執行個體中加入該資訊。 在您加入演算法之後，您可以重新啟動執行個體，然後使用 MINING_SERVICES 結構描述資料列集來檢視新的演算法，包括演算法所支援的選項和提供者。  
  
  
## <a name="see-also"></a>另請參閱  
 [處理多維度模型 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [資料採礦延伸模組 & #40; DMX & #41;參考](../../dmx/data-mining-extensions-dmx-reference.md)  
  
  
