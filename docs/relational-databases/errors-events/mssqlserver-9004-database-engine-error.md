---
description: MSSQLSERVER_9004
title: MSSQLSERVER_9004 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4f9b9a18806a4a91b58d0b30e83e560e8f73f6be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460888"
---
# <a name="mssqlserver_9004"></a>MSSQLSERVER_9004
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|9004|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LOG_CORRUPT|  
|訊息文字|在處理資料庫 '%.*ls' 的記錄檔時，發生錯誤。  If possible, restore from backup. 若備份無法使用，可能需要重建記錄檔。|  
  
## <a name="explanation"></a>說明  
在回復、復原或複寫期間處理記錄檔時發生錯誤。 這可能代表作業系統偵測到的錯誤，或是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 偵測到的內部一致性錯誤。  
[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會在讀取及處理交易記錄內容時，對其執行一致性上的邏輯檢查。 並不會檢查記錄標頭、記錄區塊及記錄的所有層面。 狀態號碼能針對失敗類型提供詳細資訊：

 - **狀態 1** 虛擬記錄檔 (VLF) 的記錄檔標頭已損毀。  如果在服務啟動時，於啟動資料庫期間發現損毀的記錄檔標頭，您在 ERRORLOG 中可能只會看見錯誤 9004。 在交易記錄內，記錄檔標頭是每個 VLF 的第一個部分。 記錄檔標頭和記錄檔的單一檔案標頭 (或前 8 KB) 並不相同。 如果記錄檔的檔案標頭已損毀，您可能會收到訊息 5172 (類似資料庫檔案標頭頁面損毀)。
 - **狀態 2 和 3** 在 RESTORE 作業期間執行復原時，有某個記錄區塊無效。
 - **狀態 4 至 12** 這些都是在處理記錄時，針對記錄區塊所做的各種檢查。 這些包括針對交易記錄一致性的同位、磁區及其他邏輯檢查

在大部分的情況下，此錯誤只會搭配 EventID = 9004 出現在 ERRORLOG 或 Windows 應用程式事件記錄檔中，因為處理記錄的作業並不是以直接使用者命令 (例如在 SQL Server 引擎啟動時執行復原) 為基礎。 在這些情況下，錯誤 9004 通常會和錯誤 3414 一起出現。 不過，如 ALTER DATABASE 的部分查詢可能會要求處理記錄，因此將會看見這些錯誤。 由於該錯誤為 Severity=21，使用者工作階段便會中斷連線。

## <a name="cause"></a>原因
錯誤 9004 是指出交易記錄內容已損毀的一般錯誤。 記錄變得不一致的原因，與 SQL Server 引擎所偵測到的任何資料庫損毀問題相似。 若要找出記錄損毀的原因，您應該遵循用於資料庫損毀的類似技術，其中包括分析可能的硬體、檔案系統及 I/O 問題。 請注意，DBCC CHECKDB 的作業並不會檢查交易記錄，且無法偵測記錄損毀錯誤。 錯誤 9004 是由 SQL Server 引擎本身所引發。

## <a name="user-action"></a>使用者動作  
您可以執行下列其中一項動作來更正此錯誤：  
  
-   **從備份還原**：從已知的良好備份還原來從此問題中復原。 如果資料庫或記錄備份的記錄部分包含損毀內容，您可能會在 RESTORE 時遇到錯誤 9004。 在此情況下，備份中的交易記錄已損毀。
  
-   **重建記錄**：如果您無法從備份還原，則可能可以透過重建交易記錄來使資料庫上線。 您應該仔細了解重建交易記錄的後果。 這包括「可能會遺失您資料庫中的交易一致性」。 如需如何重建交易記錄的詳細資訊，請參閱[以資料庫緊急模式解決錯誤](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md#resolving-errors-in-database-emergency-mode)。
  
-   **檢查記錄中的系統問題**：此外，請檢查系統事件記錄檔和錯誤記錄檔，以找出可能造成問題的系統內部問題。  
  
