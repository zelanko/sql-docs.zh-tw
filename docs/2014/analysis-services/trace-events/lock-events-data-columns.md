---
title: 鎖定事件資料行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c223157f-41a0-405c-bc1a-41c999506936
caps.latest.revision: 4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3160ffa917a0f3eb3d6a80f81d6218c8f45525e3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167569"
---
# <a name="lock-events-data-columns"></a>鎖定事件資料行
  鎖定事件類別目錄含有下列事件類別：  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|50|死結|有關處於死結狀態、目前鎖定的資訊。|  
|51|鎖定逾時。|有關最近逾時之鎖定的資訊|  
|52|取得的鎖定|有關最近取得之鎖定的資訊|  
|53|釋放的鎖定|有關最近釋放之鎖定的資訊|  
|54|正在等候的鎖定|有關正在等候其他鎖定之鎖定的資訊|  
  
 下表列出此事件類別的資料行。  
  
## <a name="deadlock"></a>死結  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="lock-timeout"></a>鎖定逾時。  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|Duration|5|2|事件所花費的時間量 (以毫秒為單位)。|  
|IntegerData|10|1|整數資料。|  
|ObjectType|12|1|物件類型。|  
|ObjectPath|14|8|物件路徑。 以物件的父系開頭之父系清單 (以逗號分隔)。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|NTUserName|32|8|Windows 使用者名稱。|  
|NTDomainName|33|8|使用者所隸屬的 Windows 網域。|  
|SessionID|39|8|工作階段 GUID。|  
|NTCanonicalUserName|40|8|標準格式的使用者名稱。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|伺服器處理序識別碼。 這可唯一識別出使用者工作階段， 直接對應到 XML/A 所使用的工作階段 GUID。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="lock-acquired"></a>取得的鎖定  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|NTUserName|32|8|Windows 使用者名稱。|  
|NTDomainName|33|8|使用者所隸屬的 Windows 網域。|  
|ClientHostName|35|8|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|ApplicationName|37|8|建立伺服器連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|SessionID|39|8|工作階段 GUID。|  
|NTCanonicalUserName|40|8|標準格式的使用者名稱。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|伺服器處理序識別碼。 這可唯一識別出使用者工作階段， 直接對應到 XML/A 所使用的工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="lock-released"></a>釋放的鎖定  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|NTUserName|32|8|Windows 使用者名稱。|  
|NTDomainName|33|8|使用者所隸屬的 Windows 網域。|  
|ClientHostName|35|8|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|ApplicationName|37|8|建立伺服器連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|SessionID|39|8|工作階段 GUID。|  
|NTCanonicalUserName|40|8|標準格式的使用者名稱。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|伺服器處理序識別碼。 這可唯一識別出使用者工作階段， 直接對應到 XML/A 所使用的工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="lock-waiting"></a>正在等候的鎖定  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|NTUserName|32|8|Windows 使用者名稱。|  
|NTDomainName|33|8|使用者所隸屬的 Windows 網域。|  
|ClientHostName|35|8|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|ApplicationName|37|8|建立伺服器連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|SessionID|39|8|工作階段 GUID。|  
|NTCanonicalUserName|40|8|標準格式的使用者名稱。 例如，engineering.microsoft.com/software/someone。|  
|SPID|41|1|伺服器處理序識別碼。 這可唯一識別出使用者工作階段， 直接對應到 XML/A 所使用的工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [鎖定事件類別目錄](lock-events-category.md)  
  
  
