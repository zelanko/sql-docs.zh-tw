---
title: 壓縮檔案 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.shrinkfile.f1
helpviewer_keywords:
- shrinking files
- decreasing file size
- databases [SQL Server], shrinking
- reducing file size
- size [SQL Server], files
- file size [SQL Server]
ms.assetid: ce5c8798-c039-4ab2-81e7-90a8d688b893
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3adf38c1908e17dbac530cab0cc47658e9241559
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71961924"
---
# <a name="shrink-a-file"></a>壓縮檔案
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中壓縮資料或記錄檔。  
  
 將資料頁面從檔案結尾移到靠近檔案前端的未使用空間，以壓縮資料並復原儲存空間。 當檔案結尾建立了足夠的可用空間後，檔案結尾的資料頁面便可取消配置並返回檔案系統。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法壓縮資料或記錄檔：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   主要資料檔無法縮到小於 model 資料庫中主要資料檔的大小。  
  
###  <a name="Recommendations"></a> 建議  
  
-   為壓縮檔案所移動的資料可散佈至檔案中的任何可用位置。 如此會造成索引片段，並可能導致大範圍之索引搜尋的查詢效能變慢。 若要消除資料片段，可考慮在壓縮之後重建該檔案的索引。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-shrink-a-data-or-log-file"></a>若要壓縮資料檔或記錄檔  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 **[資料庫]** ，然後以滑鼠右鍵按一下您要壓縮的資料庫。  
  
3.  指向 **[工作]** ，指向 **[壓縮]** ，然後按一下 **[檔案]** 。  
  
     **Database**  
     顯示選取之資料庫的名稱。  
  
     **檔案類型**  
     選取檔案的檔案類型。 可用的選擇為 **[資料]** 與 **[記錄]** 檔案。 預設的選取項目為 **[資料]** 。 若選取不同的檔案群組類型，就會變更其他欄位中的選取項目。  
  
     **檔案群組**  
     從與上面選取之 **[檔案類型]** 相關聯的檔案群組清單中選取檔案群組。 若選取不同的檔案群組，就會變更其他欄位中的選取項目。  
  
     **檔案名稱**  
     從選取的檔案群組與檔案類型的可用檔案清單中選取檔案。  
  
     **位置**  
     顯示目前選取之檔案的完整路徑。 無法編輯路徑，但是可以將它複製到剪貼簿。  
  
     **目前配置的空間**  
     若要資料檔，則顯示目前配置的空間。 針對記錄檔，顯示從 DBCC SQLPERF(LOGSPACE) 的輸出計算而來的目前配置空間。  
  
     **可用空間**  
     針對資料檔，顯示從 DBCC SHOWFILESTATS(fileid) 的輸出計算而來的目前可用空間。 針對記錄檔，顯示從 DBCC SQLPERF(LOGSPACE) 的輸出計算而來的目前可用空間。  
  
     **釋放未使用的空間**  
     使檔案中未使用的空間釋出至作業系統，並壓縮檔案至最後配置的範圍，縮減檔案大小而不移動任何資料。 未嘗試重新放置資料列給未配置的頁面。  
  
     **釋放未使用的空間之前，先重新組織頁面**  
     相當於執行指定目標檔案大小的 DBCC SHRINKFILE。 選取此選項時，使用者必須在 **[將檔案壓縮為]** 方塊中指定目標檔案大小。  
  
     **[將檔案壓縮為]**  
     指定壓縮作業的目標檔案大小。 此大小不可小於目前配置的空間或大於配置給檔案的總範圍。 一旦變更焦點或按一下工具列上的任何按鈕時，輸入超過下限或上限的值將還原為下限或上限。  
  
     **將資料移轉至同一檔案群組中的其他檔案，以清空檔案**  
     移轉來自指定之檔案的所有資料。 這個選項允許檔案使用 ALTER DATABASE 陳述式卸除。 此選項相當於執行具有 EMPTYFILE 選項的 DBCC SHRINKFILE。  
  
4.  選取檔案類型與檔案名稱。  
  
5.  (選擇性) 選取 **[釋放未使用的空間]** 核取方塊。  
  
     選取此選項，會讓檔案中任何未使用的空間釋出到作業系統，並壓縮文件到最後的配置範圍。 如此一來無需移動任何資料即可縮減檔案大小。  
  
6.  (選擇性) 選取 **[釋放未使用空間之前重新組織檔案]** 核取方塊。 若選取此選項，則必須在 **[將檔案壓縮為]** 中指定一個值。 根據預設，會清除此選項。  
  
     選取此選項，會讓檔案中任何未使用的空間釋出到作業系統，並嘗試將資料列重新放置到未配置的資料頁。  
  
7.  (選擇性) 輸入資料庫壓縮後資料庫檔案中最大的可用剩餘空間百分比。 允許值介於 0 和 99 之間。 只有當啟用 **[釋放未使用空間之前重新組織檔案]** 時，才能使用此選項。  
  
8.  (選擇性) 選取 **[將資料移轉至同一檔案群組中的其他檔案，以清空檔案]** 核取方塊。  
  
     選取此選項，使檔案群組中指定檔案內的所有資料都移到其他檔案內。 然後即可刪除空白檔案。 這個選項的作用與使用 EMPTYFILE 選項執行 DBCC SHRINKFILE 的作用相同。  
  
9. 按一下 [確定]  。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-shrink-a-data-or-log-file"></a>若要壓縮資料檔或記錄檔  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 下列範例會使用 [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) ，將 `DataFile1` 資料庫中名為 `UserDB` 之資料檔大小壓縮成 7 MB。  
  
 [!code-sql[DBCC#DBCC_SHRINKFILE1](../../relational-databases/databases/codesnippet/tsql/shrink-a-file_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)   
 [壓縮資料庫](../../relational-databases/databases/shrink-a-database.md)   
 [刪除資料庫的資料或記錄檔](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  
