---
title: MDSCHEMA_HIERARCHIES 資料列集 |Microsoft Docs
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
- MDSCHEMA_HIERARCHIES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_HIERARCHIES rowset
ms.assetid: 2e5b2a81-366e-4d5b-af1e-1d372bf596d9
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a38dd03023fc266c5b8505979766d90979d16f05
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321218"
---
# <a name="mdschemahierarchies-rowset"></a>MDSCHEMA_HIERARCHIES 資料列集
  描述特定維度中的每個階層。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_HIERARCHIES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||這個階層所屬之目錄的名稱。 如果提供者不支援目錄，則為 `NULL`。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不支援|  
|`CUBE_NAME`|`DBTYPE_WSTR`||(必要項) 此階層所屬 Cube 的名稱。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||此階層所屬維度的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|`HIERARCHY_NAME`|`DBTYPE_WSTR`||階層的名稱。 如果維度中只有單一階層則為空白。 一定會有值， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||階層架構的唯一名稱。|  
|`HIERARCHY_GUID`|`DBTYPE_GUID`||不支援|  
|`HIERARCHY_CAPTION`|`DBTYPE_WSTR`||與階層關聯的標籤或標題。 主要用於顯示用途。 如果標題不存在，就會傳回 `HIERARCHY_NAME`。 如果維度不包含階層或只具有一個階層，則此資料行會包含維度名稱。|  
|`DIMENSION_TYPE`|`DBTYPE_I2`||維度的類型。 有效值包括下列各值：<br /><br /> -   `MD_DIMTYPE_UNKNOWN` (`0`)<br />-   `MD_DIMTYPE_TIME` (`1`)<br />-   `MD_DIMTYPE_MEASURE` (`2`)<br />-   `MD_DIMTYPE_OTHER` (`3`)<br />-   `MD_DIMTYPE_QUANTITATIVE` (`5`)<br />-   `MD_DIMTYPE_ACCOUNTS` (`6`)<br />-   `MD_DIMTYPE_CUSTOMERS` (`7`)<br />-   `MD_DIMTYPE_PRODUCTS` (`8`)<br />-   `MD_DIMTYPE_SCENARIO` (`9`)<br />-   `MD_DIMTYPE_UTILIY` (`10`)<br />-   `MD_DIMTYPE_CURRENCY` (`11`)<br />-   `MD_DIMTYPE_RATES` (`12`)<br />-   `MD_DIMTYPE_CHANNEL` (`13`)<br />-   `MD_DIMTYPE_PROMOTION` (`14`)<br />-   `MD_DIMTYPE_ORGANIZATION` (`15`)<br />-   `MD_DIMTYPE_BILL_OF_MATERIALS` (`16`)<br />-   `MD_DIMTYPE_GEOGRAPHY` (`17`)|  
|`HIERARCHY_CARDINALITY`|`DBTYPE_UI4`||階層中的成員數目。|  
|`DEFAULT_MEMBER`|`DBTYPE_WSTR`||此階層的預設成員。 這是唯一的名稱。 每個階層都必須有一個預設成員。|  
|`ALL_MEMBER`|`DBTYPE_WSTR`||積存最高層級的成員。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||人們可讀取的階層描述。 如果沒有描述，則為 `NULL`。|  
|`STRUCTURE`|`DBTYPE_I2`||階層的結構。 有效值包括下列各值：<br /><br /> -   `MD_STRUCTURE_FULLYBALANCED` (`0`)<br />-   `MD_STRUCTURE_RAGGEDBALANCED` (`1`)<br />-   `MD_STRUCTURE_UNBALANCED` (`2`)<br />-   `MD_STRUCTURE_NETWORK` (`3`)|  
|`IS_VIRTUAL`|`DBTYPE_BOOL`||一律會傳回`False`。|  
|`IS_READWRITE`|`DBTYPE_BOOL`||布林值，指出是否啟用回寫至維度資料行功能。<br /><br /> 如果已啟用代表此階層的 `TRUE` 資料行，則傳回 `Write Back to dimension`。|  
|`DIMENSION_UNIQUE_SETTINGS`|`DBTYPE_I4`||永遠傳回 `MDDIMENSIONS_MEMBER_KEY_UNIQUE` (`1`)。|  
|`DIMENSION_MASTER_UNIQUE_NAME`|`DBTYPE_WSTR`||一律會傳回`NULL`。|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||一律會傳回`true`。 如果維度為不可見，就不會顯示在結構描述資料列集中。|  
|`HIERARCHY_ORDINAL`|`DBTYPE_UI4`||階層在 Cube 所有階層中的序數。|  
|`DIMENSION_IS_SHARED`|`DBTYPE_BOOL`||一律會傳回`TRUE`。|  
|`HIERARCHY_IS_VISIBLE`|`DBTYPE_BOOL`||布林值，指出階層是否為可見。<br /><br /> 如果階層為可見，則傳回 `TRUE`；否則傳回 `FALSE`。|  
|`HIERARCHY_ORIGIN`|`DBTYPE_UI2`||位元遮罩，決定階層的來源：<br /><br /> -   `MD_USER_DEFINED` 識別使用者定義階層，且其值為`0x0000001`。<br />-   `MD_SYSTEM_ENABLED` 識別屬性階層，且其值為`0x0000002`。<br />-   `MD_SYSTEM_INTERNAL` 使用沒有屬性階層，識別屬性和其值為**0x0000004**。<br /><br /> 父子式屬性階層同時為 `MD_USER_DEFINED` 和 `MD_SYSTEM_ENABLED`。|  
|`HIERARCHY_DISPLAY_FOLDER`|`DBTYPE_WSTR`||在使用者介面中顯示階層時所使用的路徑。 資料夾名稱將以分號 (;) 分隔。 巢狀的資料夾會以反斜線 (\\)。|  
|`INSTANCE_SELECTION`|`DBTYPE_UI2`||提供給用戶端應用程式有關如何顯示階層的提示。 有效值包括下列各值：<br /><br /> -   `MD_INSTANCE_SELECTION_NONE`<br />-   `MD_INSTANCE_SELECTION_DROPDOWN`<br />-   `MD_INSTANCE_SELECTION_LIST`<br />-   `MD_INSTANCE_SELECTION_FILTEREDLIST`<br />-   `MD_INSTANCE_SELECTION_MANDATORYFILTER`|  
|`GROUPING_BEHAVIOR`|`DBTYPE_I2`||列舉，指定此階層的預期用戶端分組行為。 可能的值如下：<br /><br /> -   **EncourageGrouping** (1)<br />-   **DiscourageGrouping** (2)|  
|`STRUCTURE_TYPE`|`DBTYPE_WSTR`||表示階層的類型。 有效值包括下列各值：<br /><br /> -   `Natural`<br />-   `Unnatural`<br />-   `Unknown`|  
  
 資料列集會按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME`、`DIMENSION_UNIQUE_NAME` 和 `HIERARCHY_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_HIERARCHIES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`HIERARCHY_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`HIERARCHY_ORIGIN`|`DBTYPE_UI2`|(選擇性) 預設限制會在 MD_USER_DEFINED 和 MD_SYSTEM_ENABLED 上生效。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 的 CUBE<br />-2 的維度<br /><br /> 預設限制為值 1。|  
|`HIERARCHY_VISIBILITY`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 看得見<br />-2 不可見<br /><br /> 預設限制為值 1。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  
