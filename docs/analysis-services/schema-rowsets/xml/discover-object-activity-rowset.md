---
title: DISCOVER_OBJECT_ACTIVITY 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e5ac394fea6e7f430d1eadd0dc5b0fb1e0e3865
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="discoverobjectactivity-rowset"></a>DISCOVER_OBJECT_ACTIVITY 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供每個物件自從服務啟動之後的資源使用量資訊。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_OBJECT_ACTIVITY**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_AGGREGATION_HIT**|**DBTYPE_I8**||自從服務開始之後，物件之彙總叫用的次數。|  
|**OBJECT_AGGREGATION_MISS**|**DBTYPE_I8**||自從服務開始之後，物件之現有彙總尚未遺漏 (也就是，尚未使用) 的次數。|  
|**OBJECT_CPU_TIME_MS**|**DBTYPE_I8**||自從服務開始之後，物件所耗用的 CPU 時間 (以毫秒為單位)。|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||物件中資料的歷程識別碼，每次處理物件時，這個數字會遞增。|  
|**OBJECT_HIT**|**DBTYPE_I8**||自從服務啟動之後，物件在快取中叫用的次數。|  
|**OBJECT_ID**|**DBTYPE_WSTR**||在建立時定義的物件識別碼。|  
|**OBJECT_MISS**|**DBTYPE_I8**||自從服務啟動之後，物件在快取中已經遺漏的次數。|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||目前物件父系的路徑。|  
|**OBJECT_READ_KB**|**DBTYPE_I8**||自從服務啟動之後，物件讀取的資料累積值 (以 KB 為單位)。|  
|**OBJECT_READS**|**DBTYPE_I8**||自從服務啟動之後，物件執行之讀取作業的累積數目。|  
|**OBJECT_ROWS_RETURNED**|**DBTYPE_I8**||自從服務啟動之後，物件傳回呼叫端的資料列數目。|  
|**OBJECT_ROWS_SCANNED**|**DBTYPE_I8**||自從服務啟動之後，物件掃描的資料列數目。|  
|**OBJECT_VERSION**|**DBTYPE_I4**||物件的中繼資料版本號碼，每次改變物件時，這個號碼就會變更。|  
|**OBJECT_WRITE_KB**|**DBTYPE_I8**||自從服務啟動之後，物件寫入的資料累積值 (以 KB 為單位)。|  
|**OBJECT_WRITES**|**DBTYPE_I8**||自從服務啟動之後，物件執行之寫入作業的累積數目。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_OBJECT_ACTIVTY**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|OBJECT_PARENT_PATH|DBTYPE_WSTR|選擇性。|  
|OBJECT_ID|DBTYPE_WSTR|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
