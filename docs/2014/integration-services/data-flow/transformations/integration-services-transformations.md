---
title: Integration Services 轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76157486751a08d17cf46de312f63e6e41dc3cb1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52785230"
---
# <a name="integration-services-transformations"></a>Integration Services 轉換
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 轉換是封裝之資料流程中的元件，用以彙總、合併、散發和修改資料。 轉換還可以執行查閱作業，並產生範例資料集。 此章節描述 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 所包含的轉換，並解釋其運作方式。  
  
## <a name="business-intelligence-transformations"></a>商業智慧轉換  
 下列轉換會執行商業智慧作業 (例如，清除資料、採礦文字及執行資料採礦預測查詢)。  
  
|轉換|描述|  
|--------------------|-----------------|  
|[緩時變維度轉換](slowly-changing-dimension-transformation.md)|設定緩時變維度之更新的轉換。|  
|[模糊群組轉換](fuzzy-grouping-transformation.md)|用於標準化資料行資料中值的轉換。|  
|[模糊查閱轉換](lookup-transformation.md)|在參考資料表中使用模糊比對查閱值的轉換。|  
|[詞彙擷取轉換](term-extraction-transformation.md)|從文字擷取詞彙的轉換。|  
|[詞彙查閱轉換](term-lookup-transformation.md)|在參考資料表中查閱詞彙，並計數從文字擷取之詞彙的轉換。|  
|[資料採礦查詢轉換](data-mining-query-transformation.md)|執行資料採礦預測查詢的轉換。|  
|[DQS 清理轉換](dqs-cleansing-transformation.md)|透過套用針對資料來源所建立之規則來更正來自已連接資料來源之資料的轉換。|  
  
## <a name="row-transformations"></a>資料列轉換  
 下列轉換會更新資料行的值，並建立新的資料行。 轉換會套用至轉換輸入中的每個資料列。  
  
|轉換|描述|  
|--------------------|-----------------|  
|[字元對應轉換](character-map-transformation.md)|將字串函數套用至字元資料的轉換。|  
|[複製資料行轉換](copy-column-transformation.md)|將輸入資料行的副本加入轉換輸出的轉換。|  
|[資料轉換](data-conversion-transformation.md)|將資料行的資料類型轉換成其他資料類型的轉換。|  
|[衍生的資料行轉換](derived-column-transformation.md)|以運算式的結果擴展資料行的轉換。|  
|[匯出資料行轉換](export-column-transformation.md)|將資料流程中的資料插入檔案的轉換。|  
|[匯入資料行轉換](import-column-transformation.md)|從檔案讀取資料，並將其加入資料流程的轉換。|  
|[指令碼元件](script-component.md)|使用指令碼擷取、轉換或載入資料的轉換。|  
|[OLE DB 命令轉換](ole-db-command-transformation.md)|針對資料流程中的每個資料列執行 SQL 命令的轉換。|  
  
## <a name="rowset-transformations"></a>資料列集轉換  
 下列轉換會建立新的資料列集。 資料列集可以包括彙總和排序的值、範例資料列集，或樞紐和取消樞紐的資料列集。  
  
|轉換|描述|  
|--------------------|-----------------|  
|[彙總轉換](aggregate-transformation.md)|執行彙總 (例如 AVERAGE、SUM 及 COUNT) 的轉換。|  
|[排序轉換](sort-transformation.md)|排序資料的轉換。|  
|[百分比取樣轉換](percentage-sampling-transformation.md)|透過使用百分比指定範例大小來建立範例資料集的轉換。|  
|[資料列取樣轉換](row-sampling-transformation.md)|透過指定範例中的資料列數目來建立範例資料集的轉換。|  
|[樞紐轉換](pivot-transformation.md)|為正規化資料表建立一個較不正規化版本的轉換。|  
|[取消樞紐轉換](unpivot-transformation.md)|為非正規化資料表建立一個較正規化版本的轉換。|  
  
## <a name="split-and-join-transformations"></a>分割和聯結轉換  
 下列轉換會將資料列散發至不同的輸出、建立轉換輸入的副本、將多個輸入聯結到一個輸出中，並執行查閱作業。  
  
|轉換|描述|  
|--------------------|-----------------|  
|[條件式分割轉換](conditional-split-transformation.md)|將資料列傳送至不同輸出的轉換。|  
|[多點傳送轉換](multicast-transformation.md)|將資料集散發至多個輸出的轉換。|  
|[聯集全部轉換](union-all-transformation.md)|合併多個資料集的轉換。|  
|[合併轉換](merge-transformation.md)|合併兩個已排序資料集的轉換。|  
|[合併聯結轉換](merge-join-transformation.md)|使用 FULL、LEFT 或 INNER 聯結來聯結兩個資料集的轉換。|  
|[查閱轉換](lookup-transformation.md)|在參考資料表中使用完全比對查閱值的轉換。|  
|[快取轉換](cache-transform.md)|將資料流程中已連接資料來源的資料寫入快取連接管理員以便將資料寫入快取檔案的轉換。 「查閱」轉換會在快取檔案的資料上執行查閱。|  
|[平衡資料分佈器轉換](balanced-data-distributor-transformation.md)|轉換會將傳入資料列的緩衝區一致地分佈到個別執行緒上的輸出，以提升在多核心和多處理器伺服器上執行之 SSIS 封裝的效能。|  
  
## <a name="auditing-transformations"></a>稽核轉換  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括下列轉換，用以稽核資訊與計數資料列。  
  
|轉換|描述|  
|--------------------|-----------------|  
|[稽核轉換](audit-transformation.md)|使環境之相關資訊可用於封裝中資料流程的轉換。|  
|[資料列計數轉換](row-count-transformation.md)|資料列通過資料流程時計算其數目，並將最後計數儲存到變數中的轉換。|  
  
## <a name="custom-transformations"></a>自訂轉換  
 您也可以撰寫自訂轉換。 如需詳細資訊，請參閱 [開發具有同步輸出的自訂轉換元件](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) 和 [開發具有非同步輸出的自訂轉換元件](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)。  
  
  
