---
title: 日期和時間格式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- time data types [Integration Services]
- fast parse [Integration Services]
- date data types
- date and time formats for fast parse
ms.assetid: bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 26bd117cb63ccc623ee54f3370e1d07237de9c52
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059650"
---
# <a name="date-and-time-formats"></a>日期和時間格式
  快速剖析提供一組快速、簡單的常式用以剖析資料。 快速剖析可支援下列格式的日期和時間資料類型。  
  
## <a name="date-data-types"></a>日期資料類型  
 快速剖析支援下列字串格式的日期資料：  
  
-   包含開頭空白字元的日期格式。 例如，值 " 2004- 02-03"為有效。  
  
-   ISO 8601 格式，如下表中所列：  
  
    |[格式]|描述|  
    |------------|-----------------|  
    |YYYYMMDD<br /><br /> YYYY-MM-DD|四位數年份、兩位數月份和兩位數天數的基本格式與擴充格式。 在擴充格式中，日期各部份以連字號 (-) 分隔。|  
    |YYYY-MM|降低有效位數的四位數年份和兩位數月份之基本格式與擴充格式。 在擴充格式中，日期各部份以連字號 (-) 分隔。|  
    |YYYY|降低有效位數的格式為四位數年份。|  
  
 快速剖析不支援下列格式的日期資料：  
  
-   字母月份值。 例如，日期格式 Oct-31-2003 無效。  
  
-   模稜兩可的格式，例如 DD-MM-YYYY 和 MM-DD-YYYY。 例如，日期 03-04-1995 和日期 04-03-1995 無效。  
  
-   四位數日曆年度和一年中三位數天數的基本截斷格式與擴充截斷格式 (YYYYDDD 和 YYYY-DDD)。  
  
-   四位數年份、一年中兩位數週數和一週中一位數天數的基本格式與擴充格式 (YYYYWwwD 和 YYYY-Www-D)。  
  
-   年份和週日期的基本截斷格式與擴充截斷格式為四位數年份和兩位數週數 (YYYWww 和 YYYY-Www)。  
  
 快速剖析會以 DT_DBDATE 輸出資料。 將填補以截斷格式表示的日期值。 例如，YYYY 會變為 YYYY0101。  
  
 如需詳細資訊，請參閱 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。  
  
## <a name="time-data-type"></a>時間資料類型  
 快速剖析支援下列字串格式的時間資料：  
  
-   包含開頭空白字元的時間格式。 例如，值「 10:24」為有效。  
  
-   24 小時格式。 快速剖析不支援 AM 和 PM 標記法。  
  
-   ISO 8601 時間格式，如下表中所列：  
  
    |[格式]|描述|  
    |------------|-----------------|  
    |HHMISS<br /><br /> HH:MI:SS|四位數小時、兩位數分鐘和兩位數秒鐘的基本格式與擴充格式。 在擴充格式中，時間各部份以冒號 (:) 分隔。|  
    |HHMI<br /><br /> HH:MI|兩位數小時和兩位數分鐘之基本截斷格式與擴充截斷格式。 在擴充格式中，時間各部份以冒號 (:) 分隔。|  
    |HH|兩位數小時的截斷格式。|  
    |00:00:00<br /><br /> 000000<br /><br /> 0000<br /><br /> 00<br /><br /> 240000<br /><br /> 24:00:00<br /><br /> 2400<br /><br /> 24|午夜格式。|  
  
-   指定時區的時間格式，如下表中所列：  
  
    |[格式]|描述|  
    |------------|-----------------|  
    |+HH:MI<br /><br /> +HHMI|基本格式及擴充格式，指出要加入至「國際標準時間」(UTC) 以取得本地時間的小時和分鐘數。|  
    |-HH:MI<br /><br /> -HHMI|基本格式及擴充格式，指出要從 UTC 減去以取得本地時間的小時和分鐘數。|  
    |+HH|截斷格式，指出要加入至 UTC 以取得本地時間的小時數。|  
    |-HH|截斷格式，指出要從 UTC 減去以取得本地時間的小時數。|  
    |Z|0 的值，指出時間是以 UTC 表示。|  
  
     所有時間和日期/時間資料的格式都可以包含時區元素。 不過，除非資料是 DT_DBTIMESTAMPOFFSET 類型，否則系統會忽略時區值。 如需詳細資訊，請參閱 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。  
  
     在包含時區元素的格式中，在時間元素和時區元素之間沒有空格，如以下範例所示：  
  
     HH:MI:SS[+HH:MI]  
  
     前述範例中的方括號表示時區值是選擇性的。  
  
-   包含小數的時間格式，如下表中所列：  
  
    |[格式]|描述|  
    |------------|-----------------|  
    |HH[.nnnnnnn]|n 是介於 0 和 9999999 之間且代表小數時數的值。 方括號表示此值是選擇性的。<br /><br /> 例如，值 12.750 表示 12:45。|  
    |HHMI[.nnnnnnn]<br /><br /> HH:MI[.nnnnnnn]|n 是介於 0 和 9999999 之間且代表小數分鐘數的值。 方括號表示此值是選擇性的。<br /><br /> 例如，值 1220.500 表示 12:20:30。|  
    |HHMISS[.nnnnnnn]<br /><br /> HH:MI:SS[.nnnnnnn]|n 是介於 0 和 9999999 之間且代表小數秒數的值。 方括號表示此值是選擇性的。<br /><br /> 例如，值 122040.250 表示 12:20:40.15。|  
  
    > [!NOTE]  
    >  前述表格中時間格式的小數分隔符號可以是小數點或逗號。  
  
-   包含閏秒 (Leap Second) 的時間值，如下列範例所示：  
  
     23:59:60[.0000000]  
  
     235960[.0000000]  
  
 快速剖析會以 DT_DBTIME 和 DT_DBTIME2 輸出字串。 將填補以截斷格式表示的時間值。 例如，HH:MI 會變為 HH:MM:00.000。  
  
 如需詳細資訊，請參閱 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。  
  
## <a name="datetime-data-type"></a>日期/時間資料類型  
 快速剖析支援下列字串格式的日期/時間資料：  
  
-   包含開頭空白字元的格式。 例如，值 "  2003-01-10T203910" 有效。  
  
-   有效日期格式和有效時間格式的組合會以大寫的 T 及有效的時區格式分隔，例如 YYYYMMDDT[HHMISS][+HH:MI]。 時間和時區值不是必要值。 例如，"2003-10-14" 是有效值。  
  
 快速剖析不支援時間間隔。 例如，格式為 YYYYMMDDThhmmss/YYYYMMDDThhmmss 之開始日期和時間以及結束日期和時間所識別的時間間隔將無法剖析。  
  
 快速剖析會以 DT_DATE、DT_DBTIMESTAMP、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 輸出字串。 將填補以截斷格式表示的日期/時間值。 下表列出針對遺失的日期和時間部分而加入的值。  
  
|日期/時間部分|填補|  
|---------------------|-------------|  
|秒|加入 00。|  
|分鐘|加入 00:00。|  
|Hour|加入 00:00:00。|  
|Day|加入 01 做為此月的某個日期。|  
|Month|加入 01 做為此年份的某個月份。|  
  
 如需詳細資訊，請參閱 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。  
  
  
