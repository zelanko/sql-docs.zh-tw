---
title: 資料採礦查詢工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytask.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7cd5890df8ddc080aaa3e647c77b3c09d8d35216
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832597"
---
# <a name="data-mining-query-task"></a>資料採礦查詢工作
  「資料採礦查詢」工作會根據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]內建的資料採礦模型執行預測查詢。 預測查詢會使用採礦模型建立新資料的預測。 例如，預測查詢可預測夏季各月間可能出售的帆船數目，或產生可能購買帆船的預期客戶清單。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 亦提供執行其他商業智慧作業的工作，例如執行「資料定義語言」(DDL) 陳述式和處理分析物件。  
  
 如需其他商業智慧工作的詳細資訊，請按下列其中一個主題：  
  
-   [Analysis Services 執行 DDL 工作](analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 處理工作](analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>預測查詢  
 查詢為「資料採礦延伸模組」(DMX) 陳述式。 DMX 語言為 SQL 語言的擴充模組，能提供使用採礦模型的支援。 如需如何使用 DMX 語言的詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 參考](/sql/dmx/data-mining-extensions-dmx-reference)。  
  
 此工作可查詢相同採礦結構上建立的多個採礦模型。 採礦模型是使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供的其中一種資料採礦演算法建立。 「資料採礦查詢」工作參考的採礦結構，可包含多個使用不同演算法建立的採礦模型。 如需詳細資訊，請參閱[採礦結構 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md) 和[資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
 「資料採礦查詢」工作執行的預測查詢會傳回單一資料列或資料集的結果。 傳回單一資料列的查詢稱為單一查詢：例如，預測夏季各月間將售出之帆船數的查詢會傳回數字。 如需有關預測查詢來傳回單一資料列的詳細資訊，請參閱[資料採礦查詢介面](../../analysis-services/data-mining/data-mining-query-tools.md)。  
  
 查詢結果會儲存到資料表。 如果「資料採礦查詢」工作指定的資料表名稱已存在，則工作可使用相同的名稱附加一個號碼建立新的資料表，或者覆寫資料表內容。  
  
 如果結果包含巢狀，則會在儲存之前扁平化結果。 扁平化結果會將巢狀結果集變更成資料表。 例如，扁平化含有 **Customer** 資料行和巢狀 **Product** 資料行的巢狀結果，會將資料列加入至 **Customer** 資料行，以製作包含各客戶之產品資料的資料表。 例如，擁有三種不同產品的客戶會變成擁有三個資料列的資料表，各資料列中會重複該客戶並包含不同的產品。 如果省略 FLATTENED 關鍵字，則資料表只會包含 **Customer** 資料行，且每個客戶只有一個資料列。 如需詳細資訊，請參閱 [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx)。  
  
## <a name="configuration-of-the-data-mining-query-task"></a>設定資料採礦查詢工作  
 「資料採礦查詢」工作需要兩個連接。 第一個連接是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接管理員，會連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，或含有採礦結構和採礦模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 第二個連接是 OLE DB 連接管理員，會連接到含有工作所寫入資料表的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md) 及 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [資料採礦查詢工作編輯器 &#40;採礦模型索引標籤&#41;](../data-mining-query-task-editor-mining-model-tab.md)  
  
-   [資料採礦查詢工作編輯器 &#40;查詢索引標籤&#41;](../data-mining-query-task-editor-query-tab.md)  
  
-   [資料採礦查詢工作編輯器 &#40;輸出索引標籤&#41;](../data-mining-query-task-editor-output-tab.md)  
  
> [!NOTE]  
>  「資料採礦查詢編輯器」沒有「運算式」頁面， 而是另外使用 **[屬性]** 視窗存取用來建立和管理「資料採礦查詢」工作屬性之屬性運算式的工具。  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>以程式設計方式設定資料採礦查詢工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列其中一個主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
  
