---
title: 資料庫屬性 (檔案頁面) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.files.f1
ms.assetid: 3c030e51-db82-4b43-b1e5-8547ddd3de87
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26b387537a2d3cb6a4e6ed8e6b9deda435626142
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057028"
---
# <a name="database-properties-files-page"></a>資料庫屬性 (檔案頁面)
  使用此頁面來建立新的資料庫，或者檢視或修改選取之資料庫的屬性。 此主題適用於現有資料庫的 [資料庫屬性 (檔案頁面)]，以及 [新增資料庫 (一般頁面)]。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **資料庫名稱**  
 加入或顯示資料庫的名稱。  
  
 **擁有者**  
 從清單中選取以指定資料庫的擁有者。  
  
 **使用全文檢索索引**  
 這個核取方塊會被核取並停用，因為在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，全文檢索索引一定是啟用的。 如需詳細資訊，請參閱 [全文檢索搜尋](../search/full-text-search.md)。  
  
 **資料庫檔案**  
 加入、檢視、修改或移除相關聯資料庫的資料庫檔案。 資料庫檔案具有下列屬性：  
  
 **邏輯名稱**  
 輸入或修改檔案的名稱。  
  
 **檔案類型**  
 從清單中選取檔案類型。 檔案類型可以是 **[資料]**、 **[記錄檔]** 或 **[FILESTREAM 資料]**。 您無法修改現有檔案的檔案類型。  
  
 如果您要將檔案 (容器) 加入至記憶體最佳化檔案群組，請選取 [FILESTREAM 資料]。  
  
 若要將檔案 (容器) 加入至 Filestream 資料檔案群組，就必須啟用 FILESTREAM。 您可以使用 [[伺服器屬性 (進階頁面)]](../../database-engine/configure-windows/server-properties-advanced-page.md) 對話方塊來啟用 FILESTREAM。  
  
 **檔案群組**  
 從清單中選取檔案的檔案群組。 依預設，此檔案群組為 PRIMARY。 您可以選取 [\<新增檔案群組>]，並在 [新增檔案群組] 對話方塊中輸入有關檔案群組的資訊，以建立新的檔案群組。 新的檔案群組亦可在 **[檔案群組]** 頁面上建立。 您無法修改現有檔案的檔案群組。  
  
 將檔案 (容器) 加入至記憶體最佳化檔案群組時，[檔案群組] 欄位會填入資料庫之記憶體最佳化檔案群組的名稱。  
  
 **初始大小**  
 輸入或修改檔案的初始大小 (以 MB 表示)。 依預設，這是 **[model]** 資料庫的值。  
  
 這個欄位對於 FILESTREAM 檔案無效。  
  
 若為記憶體最佳化檔案群組中的檔案，就無法修改此欄位。  
  
 **自動成長**  
 選取或顯示檔案的自動成長屬性。 這些屬性會控制當達到檔案大小上限時檔案的展開方式。 若要編輯自動成長值，請針對所要的檔案，按一下自動成長屬性旁的 [編輯] 按鈕，並變更 **[變更自動成長]** 對話方塊中的值。 依預設，這些是 **[model]** 資料庫的值。  
  
 這個欄位對於 FILESTREAM 檔案無效。  
  
 若為記憶體最佳化檔案群組中的檔案，此欄位應該是 [無限制]。  
  
 **路徑**  
 顯示選取之檔案的路徑。 若要指定新檔案的路徑，請按一下該檔案路徑旁的 [編輯] 按鈕，並導覽到目的資料夾。 您無法修改現有檔案的路徑。  
  
 如果是 FILESTREAM 檔案，路徑會是資料夾。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 將會在此資料夾中建立基礎檔案。  
  
 **檔案名稱**  
 顯示檔案的名稱。  
  
 這個欄位對於 FILESTREAM 檔案無效，包括記憶體最佳化檔案群組中的檔案。  
  
 **[加入]**  
 將新檔案加入資料庫中。  
  
 **移除**  
 從資料庫中刪除選取的檔案。 除非檔案空白，否則就無法移除。 無法移除主要資料檔案和記錄檔。  
  
 如需有關檔案的詳細資訊，請參閱＜ [Database Files and Filegroups](database-files-and-filegroups.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
