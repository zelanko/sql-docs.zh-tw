---
title: MSSQLSERVER_9955 | Microsoft Docs
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
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 274dfd7f0a8d54966a8788b6bb29a1389cd0c04b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver9955"></a>MSSQLSERVER_9955
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|9955|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|FTXT2_MSSEARCHACCESSDENY|  
|訊息文字|SQL Server 無法建立具名管道 '%ls' 來與全文檢索篩選背景程式進行通訊 (Windows 錯誤: %d)。 可能是篩選背景程式主機處理序已經有具名管道，系統資源不足，或是篩選背景程式帳戶群組的安全性識別碼 (SID) 查閱失敗。 若要解決這個錯誤，請終止任何執行中的全文檢索篩選背景程式處理序，並視需要重新設定全文檢索背景程式啟動器服務帳戶。|  
  
## <a name="explanation"></a>說明  
出現這則訊息的原因是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法建立具名管道來與全文檢索篩選背景程式進行通訊。 可能是篩選背景程式主機處理序已經有具名管道，系統資源不足，或是篩選背景程式帳戶群組的安全性識別碼 (SID) 查閱失敗。  
  
## <a name="user-action"></a>使用者動作  
若要解決這個錯誤，請終止任何執行中的全文檢索篩選背景程式處理序，並視需要使用 SQL Server 組態管理員來重新設定全文檢索背景程式的主機帳戶。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 組態管理員](~/relational-databases/sql-server-configuration-manager.md)  
[設定全文檢索篩選背景程式啟動器的服務帳戶](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[全文檢索搜尋](~/relational-databases/search/full-text-search.md)  
  
