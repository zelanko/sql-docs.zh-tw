---
title: 資料採礦查詢工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytask.f1
- sql13.dts.designer.dmquerytask.miningmodel.f1
- sql13.dts.designer.dmquerytask.query.f1
- sql13.dts.designer.dmquerytask.output.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bf7fc37921ae37996b5d93b1ed1e913232a28b0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101576"
---
# <a name="data-mining-query-task"></a>資料採礦查詢工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「資料採礦查詢」工作會根據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]內建的資料採礦模型執行預測查詢。 預測查詢會使用採礦模型建立新資料的預測。 例如，預測查詢可預測夏季各月間可能出售的帆船數目，或產生可能購買帆船的預期客戶清單。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 亦提供執行其他商業智慧作業的工作，例如執行「資料定義語言」(DDL) 陳述式和處理分析物件。  
  
 如需其他商業智慧工作的詳細資訊，請按下列其中一個主題：  
  
-   [Analysis Services 執行 DDL 工作](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 處理工作](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>預測查詢  
 查詢為「資料採礦延伸模組」(DMX) 陳述式。 DMX 語言為 SQL 語言的擴充模組，能提供使用採礦模型的支援。 如需如何使用 DMX 語言的詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 參考](../../dmx/data-mining-extensions-dmx-reference.md)。  
  
 此工作可查詢相同採礦結構上建立的多個採礦模型。 採礦模型是使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供的其中一種資料採礦演算法建立。 「資料採礦查詢」工作參考的採礦結構，可包含多個使用不同演算法建立的採礦模型。 如需詳細資訊，請參閱[採礦結構 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md) 和[資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
 「資料採礦查詢」工作執行的預測查詢會傳回單一資料列或資料集的結果。 傳回單一資料列的查詢稱為單一查詢：例如，預測夏季各月間將售出之帆船數的查詢會傳回數字。 如需傳回單一資料列之預測查詢的詳細資料，請參閱 [資料採礦查詢工具](../../analysis-services/data-mining/data-mining-query-tools.md)。  
  
 查詢結果會儲存到資料表。 如果「資料採礦查詢」工作指定的資料表名稱已存在，則工作可使用相同的名稱附加一個號碼建立新的資料表，或者覆寫資料表內容。  
  
 如果結果包含巢狀，則會在儲存之前扁平化結果。 扁平化結果會將巢狀結果集變更成資料表。 例如，扁平化含有 **Customer** 資料行和巢狀 **Product** 資料行的巢狀結果，會將資料列加入至 **Customer** 資料行，以製作包含各客戶之產品資料的資料表。 例如，擁有三種不同產品的客戶會變成擁有三個資料列的資料表，各資料列中會重複該客戶並包含不同的產品。 如果省略 FLATTENED 關鍵字，則資料表只會包含 **Customer** 資料行，且每個客戶只有一個資料列。 如需詳細資訊，請參閱 [SELECT &#40;DMX&#41;](../../dmx/select-dmx.md)。  
  
## <a name="configuration-of-the-data-mining-query-task"></a>設定資料採礦查詢工作  
 「資料採礦查詢」工作需要兩個連接。 第一個連接是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接管理員，會連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，或含有採礦結構和採礦模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 第二個連接是 OLE DB 連接管理員，會連接到含有工作所寫入資料表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md) 及 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
> [!NOTE]  
>  「資料採礦查詢編輯器」沒有「運算式」頁面， 而是另外使用 **[屬性]** 視窗存取用來建立和管理「資料採礦查詢」工作屬性之屬性運算式的工具。  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>以程式設計方式設定資料採礦查詢工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列其中一個主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
## <a name="data-mining-query-task-editor-mining-model-tab"></a>資料採礦查詢工作編輯器 (採礦模型索引標籤)
  使用 **[資料採礦查詢工作]** 對話方塊的 **[採礦模型]** 索引標籤，即可指定要使用的採礦結構和採礦模型。  
  
 若要深入了解在封裝中實作資料採礦，請參閱 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md) (資料採礦查詢工作) 和 [Data Mining Solutions](../../analysis-services/data-mining/data-mining-solutions.md)(資料採礦方案)。  
  
