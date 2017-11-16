---
title: "資料採礦結構描述資料列集 (SSAs) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
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
- schema rowsets [Analysis Services], data mining
- data mining [Analysis Services], queries
- mining model content
- data mining [Analysis Services], schema rowsets
- schema rowsets [Analysis Services], retrieving
- data mining [Analysis Services], troubleshooting
ms.assetid: 442d8c29-07c7-45de-9a15-d556059f68d7
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: deaa583071c754683120c1c519232c3c2de6b0b7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-schema-rowsets-ssas"></a>資料採礦結構描述資料列集 (SSAS)
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，許多現有的 OLE DB 資料採礦結構描述資料列集已經公開成一組系統資料表，而且您可以使用資料採礦延伸模組 (DMX) 陳述式來查詢它們。 透過針對資料採礦結構描述資料列集建立查詢，您可以識別可用的服務、取得模型和結構之狀態的更新，以及找出模型內容或參數的相關詳細資料。 如需資料採礦結構描述資料列集的描述，請參閱＜ [Data Mining Schema Rowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)＞。  
  
> [!NOTE]  
>  您也可以使用 XMLA 來查詢資料採礦結構描述資料列集。 如需如何在 SQL Server Management Studio 中執行此動作的詳細資訊，請參閱 [使用 XMLA 建立資料採礦查詢](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md)。  
  
## <a name="list-of-data-mining-schema-rowsets"></a>資料採礦結構描述資料列集的清單  
 下表列出可能適用於查詢和監視的資料採礦結構描述資料列集。  
  
|資料列集名稱|說明|  
|-----------------|-----------------|  
|DMSCHEMA_MINING_MODELS|列出目前環境中的所有採礦模型。<br /><br /> 其中包含的資訊如建立的日期、建立模型所使用的參數，以及定型集的大小。|  
|DMSCHEMA_MINING_COLUMNS|列出目前環境之採礦模型中使用的所有資料行。<br /><br /> 其中的資訊包括採礦結構來源資料行的對應、資料類型、精確度，以及可搭配資料行使用的預測函數。|  
|DMSCHEMA_MINING_STRUCTURES|列出目前環境中的所有採礦結構。<br /><br /> 其中的資訊包括是否擴展結構、上次處理結構的日期，以及針對結構所設定之鑑效組資料的定義 (如果有的話)。|  
|DMSCHEMA_MINING_STRUCTURE_COLUMNS|列出目前環境之採礦結構中使用的所有資料行。<br /><br /> 其中的資訊包括內容類型和資料類型、Null 屬性，以及資料行是否包含巢狀資料表資料。|  
|DMSCHEMA_MINING_SERVICES|列出指定之伺服器所提供的所有採礦服務或演算法。<br /><br /> 其中的資訊包括支援的模型旗標、輸入類型，以及支援的資料來源類型。|  
|DMSCHEMA_MINING_SERVICE_PARAMETERS|列出目前執行個體所提供之採礦服務的所有參數。<br /><br /> 其中的資訊包括每個參數的資料類型、預設值，以及上限與下限。|  
|DMSCHEMA_MODEL_CONTENT|如果模型已經經過處理，傳回模型的內容。<br /><br /> 如需詳細資訊，請參閱[採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。|  
|DBSCHEMA_CATALOGS|列出 Analysis Services 目前執行個體中的所有資料庫 (目錄)。|  
|MDSCHEMA_INPUT_DATASOURCES|列出 Analysis Services 目前執行個體中的所有資料來源。|  
  
> [!NOTE]  
>  資料表中的清單並不完整，因為該清單中只顯示與疑難排解相關的資料列集。  
  
## <a name="examples"></a>範例  
 下節會針對資料採礦結構描述資料列集提供查詢的一些範例。  
  
### <a name="example-1-list-data-mining-services"></a>範例 1：列出資料採礦服務  
 下列查詢會傳回目前伺服器所提供之採礦服務的清單，表示已啟用的演算法。 針對每個採礦服務提供的資料行包括每個演算法所使用的模型旗標與內容類型、每個服務的 GUID，以及可能已經針對每個服務加入的任何預測限制。  
  
```  
SELECT *  
FROM $system.DMSCHEMA_MINING_SERVICES  
```  
  
### <a name="example-2-list-mining-model-parameters"></a>範例 2：列出採礦模型參數  
 下列範例會傳回建立特定採礦模型所使用的參數：  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
### <a name="example-3-list-all-rowsets"></a>範例 3：列出所有資料列集  
 下列範例會傳回目前伺服器所提供之資料列集的完整清單：  
  
```  
SELECT *   
FROM $system.DBSCHEMA_TABLES  
```  
  
  

