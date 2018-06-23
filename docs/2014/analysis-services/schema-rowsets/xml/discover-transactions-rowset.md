---
title: DISCOVER_TRANSACTIONS 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 85789177-c5df-4336-a90c-c20d69277ab4
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3869d4f8cd3adf96bd006a8669d7d82778b02450
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029942"
---
# <a name="discovertransactions-rowset"></a>DISCOVER_TRANSACTIONS 資料列集
  傳回系統上目前的暫止交易集。  
  
 **適用於：** 表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_TRANSACTIONS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|描述|  
|-----------------|--------------------|-----------------|  
|`TRANSACTION_ID`|`DBTYPE_WSTR`|做為 GUID 的交易唯一識別碼。|  
|`TRANSACTION_SESSION_ID`|`DBTYPE_WSTR`|做為 GUID 的交易工作階段唯一識別碼。|  
|`TRANSACTION_START_TIME`|`DBTYPE_DBTIMESTAMP`|啟動交易時的伺服器 UTC 日期和時間。|  
|`TRANSACTION_ELAPSED_TIME_MS`|`DBTYPE_I8`|交易啟動以後所經過的時間 (以毫秒為單位)。|  
|`TRANSACTION_CPU_TIME_MS`|`DBTYPE_I8`|交易開始之後，所有要求所耗用的 CPU 時間 (以毫秒為單位)。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DISCOVER_TRANSACTIONS` 資料列集。  
  
|**資料行名稱**|**類型指標**|**限制狀態**|  
|---------------------|------------------------|---------------------------|  
|`ID`|`DBTYPE_WSTR`|選擇性。|  
|`SESSION_ID`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd28-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRANSACTIONS|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  