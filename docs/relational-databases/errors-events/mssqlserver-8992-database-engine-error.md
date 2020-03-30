---
title: MSSQLSERVER_8992 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9d5da60bc3e2716fb808c47f949b3b918b4e9d85
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "77479669"
---
# <a name="mssqlserver_8992"></a>MSSQLSERVER_8992
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|8992|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC3_CHECK_CATALOG|  
|訊息文字|檢查目錄訊息 ERROR 層級 LEVEL 狀態 STATE:MESSAGE。|  

> [!NOTE]
> 8992 錯誤訊息會參考有關實際不一致的另一項特定訊息 (範圍從 3851 到 3858)。

## <a name="explanation"></a>說明  
DBCC CHECKCATALOG 或 DBCC CHECKDB 在指定之物件的系統中繼資料表中發現不一致。 亦即，在記錄的物件識別碼和錯誤訊息中指定的物件之間發生不一致。  
  
當一個或多個系統資料表利用產生系統中繼資料不一致的方式進行手動更新，可能會發生這個錯誤。 例如，使用者可能已經手動刪除 **sysobjects** 資料表中的物件，而沒有移除其他資料表中相關聯的資料列，例如 **sysindexes** 和 **syscolumns**。  
  
根據已經從 SQL Server 2000 升級到 SQL Server 2005 或更新版本的資料庫執行 DBCC CHECKDB 時，可能會發生這個錯誤。 在 SQL Server 2000 中，DBCC CHECKDB 不包含 DBCC CHECKCATALOG 功能，因此，除非特別針對 SQL Server 2000 中的資料庫執行 DBCC CHECKCATALOG，否則在升級前不會造成錯誤。  
  
您可能會看到下列任一種錯誤和錯誤 8992 一起出現：  
|||
|-|-| 
|訊息識別碼|訊息文字|
|3851|在系統資料表 sys.%ls%ls 上發現無效的資料列 (%ls)。|
|3852|sys.%ls%ls 中的資料列 (%ls) 在 sys.%ls%ls 之中並沒有相符的資料列 (%ls)。|
|3853|sys.%ls%ls 中資料列 (%ls) 的屬性 (%ls) 在 sys.%ls%ls 中並沒有相符的資料列 (%ls)。|
|3854|sys.%ls%ls 中資料列 (%ls) 的屬性 (%ls) 在 sys.%ls%ls 中相符的資料列 (%ls) 無效。|
|3855|屬性 (%ls) 存在，但是在 sys.%ls%ls 中沒有資料列 (%ls)。|
|3856|屬性 (%ls) 存在，但應該不是 sys.%ls%ls 中資料列 (%ls) 的屬性。|
|3857|必須有屬性 (%ls)，但是 sys.%ls%ls 中的資料列 (%ls) 遺漏此屬性。|
|3858|sys.%ls%ls 中資料列 (%ls) 的屬性 (%ls) 有無效的值。|

## <a name="user-action"></a>使用者動作  
  
### <a name="drop-and-re-create-the-specified-object"></a>卸除指定的物件後再重新建立  
如果可能，卸除指定的物件後再重新建立。 例如，如果物件為預存程序或使用者定義型別，重新建立物件可能會解決問題。  
  
### <a name="restore-from-backup"></a>還原備份  
如果問題與硬體無關，而且確定有未受影響的備份可以使用，請利用該備份來還原資料庫。 此動作僅適用於備份不包含中繼資料錯誤時。  
  
### <a name="export-the-data-to-a-new-database"></a>將資料匯出到新資料庫  
如果備份另有中繼資料不一致的情況，則您需要建立新的資料庫，並且將現有資料庫的內容匯出到新資料庫。  
  
### <a name="dbcc-checkdb-cannot-repair-this-error"></a>DBCC CHECKDB 無法修復此錯誤  
此錯誤無法修復。  如果無法從備份還原資料庫，請連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶服務及支援中心 (CSS)。  
  
### <a name="do-not-manually-update-system-tables"></a>不要手動更新系統資料表  

不要手動更新系統資料表。 SQL Server 不支援對系統資料庫進行任何手動變更。 如果您更新 SQL Server 資料庫中的系統資料表，則會記錄下列事件：

#### <a name="when-a-system-table-is-manually-updated"></a>手動更新系統資料表時

訊息 17659：警告：已直接在資料庫識別碼 <id> 中更新系統資料表識別碼 <id>，可能未能保持快取的連貫性。 應該重新啟動 SQL Server。

#### <a name="starting-a-database-with-a-system-table-that-was-manually-updated"></a>使用手動更新的系統資料表啟動資料庫

訊息 3859：警告：已直接在資料庫識別碼 <id> 中更新系統目錄，最近一次在 date_time

#### <a name="when-you-execute-the-dbcc_checkdb-command-after-a-system-table-is-manually-updated"></a>當您在手動更新系統資料表後執行 DBCC_CHECKDB 命令時

訊息 3859：警告：已直接在資料庫識別碼 <id> 中更新系統目錄，最近一次在 date_time。  

## <a name="see-also"></a>另請參閱

[系統基底資料表](../system-tables/system-base-tables.md)
  
