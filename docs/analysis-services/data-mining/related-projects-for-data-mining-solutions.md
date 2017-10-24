---
title: "資料採礦方案的相關專案 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dc26489a-4c27-4b89-8215-6d245427c350
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 290142e362b4e41148ab2042c8c76738f3e7b54c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="related-projects-for-data-mining-solutions"></a>資料採礦方案的相關專案
  資料採礦方案至少需要資料採礦專案，專案中會定義資料來源、資料來源檢視、採礦結構和採礦模型。 但是，當使用資料採礦模型進行每日決策時，資料採礦一定要與預測性分析方案的其他部分整合，該方案可包含這些程序和元件：  
  
-   準備及選取資料和變數。 包括資料清理、中繼資料管理及整合多個資料來源，以及將資料轉換、合併和上傳到資料倉儲中。  
  
-   報告分析、呈現預測及稽核/追蹤資料採礦活動。  
  
-   使用多維度模型或表格式模型來探索各種發現。  
  
-   調整資料採礦方案來支援新的資料，或是目前分析所驅使之支援基礎結構的變更。  
  
 本主題描述 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的其他功能 (這些通常是預測性分析方案的一部分)，以便支援資料準備和資料採礦的處理，或是藉由提供分析和動作工具來支援使用者。  
  
 [Integration Services](#bkmk_SSIS)  
  
 [Reporting Services](#bkmk_SSRS)  
  
 [Data Quality Service](#bkmk_DQSetc)  
  
 [全文檢索搜尋](#bkmk_FTSetc)  
  
 [語意索引](#bkmk_SemSearch)  
  
##  <a name="bkmk_SSIS"></a> SQL Server Integration Services  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了資料準備和資料採礦專案定型階段所需的元件與功能。 雖然您可以使用類似指令碼的其他工具來執行許多資料清理或準備工作，但是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 擁有許多資料採礦的優點：  
  
-   將工作表示為工作流程的一部分，工作流程可以重複、自動化、建立分支及擴充。  
  
-   提供稽核的擴充支援以及擷取錯誤和記錄事件的多個方式。  
  
     除了擷取資料歷程之外，您也可以監視整個資料轉換管線中的資料變更。  
  
     您也可以將 SSIS 工作流程與支援 SQL Server 異動資料擷取功能的功能整合。  
  
-   資料採礦可以併入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作流程，以智慧的方式將內送資料分成多個資料表。 例如，您可能會使用預測查詢將新的客戶分成不同的群組，以便在郵寄促銷活動中鎖定目標客戶。  
  
 下列清單提供為了支援資料採礦所最常使用之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件的連結。  
  
 **控制流程元件**  
  
-   [Analysis Services 執行 DDL 工作](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 處理工作](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [CDC 控制工作](../../integration-services/control-flow/cdc-control-task.md)  
  
-   [資料清理](../../data-quality-services/data-cleansing.md)  
  
-   [資料採礦查詢工作](../../integration-services/control-flow/data-mining-query-task.md)  
  
-   [資料分析工作](../../integration-services/control-flow/data-profiling-task.md)  
  
 **資料流程元件**  
  
-   [CDC 流程元件](../../integration-services/data-flow/cdc-flow-components.md)  
  
-   [條件式分割轉換](../../integration-services/data-flow/transformations/conditional-split-transformation.md)  
  
-   [資料轉換](../../integration-services/data-flow/transformations/data-conversion-transformation.md)  
  
-   [資料採礦模型定型目的地](../../integration-services/data-flow/data-mining-model-training-destination.md)  
  
-   [資料採礦查詢轉換](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)  
  
-   [衍生的資料行轉換](../../integration-services/data-flow/transformations/derived-column-transformation.md)  
  
-   [百分比取樣轉換](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
-   [詞彙擷取轉換](../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
-   [詞彙查閱轉換](../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
##  <a name="bkmk_SSRS"></a> SQL Server Reporting Services  
 雖然 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 通常不會被視為資料採礦方案的重要元件，但是它會提供對於呈現資料採礦方案非常實用的以下功能。  
  
-   在複雜的報表中整合多個來源的資料。 針對模型內容來為分析師建立查詢，並為使用者建立報表，報表中會顯示預測和趨勢。  
  
-   建立報表的功能，該報表可讓使用者直接針對現有採礦模型進行查詢。  
  
-   與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]整合，以便支援鑽研和瀏覽資料採礦維度及從 OLAP 模型建立而來的資料採礦 Cube。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中所提供的參數化和格式化功能。  
  
 如需有關如何搭配資料來源形式的 DMX 查詢使用 Reporting Services 的詳細資訊，請參閱以下連結：  
  
 [從資料採礦模型擷取資料 &#40;DMX&#41; &#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)  
  
 [Analysis Services DMX 查詢設計工具使用者介面](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
 [Analysis Services Connection Type for DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)  
  
 但是，使用 DMX 當做資料來源並不是必要的。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的資料採礦元件也支援將預測查詢結果儲存到關聯式資料庫。 如果您已經使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]建立更新模型的工作流程，則將預測和其他資料採礦查詢結果保存到 SQL Server 可讓您啟用報告用的 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 以及不與 DMX 接觸的其他工具。  
  
 如需有關使用 Reporting Services 當做資料來源展示層的詳細資訊，請參閱＜ [Integrating Reporting Services into Applications](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)＞。  
  
##  <a name="bkmk_DQSetc"></a> Data Quality Services  
 Data Quality Services (DQS) 是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的新功能。 因為資料問題可能會讓資料採礦無法進行，所以執行重複分析或是在大型組織處理複雜資料來源的資料採礦人員應該會發現，使用 DQS 的規劃完善資料專案比起使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他指令碼隨選清理資料，為支援資料採礦的一個更可靠的方案。  
  
 資料採礦方案中的資料準備與資料完整性中，應該考量下列 DQS 功能。  
  
 **電腦輔助的資料清理程序，可分析來源資料及建議變更。**  
 DQS 可以將來源資料與資料品質提供者所維護和保證的雲端架構參考資料做比較。  
  
 DQS 可以分析原始來源資料，並從使用者資料建立知識庫。 處理過的資料會加以分類，然後顯示給使用者以供進一步處理。 清理程序為互動式，這表示資料監管可以核准、拒絕或修改電腦輔助的資料清理程序所提議的資料。  
  
 此程序的結果為知識庫，您可以在多個資料增強階段持續改良或重複使用此知識庫。  
  
 如需詳細資訊，請參閱 [Data Cleansing](../../data-quality-services/data-cleansing.md)。  
  
 **電腦輔助的比對程序，可分析來源資料及建議變更。**  
 為了避免資料重複，您可以執行資料來源的額外清理，以識別完全相符和大致相符的項目。 這些元件可讓您指定比對規則以及套用規則的臨界值。  
  
 您可以藉由尋找資料相符項目來移除重複項目，因為重複項目可能會讓資料採礦發生問題。 刪除重複資料作業不會自動進行；資料監管或 IT 專業人員必須驗證知識庫中的知識以及要進行的資料變更。  
  
 在您建立初始 DQS 專案之後，您可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件將許多工作自動化。  
  
 如需詳細資訊，請參閱 [Data Matching](../../data-quality-services/data-matching.md)。  
  
 在資料品質專案中執行清理和比對活動之後，您可以得到有關 DQS 正在處理之資料的即時統計資料和資訊。 資料分析會幫助您評估資料清理或比對提升資料品質的程度，並幫助您了解所做的變更。 如需有關資料分析和通知的詳細資訊，請參閱＜ [Data Profiling and Notifications in DQS](../../data-quality-services/data-profiling-and-notifications-in-dqs.md)＞。  
  
 **代表三種知識類型的知識庫：現成的知識、DQS 伺服器產生的知識，以及使用者產生的知識。**  
 一旦您建立知識庫之後，就可以反覆使用它來清理和驗證其他資料。  
  
 您可以從多個來源將新的資料匯入知識庫資料中，資料可以是參考提供者的乾淨資料，或是與知識庫中現有資料符合的原始資料。  
  
 如需有關資料品質專案中清理活動的詳細資訊，請參閱＜資料清理 (DQS)＞。  
  
 您也可以將知識庫中的知識套用到其他來源，在其他程序中執行資料清理。 這類資料清理有助於識別使用者輸入錯誤、傳輸或儲存中的損毀，或是不符的資料字典定義。  
  
 如需詳細資訊，請參閱 [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
##  <a name="bkmk_FTSetc"></a> 全文檢索搜尋  
 SQL Server 中的全文檢索搜尋可讓應用程式和使用者針對 SQL Server 資料表中以字元為主的資料，執行全文檢索查詢。 當啟用全文檢索搜尋時，您可以針對文字資料執行搜尋，該搜尋是以有關多形式單字或片語的語言特有規則來增強功能。 您也可以設定搜尋條件 (例如多個詞彙之間的距離)，並使用函數來限制依可能性順序傳回的結果。  
  
 因為全文檢索查詢是 SQL Server 引擎提供的功能，所以您可以建立參數化查詢、使用文字資料來源上的全文檢索搜尋功能來產生自訂資料集或詞彙向量，並在資料採礦中使用這些來源。  
  
 如需全文檢索查詢如何與全文檢索索引互動的詳細資訊，請參閱 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)。  
  
 使用 SQL Server 全文檢索搜尋功能的優點就是可以利用所有 SQL Server 語言隨附之斷詞工具和字幹分析器中所包含的語言智慧。 藉由使用隨附的斷詞工具和字幹分析器，可確保使用適合每種語言的字元來分隔字詞，而且不會忽略以讀音符號或拼字變化為根據的同義字 (例如日文中的多種數字格式)。  
  
 除了控制字詞界限的語言智慧以外，每一個語言的字幹分析器都會根據該語言中的詞形變化和拼字變化規則知識，將字詞的變化減少成單一詞彙。 每一種語言的語言分析規則都不一樣，而且會根據實際生活語料庫的大規模研究而發展。  
  
 如需詳細資訊，請參閱 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
 儲存在全文檢索索引之後的字詞版本為壓縮形式的語彙基元。 全文檢索索引後續的查詢會根據該語言的規則產生特定字詞的多個變化形式，以確保能產生所有可能的相符項目。 例如，雖然儲存的語彙基元可能是 “run”，但是查詢引擎也會尋找 "running"、"ran" 和 "runner" 等詞彙，因為這些是根單字 "run" 所正常衍生的形態變化。  
  
 您也可以建立及產生使用者同義字，以便儲存同義字並啟用更好的搜尋結果或分類詞彙。 透過開發符合全文檢索資料的同義字，您可以有效地擴大針對該資料進行全文檢索查詢的範圍。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的同義字檔案](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)。  
  
 使用全文檢索搜尋的需求如下：  
  
-   資料庫管理員必須在資料表上建立全文檢索索引。  
  
-   每個資料表只允許有一個全文檢索索引。  
  
-   您編制索引的每一個資料行必須有唯一的索引鍵。  
  
-   只有以下資料類型的資料行才支援全文檢索索引：char、varchar、nchar、nvarchar、text、ntext、image、xml、varbinary 和 varbinary(max)。 如果資料行為 varbinary、varbinary(max)、image 或 xml，您必須在個別類型資料行中指定可建立索引之文件的副檔名 (.doc、.pdf、.xls 等)。  
  
##  <a name="bkmk_SemSearch"></a> 語意索引  
 語意搜尋會根據 SQL Server 中的現有全文檢索搜尋功能而建立，但是會使用其他功能和統計資料來啟用類似自動關鍵字擷取及探索相關文件等案例。 例如，您可能會使用語意搜尋來為組織建立基本分類，或是分類某個語料的文件。 或者，您可能會使用群集或決策樹模型中擷取之詞彙和文件相似度分數的組合。  
  
 在您成功啟用語意搜尋並將資料行編制索引之後，您可以使用語意索引原本所提供的功能執行以下作業：  
  
-   傳回單一字詞關鍵片語以及其分數。  
  
-   傳回包含指定之關鍵片語的文件。  
  
-   傳回相似度分數以及對分數有貢獻的詞彙。  
  
 如需詳細資訊，請參閱 [使用語意搜尋找到文件中的主要片語](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) 和 [使用語意搜尋尋找相似及相關的文件](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)。  
  
 如需支援語意索引之資料庫物件的詳細資訊，請參閱 [在資料表和資料行上啟用語意搜尋](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)。  
  
 使用語意搜尋的需求如下：  
  
-   也必須啟用全文檢索搜尋。  
  
-   安裝語意搜尋元件也會建立特殊系統資料庫，該資料庫無法重新命名、更改或取代。  
  
-   您使用此服務編制索引的文件必須在 SQL Server 中，儲存為全文檢索索引所支援的任何資料庫物件，包括資料表和索引檢視表。  
  
-   並非所有全文檢索語言都支援語意索引。 如需受支援語言的清單，請參閱 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型方案 &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [表格式模型方案 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)  
  
  

