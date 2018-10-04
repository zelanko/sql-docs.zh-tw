---
title: DISCOVER_JOBS 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DISCOVER_JOBS rowset
ms.assetid: b4d83bb6-aed3-4513-b516-cefadf95dad2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f834e9d6e7c310e16bbb9266b004d5c8a54d176d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087078"
---
# <a name="discoverjobs-rowset"></a>DISCOVER_JOBS 資料列集
  提供在伺服器上執行之作用中作業的相關資訊。 作業是代表該命令執行特定工作之命令的一部分。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_JOBS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`JOB_CREATION_TIME`|`DBTYPE_DBTIMESTAMP`||建立作業時的伺服器 UTC 日期和時間。|  
|`JOB_DESCRIPTION`|`DBTYPE_WSTR`||伺服器服務指派的工作描述。|  
|`JOB_EXECUTION_TIME_MS`|`DBTYPE_I8`||作業作用中的時間 (以毫秒為單位)。|  
|`JOB_ID`|`DBTYPE_I4`||作業的唯一識別碼。|  
|`JOB_START_TIME`|`DBTYPE_DBTIMESTAMP`||啟動作業時的伺服器 UTC 日期和時間。|  
|`JOB_THREADPOOL_ID`|`DBTYPE_I4`||啟動目前作業的執行緒集區。|  
|`JOB_TOTAL_TIME_MS`|`DBTYPE_I8`||啟動作業之後的時間 (以毫秒為單位)。|  
|`SPID`|`DBTYPE_I4`||工作階段識別碼。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DISCOVER_JOBS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|選擇性。|  
|JOB_ID|DBTYPE_I4|選擇性。|  
|JOB_DESCRIPTION|DBTYPE_WSTR|選擇性。|  
|JOB_THREADPOOL_ID|DBTYPE_I4|選擇性。|  
|JOB_MIN TOTAL_TIME_MS|DBTYPE_I8|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  
