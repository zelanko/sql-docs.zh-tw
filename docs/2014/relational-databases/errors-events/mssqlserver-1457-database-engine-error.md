---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f45545212b494f955c6b9be97ccf0df7efeb622
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869910"
---
# <a name="mssqlserver1457"></a>MSSQLSERVER_1457
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
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
    >  只有在 SET PARTNER OFF 陳述式失敗之後，才能在鏡像仍為啟用狀態的情況下卸除鏡像資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [設定資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [移除資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
  
