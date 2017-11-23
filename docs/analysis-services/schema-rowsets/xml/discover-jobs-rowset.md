---
title: "DISCOVER_JOBS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_JOBS rowset
ms.assetid: b4d83bb6-aed3-4513-b516-cefadf95dad2
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: edf0125dff1f193106f5738aef99b8c830c29236
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="discoverjobs-rowset"></a>DISCOVER_JOBS 資料列集
  提供在伺服器上執行之作用中作業的相關資訊。 作業是代表該命令執行特定工作之命令的一部分。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_JOBS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**JOB_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||建立作業時的伺服器 UTC 日期和時間。|  
|**JOB_DESCRIPTION**|**DBTYPE_WSTR**||伺服器服務指派的工作描述。|  
|**JOB_EXECUTION_TIME_MS**|**DBTYPE_I8**||作業作用中的時間 (以毫秒為單位)。|  
|**JOB_ID**|**DBTYPE_I4**||作業的唯一識別碼。|  
|**JOB_START_TIME**|**DBTYPE_DBTIMESTAMP**||啟動作業時的伺服器 UTC 日期和時間。|  
|**JOB_THREADPOOL_ID**|**DBTYPE_I4**||啟動目前作業的執行緒集區。|  
|**JOB_TOTAL_TIME_MS**|**DBTYPE_I8**||啟動作業之後的時間 (以毫秒為單位)。|  
|**SPID**|**DBTYPE_I4**||工作階段識別碼。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_JOBS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|選擇性。|  
|JOB_ID|DBTYPE_I4|選擇性。|  
|JOB_DESCRIPTION|DBTYPE_WSTR|選擇性。|  
|JOB_THREADPOOL_ID|DBTYPE_I4|選擇性。|  
|JOB_MIN TOTAL_TIME_MS|DBTYPE_I8|選擇性。|  
  
## <a name="see-also"></a>請參閱＜  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
