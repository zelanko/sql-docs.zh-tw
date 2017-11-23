---
title: "什麼 &#39; s CLR 整合的新功能 |Microsoft 文件"
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 787552c5a10579e90a0ab62e9105172f989357f5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="clr-integration---what39s-new"></a>CLR 整合的功能 &#39; 新
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]以下是中的 CLR 整合的新功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   在 CLR 的版本 4 中，CLR 資料庫物件不再攔截損壞的狀態例外狀況。 這些例外狀況現在會在 CLR 整合裝載層中攔截。 這些例外狀況可以仍然攔截的 CLR 資料庫元件設定程式碼屬性 ([\<legacyCorruptedStateExceptionsPolicy > 項目](http://go.microsoft.com/fwlink/?LinkId=204954))。 但是不建議您這樣做，因為當發生損壞的狀態例外狀況時，結果就不可靠。  
  
-   由於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的安全性要求很嚴格，所以 CLR 資料庫元件將會繼續使用 CLR 2.0 版中所定義的程式碼存取安全性模型。  
  
-   在 CLR 第 4 版中的格式錯誤**System.TimeSpan**值將會產生**System.FormatExceptions**。 CLR 中的格式錯誤的版本 4 之前**System.TimeSpan**數值會被忽略。 依賴 CLR 的版本 4 之前行為的資料庫應用程式應該使用資料庫相容性層級 (**ALTER DATABASE 相容性層級**) 100 或更低。 如需詳細資訊，請參閱[< TimeSpan_LegacyFormatMode > 項目](http://go.microsoft.com/fwlink/?LinkId=205109)。  
  
-   版本 4 的 CLR 支援 Unicode 5.1。 涉及一些腔調字標記和符號的排序作業將得以改善。 如果您的應用程式依賴舊版的排序行為，可能會發生相容性問題。 若要啟用舊版排序，資料庫相容性層級 (**ALTER DATABASE 相容性層級**) 必須設為 100 或更低。 為了支援這項處理，[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 會將 sort00001000.dll 安裝在 .NET Framework 4 目錄中 (C:\Windows\Microsoft.NET\Framework\v4.0.30319)。 如需詳細資訊，請參閱[ \<CompatSortNLSVersion > 項目](http://go.microsoft.com/fwlink/?LinkId=205110)。  
  
-   下列資料行已加入至[sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**， **total_allocated_memory_kb**，和**survived_memory_kb**。  
  
  
