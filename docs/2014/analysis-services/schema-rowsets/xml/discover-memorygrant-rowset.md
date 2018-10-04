---
title: DISCOVER_MEMORYGRANT 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: d254e42d-9918-47ce-b6df-47f1f0b432dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 21e24d1a7ab727eeb2c014870adb9928aed989dd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48154258"
---
# <a name="discovermemorygrant-rowset"></a>DISCOVER_MEMORYGRANT 資料列集
  傳回伺服器上目前執行作業所使用之內部記憶體配額授權的清單。 若要了解作業是否正在伺服器上執行，請使用 `Select * from $System.Discover_Jobs`。  
  
 **適用於：** 表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_MEMORYGRANT`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|描述|  
|-----------------|--------------------|-----------------|-----------------|  
|`MEMORY_ID`|**DBTYPE_I8**||識別記憶體配額授權的編號。 在單一 DISCOVER_MEMORYGRANT 要求內容中唯一的。|  
|`SPID`|`DBTYPE_I4`|必要項|您可以透過執行 `Select * from $System.Discover_Sessions` 取得的 SPID。|  
|`CreationTime`|`DBTYPE_I8 DBTYPE_DBTIMESTAMP`||授與配額的時間。|  
|`LastRequestTime`|**DBTYPE_DBTIMESTAMP**||上次修改配額要求的時間。|  
|`MemoryUsed`|`DBTYPE_I4`||依照配額使用的記憶體數量。|  
|`MemoryGranted`|`DBTYPE_I4`||供取得記憶體配額之作業使用的記憶體數量。|  
|`Blocked`|`DBTYPE_BOOL`||指出作業封鎖狀態的布林值。 True 表示已封鎖作業，等候另一個作業釋放足夠的配額以授與其配額要求。 False 表示作業已收到其配額而且可執行。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd23-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|MemoryGrant|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  
