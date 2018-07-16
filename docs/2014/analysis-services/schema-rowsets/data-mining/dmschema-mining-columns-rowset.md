---
title: DMSCHEMA_MINING_COLUMNS 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_COLUMNS rowset
ms.assetid: ae35ccde-4438-46f4-8611-40b2b1a42fce
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 60dc2e773b93f27fe96489bcb55fdfe22c3168d4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232058"
---
# <a name="dmschemaminingcolumns-rowset"></a>DMSCHEMA_MINING_COLUMNS 資料列集
  說明中的所有資料採礦模型的個別資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 這個資料列集會限定為目前的目錄。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DMSCHEMA_MINING_COLUMNS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||目錄的名稱。 以模型所屬的資料庫名稱來擴展。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||不合格的結構描述名稱。 不支援此資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含`NULL`。|  
|`MODEL_NAME`|`DBTYPE_WSTR`||採礦模型名稱。 此資料行包含與資料行相關聯的採礦模型名稱，而且它永遠都不會是空的。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||資料行的名稱。|  
|`COLUMN_GUID`|`DBTYPE_GUID`||資料行 GUID。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||資料行屬性的識別碼。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||資料行的序數位置。 資料行的編號會從 1 開始。 如果資料行沒有穩定的序數值，則此資料行會包含 `NULL`。|  
|`COLUMN_HAS_DEFAULT`|`DBTYPE_BOOL`||布林值，指出資料行是否有預設值。<br /><br /> 如果資料行有預設值，則為 `TRUE`，否則為 `FALSE`。|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||資料行的預設值。<br /><br /> 如果預設值是 `NULL` 值，則 `COLUMN_HASDEFAULT` 包含 `TRUE`，而且此資料行包含 `NULL`。|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||描述資料行特性的位元遮罩。 `DBCOLUMNFLAGS` 列舉類型會指定位元遮罩中的位元。 這個資料行永遠都不會是空的。|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||布林值，指出資料行是否可為 Null。<br /><br /> 如果資料行不可為 Null，則為 `FALSE`，否則為 `TRUE`。|  
|`DATA_TYPE`|`DBTYPE_UI2`||資料行之資料類型的指標。 下列清單示範傳回的指標類型之範例。<br /><br /> "`TABLE`" 將會傳回 `DBTYPE_HCHAPTER`。<br /><br /> "`TEXT`" 將會傳回 `DBTYPE_WCHAR`。<br /><br /> "`LONG`" 將會傳回 `DBTYPE_I8`。<br /><br /> "`DOUBLE`" 將會傳回 `DBTYPE_R8`。<br /><br /> "`DATE`" 將會傳回 `DBTYPE_DATE`。|  
|`TYPE_GUID`|`DBTYPE_GUID`||資料行資料類型的 GUID。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `VT_NULL`。|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||資料欄中值的可能長度上限。 若是字元、二進位或是位元資料行，這是下列其中一個：<br /><br /> 的中的字元、 位元組或是位元，分別為資料行類型，如果有定義長度的資料行最大長度。 例如，SQL 資料表中的 `CHAR(5)` 資料行其最大的長度為 5。<br />-中的字元、 位元組或是位元，分別為資料行類型，如果資料行沒有定義的長度的資料類型最大長度。<br />零 (0) (如果資料行和資料類型都不具有已定義的最大長度。<br />-   `NULL` 所有其他類型的資料行|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||如果資料行類型是字元或是二進位，則為以八位元資料組 (位元組) 為單位之資料行的最大長度。 值為零 (0) 表示資料行沒有最大長度。 此資料行對於所有其他類型的資料行都包含 `NULL`。|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||如果資料行的資料類型是 `VARNUMERIC` 以外的數值資料類型，則為資料行的最大有效位數。<br /><br /> 如果資料行的資料類型不是數值或者是 `NULL`，則為 `VARNUMERIC`。<br /><br /> 具有 `DBTYPE_DECIMAL` 或 `DBTYPE_NUMERIC` 的資料類型之資料行的有效位數，取決於資料行定義。|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||如果資料行的類型指標為 `DBTYPE_DECIMAL`、`DBTYPE_NUMERIC` 或 `DBTYPE_VARNUMERIC`，則為小數點右邊的位數。 否則，這個資料行會包含 `VT_NULL`。|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||如果資料行的資料類型是 DateTime 或是間隔類型，則為資料行的日期/時間有效位數 (毫秒部分的位數)；否則為 `NULL`。|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||定義字元集的目錄名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||用於定義字元集的不合格結構描述名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||字元集名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||定義定序物件的目錄名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||用於定義定序的不合格結構描述名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||定序名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||定義網域的目錄名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||用於定義網域的不合格結構描述名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||網域名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 並不支援此資料行，它一律包含 `NULL`。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||使用者易記的資料行描述。[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支援這個資料行，它一律包含 `NULL`。|  
|`DISTRIBUTION_FLAG`|`DBTYPE_WSTR`||資料行的統計散發描述。 這個資料行包含下列其中一項：<br /><br /> -   "`NORMAL`"<br />-   "`LOG_NORMAL`"<br />-   "`UNIFORM`"|  
|`CONTENT_TYPE`|`DBTYPE_WSTR`||資料行內容的描述。 這個資料行包含下列其中一項：<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-「`DISCRETIZED(`[引數]`)`"<br />-   "`ORDERED`"<br />-   "`KEY TIME`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY_VARIANCE`"<br />-   "`PROBABILITY_STDEV`"<br />-   `"KEY SEQUENCE`"|  
|`MODELING_FLAG`|`DBTYPE_WSTR`||以逗號分隔的旗標清單。 已定義的旗標如下：<br /><br /> -   "`MODEL_EXISTENCE_ONLY`"<br />-   "`REGRESSOR`"<br /><br /> 演算法特定的模型旗標也可以包含在資料行中。|  
|`IS_RELATED_TO_KEY`|`DBTYPE_BOOL`||布林值，指出資料行是否與索引鍵相關。<br /><br /> 如果此資料行與索引鍵相關，則為 `TRUE`。 如果索引鍵是單一資料行，`RELATED_ATTRIBUTE` 欄位可能會選擇性地包含其資料行名稱。|  
|`RELATED_ATTRIBUTE`|`DBTYPE_WSTR`||與目前的資料行相關或為其特殊屬性的目標資料行名稱。|  
|`IS_INPUT`|`DBTYPE_BOOL`||布林值，指出資料行是否為輸入資料行。<br /><br /> 如果這是輸入資料行，則為 `VARIANT_TRUE`。|  
|`IS_PREDICTABLE`|`DBTYPE_BOOL`||布林值，指出資料行是否為可預測。<br /><br /> 如果資料行是可預測的，則為 `TRUE`。|  
|`CONTAINING_COLUMN`|`DBTYPE_WSTR`||包含此資料行的 `TABLE` 資料行之名稱。 如果資料行不包含在另一個資料行中，則此資料行包含 `NULL`。|  
|`PREDICTION_SCALAR_FUNCTIONS`|`DBTYPE_WSTR`||以逗號分隔的清單，其中列出可在資料行上執行的純量函數。|  
|`PREDICTION_TABLE_FUNCTIONS`|`DBTYPE_WSTR`||以逗號分隔的清單，其中列出可套用至資料行的函數。 函數應該傳回資料表。 此清單具有下列格式：<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> 此格式允許用戶端應用程式針對個別的函數決定簽章 (參數清單)。|  
|`IS_POPULATED`|`DBTYPE_BOOL`||布林值，指出資料行是否已使用一組可能的值來定型。<br /><br /> 如果資料行已使用一組可能的值來定型，則為 `TRUE`。<br /><br /> 如果未擴展資料行，則包含 `FALSE`。|  
|`PREDICTION_SCORE`|`DBTYPE_R8`||預測資料行之模型的分數。 分數是用以測量模型的精確度。|  
|`SOURCE_COLUMN`|`DBTYPE_WSTR`||目前採礦資料行的來源採礦結構資料行之名稱。|  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DMSCHEMA_MINING_COLUMNS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|選擇性。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|選擇性。|  
|`MODEL_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
