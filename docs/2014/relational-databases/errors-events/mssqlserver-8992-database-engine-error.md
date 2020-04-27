---
title: MSSQLSERVER_8992 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ad75e136c4bef59f24b451b84f03e06d71a32ec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62912542"
---
# <a name="mssqlserver_8992"></a>MSSQLSERVER_8992
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|8992|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC3_CHECK_CATALOG|  
|訊息文字|檢查目錄訊息 ERROR 層級 LEVEL 狀態 STATE:MESSAGE。|  
  
## <a name="explanation"></a>說明  
 DBCC CHECKCATALOG 或 DBCC CHECKDB 在指定之物件的系統中繼資料表中發現不一致。 亦即，在記錄的物件識別碼和錯誤訊息中指定的物件之間發生不一致。  
  
 當一個或多個系統資料表利用產生系統中繼資料不一致的方式進行手動更新，可能會發生這個錯誤。 例如，使用者可能已經手動刪除 **sysobjects** 資料表中的物件，而沒有移除其他資料表中相關聯的資料列，例如 **sysindexes** 和 **syscolumns**。  
  
 根據已經從 SQL Server 2000 升級到 SQL Server 2005 或更新版本的資料庫執行 DBCC CHECKDB 時，可能會發生這個錯誤。 在 SQL Server 2000 中，DBCC CHECKDB 不包含 DBCC CHECKCATALOG 功能，因此，除非特別針對 SQL Server 2000 中的資料庫執行 DBCC CHECKCATALOG，否則在升級前不會造成錯誤。  
  
 您可能會看到下列任一種錯誤和錯誤 8992 一起出現：  
  
 訊息 3851：在系統資料表 sys.%ls%ls 中發現無效的資料列 (%ls)。  
  
 訊息 3852：sys.%ls%ls 中的資料列 (%ls) 在 sys.%ls%ls 之中並沒有相符的資料列 (%ls)。  
  
 3853：sys.%ls%ls 中資料列 (%ls) 的屬性 (%ls) 在 sys.%ls%ls 中並沒有相符的資料列 (%ls)。  
  
 3854：sys.%ls%ls 中資料列 (%ls) 的屬性 (%ls) 在 sys.%ls%ls 中相符的資料列 (%ls) 無效。  
  
 3855：屬性 (%ls) 存在，但是在 sys.%ls%ls 中沒有資料列 (%ls)。  
  
 3856：屬性 (%ls) 存在，但應該不是 sys.%ls%ls 中資料列 (%ls) 的屬性。  
  
 3857：必須有屬性 (%ls)，但是 sys.%ls%ls 中的資料列 (%ls) 缺少此屬性。  
  
 3858：sys.%ls%ls 中資料列 (%ls) 的屬性 (%ls) 有無效的值。  
  
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
 不要手動更新系統資料表。 SQL Server 不支援對系統資料庫進行任何手動變更。 如果您更新 SQL Server 資料庫中的系統資料表，則會記錄兩個事件 (事件識別碼 17659 和事件識別碼 3859)。 如需詳細資訊，請參閱知識庫文件 2688307＜當您更新 SQL Server 資料庫中的系統資料表時，會記錄事件識別碼 17659 和事件識別碼 3859＞(機器翻譯)。  
  
## <a name="see-also"></a>另請參閱  
 [Event ID 17659 and event ID 3859 are logged when you update system tables in a SQL Server database](https://support.microsoft.com/kb/2688307/EN-US) (當您更新 SQL Server 資料庫中的系統資料表時，會記錄事件識別碼 17659 和事件識別碼 3859)  
  
  
