---
title: CLR 整合的新增功能 |微軟文件
description: 託管 CLR 的 Microsoft SQL 伺服器稱為 CLR 整合。 本文介紹了 SQL Server 2012 中 CLR 集成中的新功能。
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: d27bf0d925d3a98dda488fb85aff7446434cc8ad
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488087"
---
# <a name="clr-integration---what39s-new"></a>CLR 整合 -&#39;新增功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  以下是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中 CLR 整合的新功能：  
  
-   在 CLR 的版本 4 中，CLR 資料庫物件不再攔截損壞的狀態例外狀況。 這些例外狀況現在會在 CLR 整合裝載層中攔截。 CLR 資料庫元件仍可以通過設定代碼屬性([\<遺留的損壞狀態異常策略>元素](https://go.microsoft.com/fwlink/?LinkId=204954))來捕獲這些異常。 但是不建議您這樣做，因為當發生損壞的狀態例外狀況時，結果就不可靠。  
  
-   由於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的安全性要求很嚴格，所以 CLR 資料庫元件將會繼續使用 CLR 2.0 版中所定義的程式碼存取安全性模型。  
  
-   在 CLR 版本 4 中,系統中的格式錯誤 **。TimeSpan**值將生成**系統。** 在 CLR 版本 4 之前,系統 **.TimeSpan**值中的格式錯誤被忽略。 依賴於 CLR 版本 4 之前的行為的資料庫應用程式應以 100 或更低的資料庫相容性級別 **(ALTER DATABASE 相容性級別**) 運行。 有關詳細資訊,請參閱[<TimeSpan_LegacyFormatMode>元素](https://go.microsoft.com/fwlink/?LinkId=205109)。  
  
-   版本 4 的 CLR 支援 Unicode 5.1。 涉及一些腔調字標記和符號的排序作業將得以改善。 如果您的應用程式依賴舊版的排序行為，可能會發生相容性問題。 要啟用舊排序,必須將資料庫相容性級別 **(ALTER 資料庫相容性級別**) 設置為 100 或更低。 為了支援這項處理，[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 會將 sort00001000.dll 安裝在 .NET Framework 4 目錄中 (C:\Windows\Microsoft.NET\Framework\v4.0.30319)。 有關詳細資訊,請參閱[\<"比較排序">元素](https://go.microsoft.com/fwlink/?LinkId=205110)。  
  
-   以下列已新增到 sys [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md) **dm_clr_appdomains:total_processor_time_ms、total_allocated_memory_kb****total_allocated_memory_kb**和**survived_memory_kb**。  
  
  
