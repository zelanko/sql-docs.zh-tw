---
title: DISCOVER_LOCKS 資料列集 |Microsoft 文件
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
helpviewer_keywords:
- DISCOVER_LOCKS rowset
ms.assetid: dea48167-212c-40b7-a416-434042a1b697
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 41af6b328b9083151bd3ef51bfc7df1d2986c1cf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032642"
---
# <a name="discoverlocks-rowset"></a>DISCOVER_LOCKS 資料列集
  提供有關伺服器上目前永久性鎖定的資訊。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_LOCKS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`LOCK_CREATION_TIME`|`DBTYPE_DBTIMESTAMP`||要求鎖定時的 UTC 伺服器時間。|  
|`LOCK_GRANT_TIME`|`DBTYPE_DBTIMESTAMP`||在資源上授與鎖定時的 UTC 伺服器時間。|  
|`LOCK_ID`|`DBTYPE_GUID`||鎖定的唯一識別碼，用以做為 GUID。|  
|`LOCK_OBJECT_ID`|`DBTYPE_WSTR`||鎖定物件的唯一識別碼。|  
|`LOCK_STATUS`|`DBTYPE_I4`||鎖定狀態。<br /><br /> 0 表示「等待鎖定物件」。<br /><br /> 1 表示 「已授與鎖定」。|  
|`LOCK_TRANSACTION_ID`|`DBTYPE_GUID`||交易的唯一識別碼，用以做為 GUID。|  
|`LOCK_TYPE`|`DBTYPE_I4`||鎖定類型的位元遮罩，如需詳細資訊，請參閱本主題的＜備註＞一節。|  
|`SPID`|`DBTYPE_I4`||工作階段識別碼。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DISCOVER_LOCKS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|選擇性。|  
|LOCK_TRANSACTION_ID|DBTYPE_GUID|選擇性。|  
|LOCK_OBJECT_ID|DBTYPE_WSTR|選擇性。|  
|LOCK_STATUS|DBTYPE_I4|選擇性。|  
|LOCK_TYPE|DBTYPE_I4|選擇性。|  
|LOCK_MIN_TOTAL_MS|DBTYPE_I8|選擇性。|  
  
## <a name="remarks"></a>備註  
  
## <a name="lock-types"></a>鎖定類型  
  
|鎖定名稱|ReplTest1|描述|  
|---------------|-----------|-----------------|  
|LOCK_NONE|0x0000000|沒有鎖定。|  
|LOCK_SESSION_LOCK|0x0000001|非使用中工作階段，不會干擾其他鎖定。|  
|LOCK_READ|0x0000002|在處理期間讀取鎖定。|  
|LOCK_WRITE|0x0000004|在處理期間寫入鎖定。|  
|LOCK_COMMIT_READ|0x0000008|確認鎖定，共用。|  
|LOCK_COMMIT_WRITE|0x0000010|確認鎖定，獨佔。|  
|LOCK_COMMIT_ABORTABLE|0x0000020|中止認可進度。|  
|LOCK_COMMIT_INPROGRESS|0x0000040|在進度中認可。|  
|LOCK_INVALID|0x0000080|無效的鎖定。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  