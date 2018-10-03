---
title: DMSCHEMA_MINING_STRUCTURE_COLUMNS 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c012515df76b1f19712c5bf1ba828dafdc787ef7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088368"
---
# <a name="dmschemaminingstructurecolumns-rowset"></a>DMSCHEMA_MINING_STRUCTURE_COLUMNS 資料列集
  描述正在執行的伺服器上部署的所有採礦結構的個別資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DMSCHEMA_MINING_STRUCTURE_COLUMNS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`||目錄的名稱。|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`||不合格的結構描述名稱。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支援結構描述，因此這個資料行永遠都是 `NULL`。|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`||結構名稱。 這個資料行不能包含 `NULL`。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||資料行的名稱。 只有在共用相同模式的資料行之間可保證唯一性。 例如，如果它們在相同結構中屬於兩個不同的巢狀資料表，則這兩個巢狀資料行可能會有相同的名稱。|  
|`COLUMN_GUID`|`DBTYPE_GUID`||資料行 GUID。 不使用 GUID 來識別資料行的提供者，應該會在這個資料行中傳回 `NULL`。|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||資料行屬性的識別碼。 未將屬性識別碼與資料行相關聯的提供者，應該會在這個資料中傳回 `NULL`。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 傳回`NULL`這個資料行。|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||資料行的序數。 資料行的編號會從 1 開始。 如果資料行沒有穩定的序數值，則為 `NULL`。|  
|`COLUMN_HASDEFAULT`|`DBTYPE_BOOL`||布林值，指出資料行是否有預設值。<br /><br /> 如果資料行有預設值，則為 `TRUE`。<br /><br /> 如果資料行沒有預設值，或是如果不知道資料行是否有預設值，則為 `FALSE`。|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||資料行的預設值。 提供者可能會在 `DBCOLUMN_DEFAULTVALUE` 傳回的資料列集中公開 `DBCOLUMN_HASDEFAULT`，而不會公開 `IColumnsRowset::GetColumnsRowset` (適用於 ISO 資料表)。<br /><br /> 如果預設值是 `NULL`，則 `COLUMN_HASDEFAULT` 是 `TRUE`，而 `COLUMN_DEFAULT` 資料行是 `NULL` 值。|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||的描述資料行特性位元遮罩。 `DBCOLUMNFLAGS` 列舉類型會指定位元遮罩中的位元。 此資料行不得包含 `NULL` 值。 有效值包括：<br />-   **DBCOLUMNFLAGS_ISNULLABLE** (`0x20`)<br />-   **DBCOLUMNFLAGS_MAYBENULL** (`0x40`)<br />-   **DBCOLUMNFLAGS_ISLONG** (`0x80`)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||布林值，指出資料行是否有預設值。<br /><br /> 如果資料行可以包含 `TRUE`，則為 `NULL`，否則為 `FALSE`。|  
|`DATA_TYPE`|`DBTYPE_UI2`||資料行之資料類型的指標。 例如：<br /><br /> -   "`TABLE`" = `DBTYPE_HCHAPTER`<br />-   "`TEXT`" = `DBTYPE_WCHAR`<br />-   "`LONG`" = `DBTYPE_I8`<br />-   "`DOUBLE`" = `DBTYPE_R8`<br />-   "`DATE`" = `DBTYPE_DATE`|  
|`TYPE_GUID`|`DBTYPE_GUID`||資料行資料類型的 GUID。 不使用 GUID 來識別資料類型的提供者，應該會在這個資料行中傳回 `NULL`。|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||資料欄中值的可能長度上限。 若是字元、二進位或是位元資料行，這是下列其中一個：<br /><br /> 集中的資料行的最大長度字元、 位元組或是位元為單位，如果長度定義。 例如，SQL 資料表中的 `CHAR(5)` 資料行其最大的長度為 5。<br />集資料的最大長度中的字元、 位元組或是位元，分別輸入，如果資料行沒有定義的長度。<br />零 (0) (如果資料行和資料類型都不具有已定義的最大長度。<br />-   `NULL` 對於所有其他類型的資料行。|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||如果資料行類型是字元或是二進位，則為以八位元資料組 (位元組) 為單位之資料行的最大長度。 值為零 (0) 表示資料行沒有最大長度。 所有其他類型的資料行都為 `NULL`。|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||如果資料行的資料類型是 `VARNUMERIC` 以外的數值資料類型，則為資料行的最大有效位數；如果資料行的資料類型不是數值或者為 `NULL`，則為 `VARNUMERIC`。<br /><br /> 具有 `DBTYPE_DECIMAL` 或 `DBTYPE_NUM`ERIC 的資料類型之資料行的有效位數，取決於資料行的定義。|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||如果資料行的類型指標為 `DBTYPE_DECIMAL`、`DBTYPE_NUMERIC` 或 `DBTYPE_VARNUMERIC`，則為小數點右邊的位數。 否則，這個值為 `NULL`。|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||如果資料行是日期時間或是間隔類型，則為資料行的 DateTime 有效位數 (毫秒部分的位數)。 如果資料行的資料類型不是日期時間，這將會是 `NULL`。|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||定義字元集的目錄名稱。 如果提供者不支援目錄或是不同的字元集，則為 `NULL`。|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||定義字元集之不合格的結構描述名稱。 如果提供者不支援結構描述或是不同的字元集，則為 `NULL`。|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||字元集名稱。 如果提供者不支援不同的字元集，則為 `NULL`。|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||定義定序物件的目錄名稱。 如果提供者不支援目錄或是不同的定序，則為 `NULL`。|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||定義定序之不合格的結構描述名稱。 如果提供者不支援結構描述或是不同的定序，則為 `NULL`。|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||定序名稱。 如果提供者不支援不同的定序，則為 `NULL`。|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||定義網域的目錄名稱。 如果提供者不支援目錄或是網域，則為 `NULL`。|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||用於定義網域的不合格結構描述名稱。 如果提供者不支援結構描述或是網域，則為 `NULL`。|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||網域名稱。 如果提供者不支援網域，則為 `NULL`。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||人們可讀取的資料行描述。 如果沒有與資料行關聯的描述，則為 `NULL`。|  
|`DISTRIBUTION_FLAG`|`DBTYPE_WSTR`||採礦結構資料行的散發：<br /><br /> -   "`NORMAL`"<br />-「`LOG_NORM`AL"<br />-   "`UNIFORM`"|  
|`CONTENT_TYPE`|`DBTYPE_WSTR`||採礦結構資料行的內容類型：<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-「`DISCRETIZED(`[args]`)`"<br />-   "`ORDERED`"<br />-   "`SEQUENCE_TIME`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY_VARIANCE`"<br />-   "`PROBABILITY_STDEV`"|  
|`MODELING_FLAG`|`DBTYPE_WSTR`||以逗號分隔的模型旗標清單。 結構資料行唯一支援的旗標是 "`NOT NULL`"。|  
|`IS_RELATED_TO_KEY`|`DBTYPE_BOOL`||指出此資料行是否與索引鍵相關的布林值。<br /><br /> 如果此資料行與索引鍵相關，則為 `VARIANT_TRUE`，否則為 `VARIANT_FALSE`。 如果索引鍵是單一資料行，`RELATED_ATTRIBUTE` 欄位可能會選擇性地包含其資料行名稱。|  
|`RELATED_ATTRIBUTE`|`DBTYPE_WSTR`||目標資料行名稱，與目前的資料行相關，或是目前的資料行為其特殊屬性。|  
|`CONTAINING_COLUMN`|`DBTYPE_WSTR`||包含此資料行的 `TABLE` 資料行之名稱。 如果沒有資料表包含資料行，則為 `NULL`。|  
|`IS_POPULATED`|`DBTYPE_BOOL`||布林值，指出此資料行是否已取得一組可能的值。<br /><br /> 如果資料行已取得一組可能的值，則為 `TRUE`，否則為 `FALSE`。|  
  
## <a name="restriction-columns"></a>限制資料行  
 下表中的資料行上可以限制 `DMSCHEMA_MINING_STRUCTURE_COLUMNS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`|選擇性。|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`|選擇性。|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
