---
title: "通知事件資料行 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Notification Events event category
ms.assetid: 0ecf06da-1586-415a-9da8-60d4c634f030
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 39c93ff427048fe1893dd78f8fe35abc0b52885b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="notification-events-data-columns"></a>通知事件資料行
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]通知事件是不的使用者直接造成的事件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 例如，通知是因為使用者更新主動式快取的基礎資料表而發生。  
  
 [通知事件] 事件類別目錄具有下列事件類別：  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|39|通知|通知事件。|  
|40|使用者定義|使用者定義事件。|  
  
 下列資料表列出事件類別的資料行。  
  
## <a name="notification"></a>通知  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|事件子類別提供有關每個事件類別的額外資訊。<br /><br /> 下列 **子類別識別碼**：<br />                      **子類別名稱** 組定義如下︰<br /><br /> 0：主動式快取開始<br /><br /> 1：主動式快取結束<br /><br /> 2：已啟動飛行記錄器<br /><br /> 3：已停止飛行記錄器<br /><br /> 4：已更新組態屬性<br /><br /> 5：SQL 追蹤<br /><br /> 6：已建立物件<br /><br /> 7：已刪除物件<br /><br /> 8：已改變物件<br /><br /> 9：主動式快取輪詢開始<br /><br /> 10：主動式快取輪詢結束<br /><br /> 11：飛行記錄器快照集開始<br /><br /> 12：飛行記錄器快照集結束<br /><br /> 13：主動式快取：可通知物件已更新<br /><br /> 14：延遲處理：開始處理<br /><br /> 15：延遲處理：已完成處理<br /><br /> 16：SessionOpened 事件開始<br /><br /> 17：SessionOpened 事件結束<br /><br /> 18：SessionClosing 事件開始<br /><br /> 19：SessionClosing 事件結束<br /><br /> 20：CubeOpened 事件開始<br /><br /> 21：CubeOpened 事件結束<br /><br /> 22：CubeClosing 事件開始<br /><br /> 23：CubeClosing 事件結束<br /><br /> 24：已要求交易中止|  
|CurrentTime|2|5|包含通知事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|StartTime|3|5|包含事件開始的時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|EndTime|4|5|包含事件結束的時間。 此資料行不會因啟動的事件類別 (如 SQL:BatchStarting 或 SP:Starting) 而擴展。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|有效期間|5|2|包含事件所花費的時間量 (以毫秒為單位)。|  
|IntegerData|10|1|包含與通知事件相關聯的整數資料。 當 EventSubclass 資料行為 8 時，其值如下：<br /><br /> 1 = 已建立<br /><br /> 2 = 已刪除<br /><br /> 3 = 已變更物件的屬性<br /><br /> 4 = 已變更物件之子系的屬性<br /><br /> 6 = 已加入子系<br /><br /> 7 = 已刪除子系<br /><br /> 8 = 已完全處理物件<br /><br /> 9 = 已部份處理物件<br /><br /> 10 = 未處理物件<br /><br /> 11 = 完全最佳化物件<br /><br /> 12 = 部分最佳化物件<br /><br /> 13 = 物件未最佳化|  
|ObjectID|11|8|包含為其發出此通知的物件識別碼；這是一個字串值。|  
|ObjectType|12|1|包含與通知事件相關聯的物件類型。|  
|ObjectName|13|8|包含與通知事件相關聯的物件名稱。|  
|ObjectPath|14|8|包含與通知事件相關聯的物件路徑。 路徑是以父系的逗號分隔清單傳回，清單開頭是物件的父系。|  
|ObjectReference|15|8|包含進度報表結束事件的物件參考。 物件參考是由所有父系使用標記來描述物件，而編碼成 XML。|  
|ConnectionID|25|1|包含與通知事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|包含發生通知事件之資料庫的名稱。|  
|NTUserName|32|8|包含與通知事件相關聯的 Windows 使用者名稱。|  
|NTDomainName|33|8|使用者所隸屬的 Windows 網域。|  
|SessionID|39|8|包含與通知事件相關聯的工作階段識別碼。|  
|NTCanonicalUserName|40|8|包含與通知事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與通知事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|TextData|42|9|包含與通知事件相關聯的文字資料。|  
|ServerName|43|8|包含發生通知事件之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
|RequestProperties|45|9|包含 XMLA 要求的屬性。|  
  
## <a name="user-defined"></a>使用者定義  
  
|**資料行名稱**|**資料行識別碼**|**資料行類型**|**資料行描述**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|事件類別用於將事件分類。|  
|EventSubclass|1|1|提供有關每個事件類別的額外資訊的特定使用者事件子類別。|  
|CurrentTime|2|5|包含通知事件的目前時間 (如果有的話)。 篩選所需的格式為 'YYYY-MM-DD' 與 'YYYY-MM-DD HH:MM:SS'。|  
|IntegerData|10|1|特定的使用者定義事件資訊。|  
|ConnectionID|25|1|包含與通知事件相關聯的唯一連接識別碼。|  
|DatabaseName|28|8|包含發生通知事件之資料庫的名稱。|  
|NTUserName|32|8|包含與通知事件相關聯的 Windows 使用者名稱。|  
|NTDomainName|33|8|使用者所隸屬的 Windows 網域。|  
|SessionID|39|8|包含與通知事件相關聯的工作階段識別碼。|  
|NTCanonicalUserName|40|8|包含與通知事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|SPID|41|1|包含伺服器處理序識別碼 (SPID)，它會唯一識別與通知事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|TextData|42|9|包含與通知事件相關聯的文字資料。|  
|ServerName|43|8|包含發生通知事件之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
  
## <a name="see-also"></a>請參閱  
 [Notification Events Event Category](../../analysis-services/trace-events/notification-events-event-category.md)  
  
  
