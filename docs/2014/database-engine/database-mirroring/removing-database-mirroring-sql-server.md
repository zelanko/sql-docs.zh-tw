---
title: 移除資料庫鏡像 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], removing
- stopping database mirroring [SQL Server]
- removing database mirroring [SQL Server]
ms.assetid: 40c72091-8f03-4037-8b55-5e95309fe145
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 414cdedb8f2bc3dee4edc792c11b6438306818c6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754538"
---
# <a name="removing-database-mirroring-sql-server"></a>移除資料庫鏡像 (SQL Server)
  資料庫擁有者可隨時在夥伴上手動停止資料庫鏡像工作階段。  
  
## <a name="impact-of-removing-mirroring"></a>移除鏡像的影響  
 移除鏡像後，就會發生下列情況：  
  
-   夥伴之間以及每個夥伴與見證之間的關聯性會永久中斷 (若有任何關聯性存在的話)。  
  
     若工作階段停止時夥伴伺服器正在與其他夥伴伺服器通訊，則會立即在這兩台電腦上中斷其關係。 如果夥伴伺服器並未在通訊 (停止時資料庫正處於 DISCONNECTED 狀態)，則會立即在停止鏡像的夥伴伺服器上中斷關係；如果其他夥伴伺服器嘗試要重新連接，則會發現資料庫鏡像工作階段已結束。  
  
-   與暫停工作階段不同，鏡像工作階段的相關資訊會被卸除。 也會移除主體資料庫和鏡像資料庫上的鏡像。 在 **sys.databases** 中，**mirroring_state** 資料行和所有其他鏡像資料行都會設定為 NULL。 如需詳細資訊，請參閱 [sys.database_mirroring &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql)。  
  
-   每個夥伴伺服器執行個體都會保有個別的資料庫副本。  
  
-   因為鏡像資料庫是利用 RESTORE WITH NORECOVERY 建立的，所以它會處於 RESTORING 狀態 (請參閱 **sys.databases** 的 **state**資料行)。 此時，您可卸除先前的鏡像資料庫，或利用 WITH RECOVERY 予以還原。 當您復原資料庫時，因為復原會啟動新的復原分岔，所以與先前的主體資料庫有所差異。  
  
> [!NOTE]  
>  若要在停止工作階段之後繼續鏡像，您就必須建立新的資料庫鏡像工作階段。 若要在停止鏡像之後建立記錄備份，您必須在重新啟動鏡像之前將它套用到鏡像資料庫。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
 **若要移除資料庫鏡像**  
  
-   [移除資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
 **若要啟動資料庫鏡像**  
  
-   [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  

  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE 資料庫鏡像 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [暫停與繼續資料庫鏡像 &#40;SQL Server&#41;](pausing-and-resuming-database-mirroring-sql-server.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
