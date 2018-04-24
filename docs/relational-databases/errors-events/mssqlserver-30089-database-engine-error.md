---
title: MSSQLSERVER_30089 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 9992 (Database Engine error)
ms.assetid: 188e5bde-6865-4740-a2b2-582be8f55c77
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1886662926ac1b888c6d1039d24f6adfe75513e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver30089"></a>MSSQLSERVER_30089
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|30089|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|IFTS_FDHOST_TERMINATEDABNORMAL|  
|訊息文字|全文檢索篩選背景程式主機 (FDHost) 處理序已異常停止。 如果設定錯誤或故障的語言元件 (例如斷字工具、字幹分析器或篩選器) 在全文檢索索引或查詢處理過程中造成無法復原的錯誤，就可能發生這種錯誤。 處理序將自動重新啟動。|  
  
## <a name="explanation"></a>說明  
全文檢索篩選背景程式主機遇到某個強制它異常停止的問題。 導致此問題發生的原因可能是格式不正確的文件、篩選或斷字工具中的錯誤，或篩選背景程式中的問題。  
  
## <a name="user-action"></a>使用者動作  
一般而言，背景程式會從錯誤中復原。 但是，如果它一直失敗，您就必須進行疑難排解。 請嘗試下列步驟來隔離問題：  
  
1.  如果您最近安裝過新的語言元件，請從系統中移除該元件。  
  
2.  查看搜耙記錄檔，以便識別無法進行全文檢索索引的任何新文件，然後移除該文件。  
  
## <a name="see-also"></a>另請參閱  
[sp_help_fulltext_system_components &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[設定及管理搜尋的斷詞工具與字幹分析器](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[設定及管理搜尋的篩選](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  
