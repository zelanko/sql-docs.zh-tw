---
title: MDSCHEMA_MEASURES 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_MEASURES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASURES rowset
ms.assetid: 6ff5bd1a-aad0-49b8-9f8d-7df2637caacf
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84ea2ceeaef0c6431f3860f3b23da07f43ee6c5a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237468"
---
# <a name="mdschemameasures-rowset"></a>MDSCHEMA_MEASURES 資料列集
  描述 Cube 內的每個量值。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_MEASURES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此量值所屬之目錄的名稱。 如果提供者不支援目錄，則為 `NULL`。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||此量值所屬之結構描述的名稱。 如果提供者不支援結構描述，則為 `NULL`。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此量值所屬 Cube 的名稱。|  
|`MEASURE_NAME`|`DBTYPE_WSTR`||量值的名稱。|  
|`MEASURE_UNIQUE_NAME`|`DBTYPE_WSTR`||量值的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|`MEASURE_CAPTION`|`DBTYPE_WSTR`||與量值關聯的標籤或標題。 主要用於顯示用途。 如果標題不存在，就會傳回 `MEASURE_NAME`。|  
|`MEASURE_GUID`|`DBTYPE_GUID`||不支援。|  
|`MEASURE_AGGREGATOR`|`DBTYPE_I4`||識別如何衍生量值的列舉。 可為下列其中一個值：<br /><br /> -   `MDMEASURE_AGGR_SUM` (`1`) 識別量值彙總從`SUM`。<br />-   `MDMEASURE_AGGR_COUNT` (`2`) 識別量值彙總從`COUNT`。<br />-   **MDMEASURE_AGGR_MIN** (`3`) 識別量值彙總從`MIN`。<br />-   **MDMEASURE_AGGR_MAX** (`4`) 識別量值彙總從`MAX`。<br />-   `MDMEASURE_AGGR_AVG` (`5`) 識別量值彙總從`AVG`。<br />-   `MDMEASURE_AGGR_VAR` (`6`) 識別量值彙總從`VAR`。<br />-   `MDMEASURE_AGGR_STD` (`7`) 識別量值彙總從`STDEV`。<br />-   `MDMEASURE_AGGR_DST` (`8`) 識別量值彙總從`DISTINCT COUNT`。<br />-   `MDMEASURE_AGGR_NONE` (`9`) 識別量值彙總從`NONE`。<br />-   `MDMEASURE_AGGR_AVGCHILDREN` (`10`) 識別量值彙總從`AVERAGEOFCHILDREN`。<br />-   `MDMEASURE_AGGR_FIRSTCHILD` (`11`) 識別量值彙總從`FIRSTCHILD`。<br />-   `MDMEASURE_AGGR_LASTCHILD` (`12`) 識別量值彙總從`LASTCHILD`。<br />-   `MDMEASURE_AGGR_FIRSTNONEMPTY` (`13`) 識別量值彙總從`FIRSTNONEMPTY`，<br />-   `MDMEASURE_AGGR_LASTNONEMPTY` (`14`) 識別量值彙總從`LASTNONEMPTY`。<br />-   `MDMEASURE_AGGR_BYACCOUNT` (`15`) 識別量值彙總從`BYACCOUNT`。<br />-   `MDMEASURE_AGGR_CALCULATED` (`127`) 識別量值衍生自並非上述任何單一函數的公式。<br />-   `MDMEASURE_AGGR_UNKNOWN` (`0`) 識別量值衍生自未知的彙總函式或公式。|  
|`DATA_TYPE`|`DBTYPE_UI2`||量值的資料類型。|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||如果量值物件的資料類型為精確數值，則為屬性的最大有效位數。 如果是所有其他屬性類型，則為 `NULL`。|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||如果量值物件的類型指標為 `DBTYPE_NUMERIC` 或 `DBTYPE_DECIMAL`，則此為小數點右邊的位數。 否則，這個值為 `NULL`。|  
|`MEASURE_UNITS`|`DBTYPE_WSTR`||不支援|  
|`DESCRIPTION`|`DBTYPE_WSTR`||人們可讀取的量值描述。 如果沒有描述，則為 `NULL`。|  
|`EXPRESSION`|`DBTYPE_WSTR`||成員的運算式。|  
|`MEASURE_IS_VISIBLE`|`DBTYPE_BOOL`||布林值，永遠會傳回 True。 如果量值為不可見，就不會包含在結構描述資料列集中。|  
|`LEVELS_LIST`|`DBTYPE_WSTR`||字串，永遠會傳回 `NULL`。|  
|`MEASURE_NAME_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||SQL 查詢中對應到量值名稱之資料行的名稱。|  
|`MEASURE_UNQUALIFIED_CAPTION`|`DBTYPE_WSTR`||量值的名稱，未使用量值群組名稱限定。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||此量值所屬之量值群組的名稱。|  
|`MEASURE_DISPLAY_FOLDER`|`DBTYPE_WSTR`||在使用者介面中顯示量值時所使用的路徑。 資料夾名稱將以分號分隔。 巢狀的資料夾會以反斜線 (\\)。|  
|`DEFAULT_FORMAT_STRING`|`DBTYPE_WSTR`||量值的預設格式字串。|  
  
 資料列集會按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME` 和 `MEASURE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_MEASURES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`MEASURE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`MEASURE_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 的 CUBE<br />-2 的維度<br /><br /> 預設限制為值 1。|  
|`MEASURE_VISIBILITY`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 看得見<br />-2 不可見<br /><br /> 預設限制為值 1。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  
