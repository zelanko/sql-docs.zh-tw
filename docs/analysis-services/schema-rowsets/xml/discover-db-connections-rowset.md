---
title: DISCOVER_DB_CONNECTIONS 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_DB_CONNECTIONS rowset
ms.assetid: 12a51a4e-5f3d-4449-9d94-7836fea1bc8b
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8a932cfa872e0cceed0b132f486349716ba4210b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="discoverdbconnections-rowset"></a>DISCOVER_DB_CONNECTIONS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]提供有關從伺服器目前已開啟連接至資料庫的資源使用量與活動資訊。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_DB_CONNECTIONS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|**CONNECTION_CATALOG_NAME**|**DBTYPE_WSTR**||目前連接之資料庫的資料庫名稱。|  
|**CONNECTION_ID**|**DBTYPE_I4**||識別連接的唯一號碼。|  
|**CONNECTION_IDLE_TIME_MS**|**DBTYPE_I8**||自從連接啟動以後的閒置時間，以毫秒為單位。|  
|**CONNECTION_IN_USE**|**DBTYPE_I4**||指出連接是使用中 (1) 或是閒置 (0)。|  
|**CONNECTION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||當上一個命令完成其執行時，伺服器的 UTC 日期與時間。|  
|**CONNECTION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||當上一個命令起始其執行時，伺服器的 UTC 日期與時間。|  
|**CONNECTION_SERVER_NAME**|**DBTYPE_WSTR**||目前連接的伺服器名稱。|  
|**CONNECTION_SPID**|**DBTYPE_I4**||工作階段識別碼。|  
|**CONNECTION_START_TIME**|**DBTYPE_DBTIMESTAMP**||連接起始時，伺服器的 UTC 日期和時間。|  
|**CONNECTION_USAGE_TIME_MS**|**DBTYPE_I8**||自從連接啟動之後的連接使用中時間，以毫秒為單位。|  
  
 這個結構描述資料列集並未排序。  
  
> [!IMPORTANT]  
>  **DISCOVER_DB_CONNECTIONS**服務連接至關聯式資料來源時，資料列集只會顯示資訊。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_DB_CONNECTIONS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|CONNECTION_ID|DBTYPE_I4|選擇性。|  
|CONNECTION_IN_USE|DBTYPE_I4|選擇性。|  
|CONNECTION_SERVER_NAME|DBTYPE_WSTR|選擇性。|  
|CONNECTION_CATALOG_NAME|DBTYPE_WSTR|必要。|  
|CONNECTION_SPID|DBTYPE_I4|選擇性。|  
  
## <a name="see-also"></a>請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
