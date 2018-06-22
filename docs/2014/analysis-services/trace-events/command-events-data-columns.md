---
title: 命令事件資料行 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Command Events event category
ms.assetid: 7169f1e2-c6be-4d8c-b147-25719b84bc2c
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 290c9ca23a71c43d16f29e0bd0e6d1f595b6df14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022239"
---
# <a name="command-events-data-columns"></a>命令事件資料行
  下表列出 [命令事件] 事件類別目錄中，每種事件類別的資料行。  
  
 [命令事件] 事件類別目錄含有下列事件類別：  
  
-   [命令開始類別](#bkmk_1)  
  
-   [命令結束類別](#bkmk_2)  
  
 下表列出每一個這類事件類別的資料行。  
  
##  <a name="bkmk_1"></a> 命令開始類別—資料行  
  
|資料行|描述|  
|-----------------|-----------------|  
|ConnectionID|包含與命令事件相關聯的唯一連接識別碼。|  
|TextData|包含與命令事件相關聯的文字資料。|  
|ServerName|包含發生命令事件之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
|CurrentTime|包含命令事件的目前時間。|  
|DatabaseName|包含執行命令之資料庫的名稱。|  
|EventSubclass|包含命令事件中之事件的類別。 值為：<br /><br /> 0：建立<br />1：變更<br />2：刪除<br />3：處理<br />4：DesignAggregations<br />5：WBInsert<br />6：WBUpdate<br />7：WBDelete<br />8：備份<br />9：還原<br />10：MergePartitions<br />11：訂閱<br />12：批次<br />13：BeginTransaction<br />14：CommitTransaction<br />15：RollbackTransaction<br />16：GetTransactionState<br />17：取消<br />18：同步處理<br />19：Import80MiningModels<br />20：附加<br />21︰卸離<br />22：SetAuthContext<br />23：ImageLoad<br />24：ImageSave<br />10000：其他|  
|NTUserName|包含與命令事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|RequestProperties|包含與命令事件相關聯的 XML for Analysis (XMLA) 要求屬性。|  
|SPID|包含伺服器處理序識別碼 (SPID)，它會唯一識別與命令事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|StartTime|包含啟動命令事件的時間 (如果有的話)。|  
|SessionType|包含造成作業的實體。|  
|NTDomainName|包含與物件權限事件相關聯的 Windows 網域帳戶。|  
|ClientProcessID|包含與命令事件相關聯的唯一用戶端處理序識別碼。|  
  
##  <a name="bkmk_2"></a> 命令結束類別—資料行  
  
|資料行|描述|  
|-----------------|-----------------|  
|ConnectionID|包含與命令事件相關聯的唯一連接識別碼。|  
|TextData|包含與命令事件相關聯的文字資料。|  
|ServerName|包含發生命令事件之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|  
|CurrentTime|包含命令事件的目前時間。 篩選的格式為 *YYYY*-*MM*-*DD* 和 *YYYY*-*MM*-*DD HH*:*MM*:*SS*。|  
|DatabaseName|包含執行命令之資料庫的名稱。|  
|Duration|包含在命令開始和命令結束事件之間的大約時間量。|  
|EndTime|包含命令事件結束的時間。 篩選的格式為 *YYYY*-*MM*-*DD* 和 *YYYY*-*MM*-*DD HH*:*MM*:*SS*。|  
|EventSubclass|包含命令事件中之事件的類別。 值為：<br /><br /> 0：建立<br />1：變更<br />2：刪除<br />3：處理<br />4：DesignAggregations<br />5：WBInsert<br />6：WBUpdate<br />7：WBDelete<br />8：備份<br />9：還原<br />10：MergePartitions<br />11：訂閱<br />12：批次<br />13：BeginTransaction<br />14：CommitTransaction<br />15：RollbackTransaction<br />16：GetTransactionState<br />17：取消<br />18：同步處理<br />19：Import80MiningModels<br />20：附加<br />21︰卸離<br />22：SetAuthContext<br />23：ImageLoad<br />24：ImageSave<br />10000：其他|  
|NTCanonicalUserName|包含與命令事件相關聯的 Windows 使用者名稱。 使用者名稱採用標準格式。 例如，engineering.microsoft.com/software/user。|  
|NTUserName|包含與命令事件相關聯的 Windows 使用者帳戶。|  
|SPID|包含伺服器處理序識別碼 (SPID)，它會唯一識別與命令事件相關聯的使用者工作階段。 SPID 直接對應到 XMLA 使用的工作階段 GUID。|  
|StartTime|包含命令結束事件的啟動時間 (如果有的話)。|  
|CPUTime|包含命令開始事件時間和命令結束事件時間兩者之間，處理序所使用的 CPU 時間量 (以毫秒為單位)。|  
|錯誤|包含與命令事件相關聯之錯誤的錯誤號碼。|  
|Severity|包含與命令事件相關聯之例外狀況的嚴重性層級。 值為：<br /><br /> 0 = 成功<br /><br /> 1 = 參考資訊<br /><br /> 2 = 警告<br /><br /> 3 = 錯誤|  
|成功|包含命令事件的成功或失敗。 值為：<br /><br /> 0 = 失敗<br /><br /> 1 = 成功|  
|SessionType|包含造成與命令結束事件相關聯之作業的實體。|  
|NTDomainName|包含與命令事件相關聯的 Windows 網域帳戶。|  
|ClientProcessID|包含與命令事件相關聯的唯一用戶端處理序識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [命令事件的事件類別目錄](command-events-event-category.md)  
  
  