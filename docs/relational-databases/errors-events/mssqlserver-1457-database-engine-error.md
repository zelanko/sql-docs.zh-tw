---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f4a756af242a9cdf8b75241be204c289c8bc8eb3
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1457"></a>MSSQLSERVER_1457
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1457|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBM_PAGE_UNDO_PENDING|  
|訊息文字|鏡像資料庫 '%.*ls' 的同步處理已中斷，導致資料庫成為不一致的狀態。 ALTER DATABASE 命令失敗。 請確定鏡像資料庫有備份且在線上，然後重新連接鏡像伺服器執行個體，讓鏡像資料庫能夠完成同步處理。|  
  
## <a name="explanation"></a>說明  
此訊息表示 ALTER DATABASE *database_name* SET PARTNER OFF 陳述式失敗。 嘗試移除資料庫鏡像失敗，導致鏡像資料庫的同步處理中斷。 資料庫的狀態不一致。  
  
## <a name="user-action"></a>使用者動作  
若要解決此錯誤，可以採取下列其中一個動作︰  
  
-   還原鏡像伺服器與主體伺服器之間的連絡，讓鏡像資料庫進行同步處理。  
  
-   卸除鏡像資料庫。  
  
    卸除鏡像資料庫之後，您就可以從備份建立新的鏡像資料庫。  
  
    > [!NOTE]  
    > 只有在 SET PARTNER OFF 陳述式失敗之後，才能在鏡像仍為啟用狀態的情況下卸除鏡像資料庫。  
  
## <a name="see-also"></a>另請參閱  
[資料庫鏡像 &#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[設定資料庫鏡像 &#40;SQL Server&#41;](~/database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
[移除資料庫鏡像 &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
[準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](~/database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  

