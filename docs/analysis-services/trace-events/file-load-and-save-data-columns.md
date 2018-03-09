---
title: "檔案載入及儲存資料行 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 0101e809-d6ea-4d0c-95ec-65dd77acf665
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8f10d93cf8670da5e14d2fb65193c43398ad1c6c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="file-load-and-save-data-columns"></a>檔案載入及儲存資料行
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
檔案載入和儲存事件類別目錄具有下列事件類別：  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|90|檔案載入開始|檔案載入開始。|  
|91|檔案載入結束|檔案載入結束。|  
|92|檔案儲存開始|檔案儲存開始。|  
|93|檔案儲存結束|檔案儲存結束|  
|94|PageOut 開始|PageOut 開始。|  
|95|PageOut 結束|PageOut 結束|  
|96|PageIn 開始|PageIn 開始。|  
|97|PageIn 結束|PageIn 結束|  
  
 下表列出此事件類別的資料行。  
  
## <a name="file-load-begin"></a>檔案載入開始  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|JobID|7|1|進度的作業識別碼。|  
|SessionType|8|8|工作階段類型 (造成作業的實體)。|  
|ObjectID|11|8|物件識別碼 (請注意這是一個字串)。|  
|ObjectType|12|1|物件類型。|  
|ObjectName|13|8|物件名稱。|  
|ObjectPath|14|8|物件路徑。 以物件的父系開頭之父系清單 (以逗號分隔)。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|SessionID|39|8|工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="file-load-end"></a>檔案載入結束  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|事件所花費的時間量 (以毫秒為單位)。|  
|JobID|7|1|進度的作業識別碼。|  
|SessionType|8|8|工作階段類型 (造成作業的實體)。|  
|IntegerData|10|1|整數資料。|  
|ObjectID|11|8|物件識別碼 (請注意這是一個字串)。|  
|ObjectType|12|1|物件類型。|  
|ObjectName|13|8|物件名稱。|  
|ObjectPath|14|8|物件路徑。 以物件的父系開頭之父系清單 (以逗號分隔)。|  
|Severity|22|1|例外狀況的嚴重性層級。|  
|成功|23|1|1 = 成功。 0 = 失敗 (例如，1 表示權限檢查成功，而 0 表示該檢查失敗)。|  
|錯誤|24|1|給定事件的錯誤號碼。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|SessionID|39|8|工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="file-save-begin"></a>檔案儲存開始  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|JobID|7|1|進度的作業識別碼。|  
|SessionType|8|8|工作階段類型 (造成作業的實體)。|  
|ObjectID|11|8|物件識別碼 (請注意這是一個字串)。|  
|ObjectType|12|1|物件類型。|  
|ObjectName|13|8|物件名稱。|  
|ObjectPath|14|8|物件路徑。 以物件的父系開頭之父系清單 (以逗號分隔)。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|SessionID|39|8|工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱|  
  
## <a name="file-save-end"></a>檔案儲存結束  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|事件所花費的時間量 (以毫秒為單位)。|  
|JobID|7|1|進度的作業識別碼。|  
|SessionType|8|8|工作階段類型 (造成作業的實體)。|  
|IntegerData|10|1|整數資料。|  
|ObjectID|11|8|物件識別碼 (請注意這是一個字串)。|  
|ObjectType|12|1|物件類型。|  
|ObjectName|13|8|物件名稱。|  
|ObjectPath|14|8|物件路徑。 以物件的父系開頭之父系清單 (以逗號分隔)。|  
|Severity|22|1|例外狀況的嚴重性層級。|  
|成功|23|1|1 = 成功。 0 = 失敗 (例如，1 表示權限檢查成功，而 0 表示該檢查失敗)。|  
|錯誤|24|1|給定事件的錯誤號碼。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|SessionID|39|8|工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="pageout-begin"></a>PageOut 開始  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|JobID|7|1|進度的作業識別碼。|  
|SessionType|8|8|工作階段類型 (造成作業的實體)。|  
|ObjectID|11|8|物件識別碼 (請注意這是一個字串)。|  
|ObjectType|12|1|物件類型。|  
|ObjectName|13|8|物件名稱。|  
|ObjectPath|14|8|物件路徑。 以物件的父系開頭之父系清單 (以逗號分隔)。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|SessionID|39|8|工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="pageout-end"></a>PageOut 結束  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|事件所花費的時間量 (以毫秒為單位)。|  
|JobID|7|1|進度的作業識別碼。|  
|SessionType|8|8|工作階段類型 (造成作業的實體)。|  
|IntegerData|10|1|整數資料。|  
|ObjectID|11|8|物件識別碼 (請注意這是一個字串)。|  
|ObjectType|12|1|物件類型。|  
|ObjectName|13|8|物件名稱。|  
|ObjectPath|14|8|物件路徑。 以物件的父系開頭之父系清單 (以逗號分隔)。|  
|Severity|22|1|例外狀況的嚴重性層級。|  
|成功|23|1|1 = 成功。 0 = 失敗 (例如，1 表示權限檢查成功，而 0 表示該檢查失敗)。|  
|錯誤|24|1|給定事件的錯誤號碼。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|SessionID|39|8|工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="pagein-begin"></a>PageIn 開始  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|JobID|7|1|進度的作業識別碼。|  
|SessionType|8|8|工作階段類型 (造成作業的實體)。|  
|ObjectID|11|8|物件識別碼 (請注意這是一個字串)。|  
|ObjectType|12|1|物件類型。|  
|ObjectName|13|8|物件名稱。|  
|ObjectPath|14|8|物件路徑。 以物件的父系開頭之父系清單 (以逗號分隔)。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|SessionID|39|8|工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="pagein-end"></a>PageIn 結束  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|CurrentTime|2|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|事件的開始時間 (如果可以取得的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|事件所花費的時間量 (以毫秒為單位)。|  
|JobID|7|1|進度的作業識別碼。|  
|SessionType|8|8|工作階段類型 (造成作業的實體)。|  
|IntegerData|10|1|整數資料。|  
|ObjectID|11|8|物件識別碼 (請注意這是一個字串)。|  
|ObjectType|12|1|物件類型。|  
|ObjectName|13|8|物件名稱。|  
|ObjectPath|14|8|物件路徑。 以物件的父系開頭之父系清單 (以逗號分隔)。|  
|Severity|22|1|例外狀況的嚴重性層級。|  
|成功|23|1|1 = 成功。 0 = 失敗 (例如，1 表示權限檢查成功，而 0 表示該檢查失敗)。|  
|錯誤|24|1|給定事件的錯誤號碼。|  
|ConnectionID|25|1|唯一的連接識別碼。|  
|DatabaseName|28|8|正在執行使用者之陳述式的資料庫名稱。|  
|ClientProcessID|36|1|用戶端應用程式的處理序識別碼。|  
|SessionID|39|8|工作階段 GUID。|  
|TextData|42|9|與事件相關的文字資料。|  
|ServerName|43|8|產生事件的伺服器名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [檔案載入及儲存事件類別目錄](../../analysis-services/trace-events/file-load-and-save-event-category.md)  
  
  
