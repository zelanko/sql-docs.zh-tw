---
title: "Integration Services 轉換 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transformations [Integration Services], listed
- transformations [Integration Services], types
- transformations [Integration Services]
- data flow [Integration Services], transformations
- business intelligence transformations [Integration Services]
- join transformations
- split transformations [Integration Services]
- custom transformations [Integration Services]
- row transformations [Integration Services]
- rowset transformations [Integration Services]
ms.assetid: c70c4f6e-82dd-4948-b923-fd5193f67f7e
caps.latest.revision: "56"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3e4ed1c7f0497f8be036b258f35d7a003db00d1f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-transformations"></a>Integration Services 轉換
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 轉換是封裝之資料流程中的元件，用以彙總、合併、散發和修改資料。 轉換還可以執行查閱作業，並產生範例資料集。 此章節描述 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 所包含的轉換，並解釋其運作方式。  
  
## <a name="business-intelligence-transformations"></a>商業智慧轉換  
 下列轉換會執行商業智慧作業 (例如，清除資料、採礦文字及執行資料採礦預測查詢)。  
  
|轉換|說明|  
|--------------------|-----------------|  
|[緩時變維度轉換](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)|設定緩時變維度之更新的轉換。|  
|[模糊群組轉換](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)|用於標準化資料行資料中值的轉換。|  
|[模糊查閱轉換](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)|在參考資料表中使用模糊比對查閱值的轉換。|  
|[詞彙擷取轉換](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)|從文字擷取詞彙的轉換。|  
|[詞彙查閱轉換](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)|在參考資料表中查閱詞彙，並計數從文字擷取之詞彙的轉換。|  
|[資料採礦查詢轉換](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|執行資料採礦預測查詢的轉換。|  
|[DQS 清理轉換](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)|透過套用針對資料來源所建立之規則來更正來自已連接資料來源之資料的轉換。|  
  
## <a name="row-transformations"></a>資料列轉換  
 下列轉換會更新資料行的值，並建立新的資料行。 轉換會套用至轉換輸入中的每個資料列。  
  
|轉換|說明|  
|--------------------|-----------------|  
|[字元對應轉換](../../../integration-services/data-flow/transformations/character-map-transformation.md)|將字串函數套用至字元資料的轉換。|  
|[複製資料行轉換](../../../integration-services/data-flow/transformations/copy-column-transformation.md)|將輸入資料行的副本加入轉換輸出的轉換。|  
|[資料轉換](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)|將資料行的資料類型轉換成其他資料類型的轉換。|  
|[衍生的資料行轉換](../../../integration-services/data-flow/transformations/derived-column-transformation.md)|以運算式的結果擴展資料行的轉換。|  
|[匯出資料行轉換](../../../integration-services/data-flow/transformations/export-column-transformation.md)|將資料流程中的資料插入檔案的轉換。|  
|[匯入資料行轉換](../../../integration-services/data-flow/transformations/import-column-transformation.md)|從檔案讀取資料，並將其加入資料流程的轉換。|  
|[指令碼元件](../../../integration-services/data-flow/transformations/script-component.md)|使用指令碼擷取、轉換或載入資料的轉換。|  
|[OLE DB 命令轉換](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)|針對資料流程中的每個資料列執行 SQL 命令的轉換。|  
  
## <a name="rowset-transformations"></a>資料列集轉換  
 下列轉換會建立新的資料列集。 資料列集可以包括彙總和排序的值、範例資料列集，或樞紐和取消樞紐的資料列集。  
  
|轉換|說明|  
|--------------------|-----------------|  
|[彙總轉換](../../../integration-services/data-flow/transformations/aggregate-transformation.md)|執行彙總 (例如 AVERAGE、SUM 及 COUNT) 的轉換。|  
|[排序轉換](../../../integration-services/data-flow/transformations/sort-transformation.md)|排序資料的轉換。|  
|[百分比取樣轉換](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)|透過使用百分比指定範例大小來建立範例資料集的轉換。|  
|[資料列取樣轉換](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)|透過指定範例中的資料列數目來建立範例資料集的轉換。|  
|[樞紐轉換](../../../integration-services/data-flow/transformations/pivot-transformation.md)|為正規化資料表建立一個較不正規化版本的轉換。|  
|[取消樞紐轉換](../../../integration-services/data-flow/transformations/unpivot-transformation.md)|為非正規化資料表建立一個較正規化版本的轉換。|  
  
## <a name="split-and-join-transformations"></a>分割和聯結轉換  
 下列轉換會將資料列散發至不同的輸出、建立轉換輸入的副本、將多個輸入聯結到一個輸出中，並執行查閱作業。  
  
|轉換|說明|  
|--------------------|-----------------|  
|[條件式分割轉換](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)|將資料列傳送至不同輸出的轉換。|  
|[多點傳送轉換](../../../integration-services/data-flow/transformations/multicast-transformation.md)|將資料集散發至多個輸出的轉換。|  
|[聯集全部轉換](../../../integration-services/data-flow/transformations/union-all-transformation.md)|合併多個資料集的轉換。|  
|[合併轉換](../../../integration-services/data-flow/transformations/merge-transformation.md)|合併兩個已排序資料集的轉換。|  
|[合併聯結轉換](../../../integration-services/data-flow/transformations/merge-join-transformation.md)|使用 FULL、LEFT 或 INNER 聯結來聯結兩個資料集的轉換。|  
|[查閱轉換](../../../integration-services/data-flow/transformations/lookup-transformation.md)|在參考資料表中使用完全比對查閱值的轉換。|  
|[快取轉換](../../../integration-services/data-flow/transformations/cache-transform.md)|將資料流程中已連接資料來源的資料寫入快取連接管理員以便將資料寫入快取檔案的轉換。 「查閱」轉換會在快取檔案的資料上執行查閱。|  
|[平衡資料分佈器轉換](../../../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md)|轉換會將傳入資料列的緩衝區一致地分佈到個別執行緒上的輸出，以提升在多核心和多處理器伺服器上執行之 SSIS 封裝的效能。|  
  
## <a name="auditing-transformations"></a>稽核轉換  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括下列轉換，用以稽核資訊與計數資料列。  
  
|轉換|說明|  
|--------------------|-----------------|  
|[稽核轉換](../../../integration-services/data-flow/transformations/audit-transformation.md)|使環境之相關資訊可用於封裝中資料流程的轉換。|  
|[資料列計數轉換](../../../integration-services/data-flow/transformations/row-count-transformation.md)|資料列通過資料流程時計算其數目，並將最後計數儲存到變數中的轉換。|  
  
## <a name="custom-transformations"></a>自訂轉換  
 您也可以撰寫自訂轉換。 如需詳細資訊，請參閱 [開發具有同步輸出的自訂轉換元件](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) 和 [開發具有非同步輸出的自訂轉換元件](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)。  
  
  