### <a name="general-options"></a>一般選項  
 **名稱**  
 為資料採礦查詢工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入資料採礦查詢工作的描述。  
  
### <a name="mining-model-tab-options"></a>採礦模型索引標籤選項  
 **[連接]**  
 在清單中選取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員，或按一下 [新增]  以建立新的連線管理員。  
  
 **相關主題：** [Analysis Services 連線管理員](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **新增**  
 建立新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員。  
  
 **相關主題：** [加入 Analysis Services 連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **採礦結構**  
 從清單中選取採礦結構。  
  
 **採礦模型**  
 選取在所選取採礦結構上建立的採礦模型。  

## <a name="data-mining-query-task-editor-query-tab"></a>資料採礦查詢工作編輯器 (查詢索引標籤)
  使用 [資料採礦查詢工作]  對話方塊的 [查詢]  索引標籤，即可依據採礦模型建立預測查詢。 在此對話方塊中，您也可以將參數和結果集繫結到變數。  
  
 若要深入了解在封裝中實作資料採礦，請參閱 [資料採礦查詢工作](../../integration-services/control-flow/data-mining-query-task.md) 和 [資料採礦方案](../../analysis-services/data-mining/data-mining-solutions.md)。  
  
### <a name="general-options"></a>一般選項  
 **名稱**  
 為資料採礦查詢工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入資料採礦查詢工作的描述。  
  
### <a name="build-query-tab-options"></a>建立查詢索引標籤選項  
 **資料採礦查詢**  
 輸入資料採礦查詢。  
  
 **相關主題：** [資料採礦延伸模組 &#40;DMX&#41; 參考](../../dmx/data-mining-extensions-dmx-reference.md)  
  
 **建立新查詢**  
 使用圖形工具來建立資料採礦查詢。  
  
 **相關主題：** [資料採礦查詢](../../integration-services/control-flow/data-mining-query.md)  
  
### <a name="parameter-mapping-tab-options"></a>參數對應索引標籤選項  
 **參數名稱**  
 選擇性地更新參數名稱。 在 [變數名稱]  清單中選取變數，即可將參數對應至變數。  
  
 **變數名稱**  
 在清單中選取變數，以將其對應至參數。  
  
 **[加入]**  
 將參數加入清單中。  
  
 **移除**  
 選取參數，然後按一下 [移除]  。  
  
### <a name="result-set-tab-options"></a>結果集索引標籤選項  
 **結果名稱**  
 選擇性地更新結果集名稱。 在 [變數名稱]  清單中選取變數，即可將結果對應至變數。  
  
 按一下 [加入]  來加入結果之後，請為該結果提供唯一的名稱。  
  
 **變數名稱**  
 在清單中選取變數，以將其對應至結果集。  
  
 **結果類型**  
 指出傳回單一資料列或完整結果集。  
  
 **[加入]**  
 將結果集加入清單中。  
  
 **移除**  
 選取結果，然後按一下 [移除]  。  
## <a name="data-mining-query-task-editor-output-tab"></a>資料採礦查詢工作編輯器 (輸出索引標籤)
  使用 **[資料採礦查詢工作編輯器]** 對話方塊的 **[輸出]** 索引標籤，即可指定預測查詢的目的地。  
  
 若要深入了解在封裝中實作資料採礦，請參閱 [資料採礦查詢工作](../../integration-services/control-flow/data-mining-query-task.md) 和 [資料採礦方案](../../analysis-services/data-mining/data-mining-solutions.md)。  
  
### <a name="general-options"></a>一般選項  
 **名稱**  
 為資料採礦查詢工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入資料採礦查詢工作的描述。  
  
### <a name="output-tab-options"></a>輸出索引標籤選項  
 **[連接]**  
 在清單中選取連線管理員，或按一下 [新增]  來建立新的連線管理員。  
  
 **新增**  
 建立新的連接管理員。 只能使用 ADO.NET 和 OLE DB 連接管理員類型。  
  
 **輸出資料表**  
 指定供預測查詢撰寫其結果的資料表。  
  
 **卸除並重新建立輸出資料表**  
 指出預測查詢是否應藉由卸除然後重新建立資料表，來覆寫目的地資料表的內容。  
  
