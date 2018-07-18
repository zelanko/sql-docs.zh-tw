---
title: MDSCHEMA_KPIS 資料列集 |Microsoft Docs
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
- MDSCHEMA_KPIS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 391c27165b9b4482160b2a8396e64e46650aa87e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314768"
---
# <a name="mdschemakpis-rowset"></a>MDSCHEMA_KPIS 資料列集
  描述資料庫內的關鍵效能指標 (KPI)。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_KPIS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||來源資料庫。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不支援。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||KPI 的父 Cube。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||KPI 的相關量值群組。<br /><br /> 您可以使用此資料行來決定 KPI 的維度性。 如果 「**\<NULL >**」，將會建立維度的所有量值群組的 KPI。<br /><br /> 預設值是"**\<NULL >**"。|  
|`KPI_NAME`|`DBTYPE_WSTR`||KPI 的名稱。|  
|`KPI_CAPTION`|`DBTYPE_WSTR`||與 KPI 相關聯的標籤或標題。 主要用於顯示用途。 如果標題不存在，就會傳回 `KPI_NAME`。|  
|`KPI_DESCRIPTION`|`DBTYPE_WSTR`||人們可讀取的 KPI 描述。|  
|`KPI_DISPLAY_FOLDER`|`DBTYPE_WSTR`||識別用戶端應用程式用於顯示成員之顯示資料夾路徑的字串。 資料夾層級的分隔符號是由用戶端應用程式所定義。 工具和所提供的用戶端[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，反斜線 (\\) 為層級分隔符號。 若要提供多個顯示資料夾，請使用分號 （;） 來分隔資料夾。|  
|`KPI_VALUE`|`DBTYPE_WSTR`||KPI 值之量值維度中成員的唯一名稱。|  
|`KPI_GOAL`|`DBTYPE_WSTR`||KPI Goal 之量值維度中成員的唯一名稱。<br /><br /> 如果沒有定義 Goal，就會傳回 `NULL`。|  
|`KPI_STATUS`|`DBTYPE_WSTR`||KPI Status 的量值維度中成員的唯一名稱。<br /><br /> 如果沒有定義 Status，則會傳回 `NULL`。|  
|`KPI_TREND`|`DBTYPE_WSTR`||KPI Trend 的量值維度中成員的唯一名稱。<br /><br /> 如果沒有定義 Trend，會傳回 `NULL`。|  
|`KPI_STATUS_GRAPHIC`|`DBTYPE_WSTR`||KPI 預設圖形表示。|  
|`KPI_TREND_GRAPHIC`|`DBTYPE_WSTR`||KPI 預設圖形表示。|  
|`KPI_WEIGHT`|`DBTYPE_WSTR`||KPI Weight 之量值維度中成員的唯一名稱。|  
|`KPI_CURRENT_TIME_MEMBER`|`DBTYPE_WSTR`||定義 KPI 暫時內容之時間維度中成員的唯一名稱。<br /><br /> 如果沒有定義 Time 成員，則會傳回 `NULL`。|  
|`KPI_PARENT_KPI_NAME`|`DBTYPE_WSTR`||父 KPI 的名稱。|  
|`SCOPE`|`DBTYPE_I4`||KPI 的範圍。 KPI 可以是工作階段 KPI 或是全域 KPI。<br /><br /> 此資料行可以有下列其中一個值：<br /><br /> -MDKPI_SCOPE_GLOBAL = 1<br />-MDKPI_SCOPE_SESSION = 2|  
|`ANNOTATIONS`|`DBTYPE_WSTR`||(選擇性) 一組注意事項 (以 XML 格式表示)。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_KPIS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`KPI_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -   `1` CUBE<br />-   `2` 維度<br /><br /> 預設限制為值 `1`。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  
