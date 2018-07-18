---
title: MSSQLSERVER_30053 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 8ad23889-e243-4bd7-bc3e-150403399d89
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d7f14aed745e4421a6ea43746d1286712834a47d
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323339"
---
# <a name="mssqlserver30053"></a>MSSQLSERVER_30053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|30053|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|訊息文字|全文檢索查詢字串的斷詞工作逾時。 如果斷詞工具處理全文檢索查詢字串的時間太長，或伺服器上有大量查詢正在執行，就可能發生這個錯誤。 請嘗試在負載較輕時再執行一次查詢。|  
  
## <a name="explanation"></a>說明  
斷詞逾時錯誤可能會在下列情況中發生：  
  
-   查詢語言的斷詞工具設定不正確。例如，其登錄設定不正確。  
  
-   斷詞工具由於特定的查詢字串而無法運作。  
  
-   斷詞工具針對特定的查詢字串傳回太多資料。 資料過多會被系統視為可能的緩衝區滿溢攻擊，因而關閉主控斷詞服務的篩選背景程式處理序 (fdhost.exe)。  
  
-   篩選背景程式處理序的組態不正確。  
  
    最常見的組態問題是密碼逾期或讓篩選背景程式帳戶無法登入的網域原則。  
  
-   伺服器執行個體正在執行非常繁重的查詢工作負載。例如，斷詞工具處理全文檢索查詢字串的時間太長，或伺服器上有大量查詢正在執行。 請注意，這是可能性最低的原因。  
  
## <a name="user-action"></a>使用者動作  
請選取適用於逾時可能原因的使用者動作，如下所示：  
  
|可能原因|使用者動作|  
|------------------|---------------|  
|查詢語言的斷詞工具設定不正確。|如果您正在使用協力廠商斷詞工具，可能是作業系統的註冊不正確。 在此情況下，請重新註冊斷詞工具。 如需詳細資訊，請參閱[將搜索所使用的斷詞工具還原為舊版](~/relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)。|  
|斷詞工具由於特定的查詢字串而無法運作。|如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援斷詞工具，請連絡 Microsoft 客戶服務及支援中心。|  
|斷詞工具針對特定的查詢字串傳回太多資料。|如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援斷詞工具，請連絡 Microsoft 客戶服務及支援中心。|  
|篩選背景程式處理序的組態不正確。|請確定您使用最新的密碼，而且網域原則並未讓篩選背景程式帳戶無法登入。|  
|伺服器執行個體正在執行非常繁重的查詢工作負載。|請嘗試在負載較輕時再執行一次查詢。|  
  
## <a name="see-also"></a>另請參閱  
[設定全文檢索篩選背景程式啟動器的服務帳戶](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[全文檢索搜尋](~/relational-databases/search/full-text-search.md)  
[sp_help_fulltext_system_components &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[設定及管理搜尋的斷詞工具與字幹分析器](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[設定及管理搜尋的篩選](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  
