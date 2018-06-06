---
title: 查詢事件資料行 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 56a945a1130753fc2feb08a89bd4f6e2676f1bd0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="queries-events-data-columns"></a>查詢事件資料行
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [查詢事件] 事件類別目錄具有下列事件類別：  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|9|查詢開始|查詢開始。|  
|10|查詢結束|查詢結束。|  
  
 下表列出每一個這類事件類別的資料行。  
  
## <a name="query-begin-classdata-columns"></a>查詢開始類別—資料行  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊。<br /><br /> 0：MDXQuery<br /><br /> 1：DMXQuery<br /><br /> 2：SQLQuery<br /><br /> 3：DAXQuery|  
|CurrentTime|2|5|包含事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|ConnectionID|25|1|包含與查詢事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|包含執行查詢之資料庫的名稱。|  
|NTUserName|32|8|包含與查詢事件相關聯的 Windows 使用者名稱。|  
|NTDomainName|33|8|包含與查詢事件相關聯的 Windows 網域帳戶。|  
|ClientProcessID|36|1|包含用戶端應用程式的處理序識別碼。|  
|ApplicationName|37|8|包含建立伺服器之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|SessionID|39|8|包含 XMLA 要求的工作階段唯一識別碼。|  
|NTCanonicalUserName|40|8|包含與查詢事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與查詢事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|TextData|42|9|包含與查詢事件相關聯的文字資料。|  
|ServerName|43|8|包含發生查詢事件之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
|RequestParameters|44|9|包含與查詢事件相關聯之參數化查詢和命令的參數。|  
|RequestProperties|45|9|包含 XMLA 要求的屬性。|  
  
## <a name="query-end-classdata-columns"></a>查詢結束類別—資料行  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊。<br /><br /> 0：MDXQuery<br /><br /> 1：DMXQuery<br /><br /> 2：SQLQuery<br /><br /> 3：DAXQuery|  
|CurrentTime|2|5|包含事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|包含事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|包含事件所經歷的時間量 (以毫秒為單位)。|  
|CPUTime|6|2|包含事件所使用的 CPU 時間量 (以毫秒為單位)。|  
|Severity|22|1|包含與查詢事件相關聯之例外狀況的嚴重性層級。 值為：<br /><br /> 0 = 成功<br /><br /> 1 = 參考資訊<br /><br /> 2 = 警告<br /><br /> 3 = 錯誤|  
|成功|23|1|包含查詢事件的成功或失敗。 值為：<br /><br /> 0 = 失敗<br /><br /> 1 = 成功|  
|錯誤|24|1|包含與查詢事件相關聯之錯誤的錯誤號碼。|  
|ConnectionID|25|1|包含與查詢事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|包含執行查詢之資料庫的名稱。|  
|NTUserName|32|8|包含與查詢事件相關聯的 Windows 使用者名稱。|  
|NTDomainName|33|8|包含與查詢事件相關聯的 Windows 網域帳戶。|  
|ClientProcessID|36|1|包含用戶端應用程式的處理序識別碼。|  
|ApplicationName|37|8|包含建立伺服器之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|SessionID|39|8|包含 XMLA 要求的工作階段唯一識別碼。|  
|NTCanonicalUserName|40|8|包含與查詢事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與查詢事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|TextData|42|9|包含與查詢事件相關聯的文字資料。|  
|ServerName|43|8|包含發生查詢事件之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [查詢事件類別目錄](../../analysis-services/trace-events/queries-events-category.md)  
  
  
