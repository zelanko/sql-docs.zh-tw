---
title: 資料庫屬性 (檔案群組頁面) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.filegroups.f1
ms.assetid: 8d06e859-73dd-4019-b6e8-99c5c5297697
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f879da34541b11cf511c2178c9a9ab8223af549
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233358"
---
# <a name="database-properties-filegroups-page"></a>資料庫屬性 (檔案群組頁面)
  使用此頁面來檢視檔案群組或將新的檔案群組加入選取的資料庫中。 檔案群組類型分成「資料列」檔案群組、FILESTREAM 資料和記憶體最佳化檔案群組。  
  
 資料列檔案群組包含一般的資料和記錄檔。 FILESTREAM 資料檔案群組包含 FILESTREAM 資料檔案。 當您使用 FILESTREAM 儲存體時，這些資料檔案會儲存有關二進位大型物件 (BLOB) 資料如何儲存在檔案系統上的資訊。 對於這兩種類型的檔案群組而言，選項都是相同的。  
  
 如果未啟用 FILESTREAM，將無法使用 [Filestream] 區段。 您可以使用[伺服器屬性 (進階頁面)](../../database-engine/configure-windows/server-properties-advanced-page.md) 來啟用 FILESTREAM 儲存體。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何使用資料列檔案群組的相關資訊，請參閱[資料庫檔案與檔案群組](database-files-and-filegroups.md)。 如需 FILESTREAM 資料和檔案群組的詳細資訊，請參閱 [FILESTREAM &#40;SQL Server&#41;](../blob/filestream-sql-server.md)。  
  
 記憶體最佳化檔案群組是讓資料庫包含一個或多個記憶體最佳化資料表的必要條件。  
  
## <a name="row-and-filestream-data-filegroup-options"></a>資料列和 FILESTREAM 資料檔案群組選項  
 **名稱**  
 輸入檔案群組的名稱。  
  
 **檔案**  
 顯示檔案群組中的檔案計數。  
  
 **唯讀**  
 選取即可將檔案群組設定為唯讀狀態。  
  
 **預設值**  
 選取即可讓這個檔案群組成為預設的檔案群組。 您可以有一個預設的資料列檔案群組，以及一個預設的 FILESTREAM 資料檔案群組。  
  
 **[加入]**  
 將新的空白資料列加入列出資料庫之檔案群組的方格中。  
  
 **移除**  
 從方格中移除選取的檔案群組資料列。  
  
## <a name="memory-optimized-data-filegroup-options"></a>記憶體最佳化資料檔案群組選項  
 **名稱**  
 輸入記憶體最佳化檔案群組的名稱。  
  
 **Filestream 檔案**  
 顯示記憶體最佳化資料檔案群組中的檔案 (容器) 數目。 您可以在 [檔案] 頁面中加入容器。  
  
 **[加入]**  
 將新的空白資料列加入列出資料庫之檔案群組的方格中。  
  
 **移除**  
 從方格中移除選取的檔案群組資料列。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
