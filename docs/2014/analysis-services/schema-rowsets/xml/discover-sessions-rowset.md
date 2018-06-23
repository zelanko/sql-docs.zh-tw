---
title: DISCOVER_SESSIONS 資料列集 |Microsoft 文件
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
- DISCOVER_SESSIONS rowset
ms.assetid: 47a79542-3142-4e62-a66f-6c4dbfe0f5c0
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b85e563aacdfe2f520c185a3ddcbd0c4b5dc5453
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134025"
---
# <a name="discoversessions-rowset"></a>DISCOVER_SESSIONS 資料列集
  提供伺服器上目前已開啟的工作階段之資源使用量與活動的有關資訊。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_SESSIONS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`SESSION_COMMAND_COUNT`|`DBTYPE_I4`||工作階段開始之後開始執行的命令數目。|  
|`SESSION_CONNECTION_ID`|`DBTYPE_I4`||工作階段的連接識別碼。|  
|`SESSION_CPU_TIME_MS`|`DBTYPE_UI8`||工作階段開始之後，全部要求所耗用的 CPU 時間 (以毫秒為單位)。|  
|`SESSION_CURRENT_DATABASE`|`DBTYPE_WSTR`||目前命令執行所使用的資料庫名稱，或是上次執行的命令所使用的資料庫。|  
|`SESSION_ELAPSED_TIME_MS`|`DBTYPE_UI8`||工作階段開始之後所經過的時間 (以毫秒為單位)。|  
|`SESSION_ID`|`DBTYPE_WSTR`||做為 GUID 的工作階段唯一識別碼。|  
|`SESSION_IDLE_TIME_MS`|`DBTYPE_UI8`||工作階段開始之後的閒置時間 (以毫秒為單位)。|  
|`SESSION_LAST_COMMAND`|`DBTYPE_WSTR`||目前命令執行的文字或是上次命令執行的文字。|  
|`SESSION_LAST_COMMAND_CPU_TIME_MS`|`DBTYPE_UI8`||`SESSION_LAST_COMMAND` 所耗用的 CPU 時間 (以毫秒為單位)。|  
|`SESSION_LAST_COMMAND_ELAPSED_TIME_MS`|`DBTYPE_UI8`||`SESSION_LAST_COMMAND` 開始之後所經過的時間 (以毫秒為單位)。|  
|`SESSION_LAST_COMMAND_END_TIME`|`DBTYPE_DBTIMESTAMP`||上次命令執行完成時的 UTC 伺服器時間。|  
|`SESSION_LAST_COMMAND_START_TIME`|`DBTYPE_DBTIMESTAMP`||上次命令開始執行時的 UTC 伺服器時間。|  
|`SESSION_PROPERTIES`|`DBTYPE_WSTR`||保留供日後使用。|  
|`SESSION_READ_KB`|`DBTYPE_UI8`||工作階段啟動之後，從磁碟讀取的資料累積值 (以 KB 為單位)。|  
|`SESSION_READS`|`DBTYPE_UI8`||工作階段啟動之後，磁碟讀取的累積數目。|  
|`SESSION_SPID`|`DBTYPE_I4`||工作階段識別碼。|  
|`SESSION_START_TIME`|`DBTYPE_DBTIMESTAMP`||以伺服器之 UTC 時間啟動工作階段的日期和時間。|  
|`SESSION_STATUS`|`DBTYPE_I4`||工作階段的活動狀態。<br /><br /> 0 表示「閒置」：目前沒有正在進行的活動。<br /><br /> 1 表示「使用中」：工作階段正在執行某些要求的工作。<br /><br /> 2 表示「被封鎖」：工作階段正在等待某些資源繼續執行暫停的工作。<br /><br /> 3 表示 「 已取消 」: 工作階段已標記為已取消。|  
|`SESSION_USED_MEMORY`|`DBTYPE_I4`||工作階段使用的記憶體目前之大小 (以 KB 為單位)。 報告的值是依照 SPID 的 RAM 使用量，可壓縮和不可壓縮的記憶體之間並無差別。 不同於報告記憶體使用量的其他 DMVS，DISCOVER_SESSIONS 並不會依據類別區分記憶體使用量。<br /><br /> 請注意，SESSION_USED_MEMORY 往往會少報實際記憶體使用量，因為它會排除在多個工作階段之間共用的物件。  只有工作階段特有的物件會在記憶體計算中表示。|  
|`SESSION_USER_NAME`|`DBTYPE_WSTR`||工作階段使用者名稱。|  
|`SESSION_WRITE_KB`|`DBTYPE_UI8`||工作階段啟動之後，寫入磁碟的資料累積值 (以 KB 為單位)。|  
|`SESSION_WRITES`|`DBTYPE_UI8`||工作階段啟動之後，磁碟寫入的累積數目。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DISCOVER_SESSIONS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|SESSION_ID|DBTYPE_WSTR|選擇性。|  
|SESSION_SPID|DBTYPE_I4|選擇性。|  
|SESSION_CONNECTION_ID|DBTYPE_I4|選擇性。|  
|SESSION_USER_NAME|DBTYPE_WSTR|選擇性。|  
|SESSION_CURRENT_DATABASE|DBTYPE_WSTR|選擇性。|  
|SESSION_ELAPSED_TIME_MS|DBTYPE_UI8|選擇性。|  
|SESSION_CPU_TIME_MS|DBTYPE_UI8|選擇性。|  
|SESSION_IDLE_TIME_MS|DBTYPE_UI8|選擇性。|  
|SESSION_STATUS|DBTYPE_I4|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  