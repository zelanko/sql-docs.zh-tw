---
title: CLR 整合的新功能 |Microsoft Docs
description: Microsoft SQL Server 裝載 CLR 稱為 CLR 整合。 本文說明 SQL Server 2012 中 CLR 整合的新功能。
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: eaf16cda98f019f6d378a3287e1068d78df88bac
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809514"
---
# <a name="clr-integration---what39s-new"></a>CLR 整合-新功能&#39;
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  以下是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中 CLR 整合的新功能：  
  
-   在 CLR 的版本 4 中，CLR 資料庫物件不再攔截損壞的狀態例外狀況。 這些例外狀況現在會在 CLR 整合裝載層中攔截。 這些例外狀況仍可由 CLR 資料庫元件攔截，方法是將程式碼屬性設定為 ([ \<legacyCorruptedStateExceptionsPolicy> 元素](/dotnet/framework/configure-apps/file-schema/runtime/legacycorruptedstateexceptionspolicy-element)) 。 但是不建議您這樣做，因為當發生損壞的狀態例外狀況時，結果就不可靠。  
  
-   由於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的安全性要求很嚴格，所以 CLR 資料庫元件將會繼續使用 CLR 2.0 版中所定義的程式碼存取安全性模型。  
  
-   在 CLR 第4版中， **TimeSpan** 值的格式錯誤將會產生 **FormatExceptions**。 在 CLR 的第4版之前，系統會忽略 **TimeSpan** 值的格式錯誤。 依賴 CLR 第4版之前行為的資料庫應用程式應該使用資料庫相容性層級來執行， (**ALTER Database 相容性層級**) 100 或更低版本。 如需詳細資訊，請參閱 [<TimeSpan_LegacyFormatMode> 元素](/dotnet/framework/configure-apps/file-schema/runtime/timespan-legacyformatmode-element)。  
  
-   版本 4 的 CLR 支援 Unicode 5.1。 涉及一些腔調字標記和符號的排序作業將得以改善。 如果您的應用程式依賴舊版的排序行為，可能會發生相容性問題。 若要啟用舊版排序，資料庫相容性層級 (的 **ALTER Database 相容性層級**) 必須設定為100或更低版本。 為了支援這項處理，[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 會將 sort00001000.dll 安裝在 .NET Framework 4 目錄中 (C:\Windows\Microsoft.NET\Framework\v4.0.30319)。 如需詳細資訊，請參閱[ \<CompatSortNLSVersion> 元素](/dotnet/framework/configure-apps/file-schema/runtime/compatsortnlsversion-element)。  
  
-   下列資料行已加入至 [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)： **total_processor_time_ms**、 **total_allocated_memory_kb**和 **survived_memory_kb**。  
  
