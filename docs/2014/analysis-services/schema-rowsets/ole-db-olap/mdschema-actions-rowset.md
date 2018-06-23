---
title: MDSCHEMA_ACTIONS 資料列集 |Microsoft 文件
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
- MDSCHEMA_ACTIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_ACTIONS rowset
ms.assetid: f73081f8-ac51-4286-b46e-2b34e792c3e0
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5b3e3a4c91d998e0ba0459577f1e0b469ec7f78b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136298"
---
# <a name="mdschemaactions-rowset"></a>MDSCHEMA_ACTIONS 資料列集
  描述可用於用戶端應用程式的動作。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_ACTIONS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||資料庫的名稱。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不支援。 一定會包含 `VT_NULL`。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此動作所屬 Cube 的名稱。|  
|`ACTION_NAME`|`DBTYPE_WSTR`||此動作的名稱。|  
|`ACTION_TYPE`|`DBTYPE_I4`||點陣圖，可用於指定動作的觸發方法。 Msmd.h 檔案為此點陣圖定義下列的位元值常數：<br /><br /> -   `MDACTION_TYPE_URL` (`0x01`)<br />-   `MDACTION_TYPE_HTML` (`0x02`)<br />-   `MDACTION_TYPE_STATEMENT` (`0x04`)<br />-   `MDACTION_TYPE_DATASET` (`0x08`)<br />-   `MDACTION_TYPE_ROWSET` (`0x10`)<br />-   `MDACTION_TYPE_COMMANDLINE` (`0x20`)<br />-   `MDACTION_TYPE_PROPRIETARY` (`0x40`)<br />-   `MDACTION_TYPE_REPORT` (`0x80`)<br />-   `MDACTION_TYPE_DRILLTHROUGH` (`0x100`)|  
|`COORDINATE`|`DBTYPE_WSTR`||多維度運算式 (MDX) 運算式，指定物件或要在其中執行動作的多維度空間中的座標。 用戶端應用程式必須負責提供此限制資料行的值。<br /><br /> `CORDINATE` 必須解決成 `COORDINATE_TYPE` 所指定的物件。|  
|`COORDINATE_TYPE`|`DBTYPE_I4`||點陣圖，指定如何解譯 `COORDINATE` 限制資料行。 Msmd.h 檔案為此點陣圖定義下列的位元值常數：<br /><br /> -   `MDACTION_COORDINATE_CUBE` (`1`)<br />-   `MDACTION_COORDINATE_DIMENSION` (`2`)<br />     參考到維度階層。<br />-   `MDACTION_COORDINATE_LEVEL` (`3`)<br />-   `MDACTION_COORDINATE_MEMBER` (`4`)<br />-   `MDACTION_COORDINATE_SET` (`5`)<br />-   `MDACTION_COORDINATE_CELL` (`6`)|  
|`ACTION_CAPTION`|`DBTYPE_WSTR`||如果未指定任何標題，且 DDL 中未指定任何翻譯，則此為動作名稱。<br /><br /> 如果指定了標題或翻譯，且 `CaptionIsMDX` 為 False，則下列其中一個字串：<br /><br /> 的適當語言翻譯。<br />如果找不到指定之語言的任何轉譯-指定的標題。<br />的如果沒有找到翻譯，且 DDL 中未指定標題動作名稱。<br /><br /> 如果指定了標題或翻譯，且 `CaptionIsMDX` 為 True，則字串會在找到 DDL 標題中所指定語言的適當翻譯或指定翻譯，並計算建立字串的公式後產生。<br /><br /> 如果動作是在 MDX 指令碼中指定，則沒有翻譯，且標題一定會被視為 MDX 運算式。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||動作的易記描述。|  
|`CONTENT`|`DBTYPE_WSTR`||要執行之動作的運算式或內容。|  
|`APPLICATION`|`DBTYPE_WSTR`||要用於執行動作的應用程式的名稱。|  
|`INVOCATION`|`DBTYPE_I4`||如何叫用動作的相關資訊：<br /><br /> -   `MDACTION_INVOCATION_INTERACTIVE` (`1`) 指出在正常作業期間使用的一般動作。 這是此資料行的預設值。<br />-   `MDACTION_INVOCATION_ON_OPEN` (`2`) 表示第一次開啟 cube 時，應該執行此動作。<br />-   `MDACTION_INVOCATION_BATCH` (`4`) 表示執行的動作是做為批次作業的一部分或[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]工作。<br /><br /> 這些列舉值會定義於 Msmd.h 檔案中。|  
  
 資料列集會按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME` 和 `ACTION_NAME` 排序。  
  
> [!NOTE]  
>  `MDACTION_TYPE_PROPRIETARY` 類型的動作必須提供 `APPLICATION` 資料行的值。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_ACTIONS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性|  
|`CUBE_NAME`|`DBTYPE_WSTR`|強制性|  
|`ACTION_NAME`|`DBTYPE_WSTR`|選擇性|  
|`ACTION_TYPE`|`DBTYPE_I4`|選擇性|  
|`COORDINATE`|`DBTYPE_WSTR`|強制性|  
|`COORDINATE_TYPE`|`DBTYPE_I4`|強制性|  
|`INVOCATION`|`DBTYPE_I4`|(選擇性) `INVOCATION` 限制資料行預設為 `MDACTION_INVOCATION_INTERACTIVE` 的值。 若要擷取所有動作，請使用 `MDACTION_INVOCATION_ALL` 限制資料行中的 `INVOCATION` 值。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 的 CUBE<br />-2 的維度<br /><br /> 預設限制為值 1。|  
  
> [!IMPORTANT]  
>  `INVOCATION` 限制資料行具有 `MDACTION_INVOCATION_INTERACTIVE` 的預設值。 任何未明確指定此資料行值的結構描述資料列集，都只包含具有此值的資料列。 如果想要資料列集包含整個動作集，請在 `MDACTION_INVOCATION_ALL` 限制資料行中使用 `INVOCATION` 常數。  
  
 用戶端應用程式可以使用 OR 運算子來定義一個以上的 `ACTION_TYPE`。  
  
## <a name="remarks"></a>備註  
 下表列出有效的 `COORDINATE` 和 `COORDINATE_TYPE` 組合。  
  
|COORDINATE 物件類型|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|`Cube`|`MDACTION_COORDINATE_CUBE`|  
|`Dimension`|`MDACTION_COORDINATE_DIMENSION`<br /><br /> `MDACTION_COORDINATE_LEVEL`<br /><br /> `MDACTION_COORDINATE_MEMBER`<br /><br /> `MDACTION_COORDINATE_SET`<br /><br /> `MDACTION_COORDINATE_CELL`|  
|`Hierarchy`|`MDACTION_COORDINATE_DIMENSION`|  
|`Level`|`MDACTION_COORDINATE_LEVEL`|  
|`Member`|`MDACTION_COORDINATE_MEMBER`|  
|`Set`|`MDACTION_COORDINATE_SET`|  
|`cell`|`MDACTION_COORDINATE_CELL`|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  