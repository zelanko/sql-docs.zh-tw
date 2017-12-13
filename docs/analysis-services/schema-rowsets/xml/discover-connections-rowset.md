---
title: "DISCOVER_CONNECTIONS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_CONNECTIONS rowset
ms.assetid: e4703970-c31d-448c-ab68-503303c91aa4
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3dfac6a570588d4fb08d255319bebd834c3512cf
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="discoverconnections-rowset"></a>DISCOVER_CONNECTIONS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]提供在伺服器上的資源使用量與活動資訊目前開啟的連接。  
  
 **適用於：**表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_CONNECTIONS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|Description|  
|-----------------|--------------------|------------------|-----------------|  
|**CONNECTION_ID**|**DBTYPE_I4**|是|識別連接的唯一號碼。|  
|**CONNECTION_USER_NAME**|**DBTYPE_WSTR**|是|連接使用者名稱。|  
|**CONNECTION_IMPERSONATED_USER_NAME**|**DBTYPE_WSTR**|是|保留供日後使用。 針對 CONNECTION_IMPERSONATED_USER_NAME 的值，Analysis Services 一律會傳回 NULL。|  
|**CONNECTION_HOST_NAME**|**DBTYPE_WSTR**|是|起始連接的電腦名稱。|  
|**CONNECTION_HOST_APPLICATION**|**DBTYPE_WSTR**||起始連接的應用程式名稱。|  
|**CONNECTION_START_TIME**|**DBTYPE_DBTIMESTAMP**||連接起始時，伺服器的 UTC 日期和時間。|  
|**CONNECTION_ELAPSED_TIME_MS**|**DBTYPE_I8**|是|連接開始之後，以毫秒為單位的經過時間。|  
|**CONNECTION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||當上一個命令起始其執行時，伺服器的 UTC 日期與時間。|  
|**CONNECTION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||當上一個命令完成其執行時，伺服器的 UTC 日期與時間。|  
|**CONNECTION_LAST_COMMAND_ELAPSED_TIME_MS**|**DBTYPE_I8**|是|上次執行命令結束之後，以毫秒為單位的經過時間。|  
|**CONNECTION_IDLE_TIME_MS**|**DBTYPE_I8**|是|自從連接啟動以後的閒置時間，以毫秒為單位。|  
|**CONNECTION_BYTES_SENT**|**DBTYPE_I8**||連接啟動之後，連接傳送的累積位元組數。|  
|**CONNECTION_DATA_BYTES_SENT**|**DBTYPE_I8**||連接啟動之後，連接傳送的累積資料位元組數。<br /><br /> 傳輸的資料會在連接中壓縮，這個值代表所傳送的展開資料。|  
|**CONNECTION_BYTES_RECEIVED**|**DBTYPE_I8**||連接啟動之後，連接收到的累積位元組數。|  
|**CONNECTION_DATA_BYTES_RECEIVED**|**DBTYPE_I8**||連接啟動之後，連接收到的累積資料位元組數。<br /><br /> 傳輸的資料會在連接中壓縮，這個值代表所收到的展開資料。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd25-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|連接|  
  
## <a name="see-also"></a>請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
