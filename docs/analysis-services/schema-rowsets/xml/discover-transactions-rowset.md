---
title: DISCOVER_TRANSACTIONS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: efa1a31f5263b2304bb10fd23eb4fa26a5d3f8ad
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="discovertransactions-rowset"></a>DISCOVER_TRANSACTIONS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  傳回系統上目前的暫止交易集。  
  
 **適用於：**表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_TRANSACTIONS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|Description|  
|-----------------|--------------------|-----------------|  
|**TRANSACTION_ID**|**DBTYPE_WSTR**|做為 GUID 的交易唯一識別碼。|  
|**TRANSACTION_SESSION_ID**|**DBTYPE_WSTR**|做為 GUID 的交易工作階段唯一識別碼。|  
|**TRANSACTION_START_TIME**|**DBTYPE_DBTIMESTAMP**|啟動交易時的伺服器 UTC 日期和時間。|  
|**TRANSACTION_ELAPSED_TIME_MS**|**DBTYPE_I8**|交易啟動以後所經過的時間 (以毫秒為單位)。|  
|**TRANSACTION_CPU_TIME_MS**|**DBTYPE_I8**|交易開始之後，所有要求所耗用的 CPU 時間 (以毫秒為單位)。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_TRANSACTIONS**上表中列出的資料行可能會限制資料列集。  
  
|**資料行名稱**|**類型指標**|**限制狀態**|  
|---------------------|------------------------|---------------------------|  
|**識別碼**|**DBTYPE_WSTR**|選擇性。|  
|**SESSION_ID**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd28-8148-11d0-87bb-00c04fc33942|  
|字串|DISCOVER_TRANSACTIONS|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
