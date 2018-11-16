---
title: 改善追蹤資料的存取 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], space
- SQL Server Profiler, space
- space [SQL Server], SQL Server Profiler
ms.assetid: c260c000-fd53-4831-993f-df6894f3228b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3319e045a2503767d9227c3064c18583be7d6e82
ms.sourcegitcommit: ddb682c0061c2a040970ea88c051859330b8ac00
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51570988"
---
# <a name="improve-access-to-trace-data"></a>改善追蹤資料的存取
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 會使用 **temp** 目錄中的空間，來改進追蹤資料的存取。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 需要至少 10 MB 的可用空間。 如果您使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]時，可用空間在 10 MB 以下，所有 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 功能都會停止運作。  
  
 當 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 使用 **temp** 目錄中的空間，這個空間用法可能會使 **temp** 目錄快速成長。 為了避免發生檔案成長問題，您可以變更 TEMP 環境變數值，將 **temp** 目錄放在非系統磁碟機中。  
  
 下列程序說明如何在 Microsoft Windows 作業系統中，變更 TEMP 環境變數值。 如需有關設定環境變數的詳細資訊，請參閱您的 Windows 作業系統文件。  
  
### <a name="to-change-the-temp-environment-variable-in-windows-operating-systems"></a>在 Windows 作業系統中變更 TEMP 環境變數  
  
1.  在 [開始] 功能表上，選擇 [控制台]，然後按一下 [系統]。  
  
2.  在 [系統內容] 對話方塊中，按一下 [進階] 索引標籤，然後按一下 [環境變數]。  
  
3.  向下捲動 [系統變數] 清單，選取對應於 **TEMP** 變數的資料列，然後按一下 [編輯]。  
  
4.  在 [編輯系統變數] 對話方塊中，輸入 **temp** 目錄要放在其中之磁碟機和目錄的路徑與名稱。  
  
5.  按一下 [確定] 來儲存變更。  
  
## <a name="see-also"></a>另請參閱  
 [啟動 SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
