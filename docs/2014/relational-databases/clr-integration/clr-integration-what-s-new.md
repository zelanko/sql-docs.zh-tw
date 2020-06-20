---
title: CLR 整合的新功能&#39;|Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: b51eb5d8bee5ff8e514f294d5e9facca93a30bfa
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953550"
---
# <a name="what39s-new-in-clr-integration"></a>CLR 整合的新功能&#39;
  以下是 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中 CLR 整合的新功能：  
  
-   在 CLR 的版本 4 中，CLR 資料庫物件不再攔截損壞的狀態例外狀況。 這些例外狀況現在會在 CLR 整合裝載層中攔截。 CLR 資料庫元件仍然可以藉由設定程式碼屬性（專案）來攔截這些[ \<legacyCorruptedStateExceptionsPolicy> ](https://go.microsoft.com/fwlink/?LinkId=204954)例外狀況。 但是不建議您這樣做，因為當發生損壞的狀態例外狀況時，結果就不可靠。  
  
-   由於 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 的安全性要求很嚴格，所以 CLR 資料庫元件將會繼續使用 CLR 2.0 版中所定義的程式碼存取安全性模型。  
  
-   在 CLR 版本 4 中，`System.TimeSpan` 值的格式錯誤將會產生 `System.FormatExceptions`。 在 CLR 的版本 4 之前，`System.TimeSpan` 值的格式錯誤會被忽略。 依賴 CLR 版本 4 之前行為的資料庫應用程式應該要以資料庫相容性層級 (`ALTER DATABASE Compatibility Level`) 100 或更低的層級來執行。 如需詳細資訊，請參閱[<TimeSpan_LegacyFormatMode> 元素](https://go.microsoft.com/fwlink/?LinkId=205109)。  
  
-   版本 4 的 CLR 支援 Unicode 5.1。 涉及一些腔調字標記和符號的排序作業將得以改善。 如果您的應用程式依賴舊版的排序行為，可能會發生相容性問題。 若要啟用舊版排序，資料庫相容性層級 (`ALTER DATABASE Compatibility Level`) 必須設定為 100 或更低的值。 為了支援這項處理，[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 會將 sort00001000.dll 安裝在 .NET Framework 4 目錄中 (C:\Windows\Microsoft.NET\Framework\v4.0.30319)。 如需詳細資訊，請參閱[ \<CompatSortNLSVersion> 元素](https://go.microsoft.com/fwlink/?LinkId=205110)。  
  
-   下列資料行已加入至[sys. dm_clr_appdomains](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql)： `total_processor_time_ms` 、 `total_allocated_memory_kb` 和 `survived_memory_kb` 。  
  
  
