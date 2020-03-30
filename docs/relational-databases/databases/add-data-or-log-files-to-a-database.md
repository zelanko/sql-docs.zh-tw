---
title: 將資料或記錄檔新增至資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], files
- adding data files
- adding files
- adding log files
- file additions [SQL Server], steps
- files [SQL Server], adding
- data additions [SQL Server]
ms.assetid: 8ead516a-1334-4f40-84b2-509d0a8ffa45
author: stevestein
ms.author: sstein
ms.openlocfilehash: 34e976dca163289450c3aa481d1f72bb46712046
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68137401"
---
# <a name="add-data-or-log-files-to-a-database"></a>將資料或記錄檔加入資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中將資料或記錄檔加入至資料庫。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法，將資料或記錄檔加入資料庫：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   當 BACKUP 陳述式在執行中，您不能新增或移除檔案。  
  
-   每個資料庫最多可以指定 32,767 個檔案和 32,767 個檔案群組。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料庫的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-add-data-or-log-files-to-a-database"></a>若要將資料或記錄檔加入資料庫  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫]  ，以滑鼠右鍵按一下要加入檔案的來源資料庫，然後按一下 [屬性]  。  
  
3.  在 **[資料庫屬性]** 對話方塊中，選取 **[檔案]** 頁面。  
  
4.  若要加入資料或交易記錄檔，請按一下 **[加入]** 。  
  
5.  在 **[資料庫檔案]** 方格中，輸入檔案的邏輯名稱。 檔案名稱在資料庫中必須是唯一的。  
  
6.  選取檔案類型：資料或記錄檔。  
  
7.  若是資料檔案，請選取檔案群組，其中的檔案應包含在清單中，或選取 [**新增檔案群組>]\<** 以建立新的檔案群組。 交易記錄檔無法放在檔案群組中。  
  
8.  指定檔案的起始大小。 可根據預期的資料庫最大資料量，儘可能將資料檔設為最大。  
  
9. 若要指定檔案應該如何成長，請按一下 [自動成長]  資料行中的 ( **…** )。 然後選取下列選項：  
  
    1.  若要允許目前選取的檔案依所需的資料空間成長，請選取 **[啟用自動成長]** 核取方塊，然後選取下列選項：  
  
    2.  若要指定檔案以固定遞增值成長，請選取 **[以 MB 表示]** ，然後指定一個值。  
  
    3.  若要指定檔案依照目前檔案大小的百分比成長，請選取 **[以百分比表示]** ，然後指定一個值。  
  
10. 若要指定檔案大小上限，請選取下列些選項：  
  
    1.  若要指定檔案大小可以成長的上限，請選取 [限制的檔案成長 (MB)]  ，然後指定一個值。  
  
    2.  若要讓檔案依照需要成長，請選取 **[不限制檔案成長]** 。  
  
    3.  若要防止檔案成長，請清除 **[啟用自動成長]** 核取方塊。 檔案成長的大小將不會超過 [初始大小 (MB)]  資料行中所指定的值。  
  
    > [!NOTE]  
    >  資料庫大小的上限取決於可用的磁碟空間，及所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的授權限制。  
  
11. 指定檔案位置的路徑。 在加入檔案之前必須先指定路徑。  
  
    > [!NOTE]  
    >  依預設，資料和交易記錄是放在相同的磁碟及路徑中以配合單一磁碟系統，但在實際執行環境中可能不是最理想的。 如需相關資訊，請參閱 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)。  
  
12. 按一下 [確定]  。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-add-data-or-log-files-to-a-database"></a>若要將資料或記錄檔加入資料庫  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例會將含有兩個檔案的檔案群組加入資料庫中。 此範例會在 `Test1FG1` 資料庫中建立 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 檔案群組，且會將兩個 5 MB 的檔案加入檔案群組中。  
  
 [!code-sql[DatabaseDDL#AlterDatabase2](../../relational-databases/databases/codesnippet/tsql/add-data-or-log-files-to_1.sql)]  
  
 如需其他範例，請參閱 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)   
 [刪除資料庫的資料或記錄檔](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)   
 [增加資料庫的大小](../../relational-databases/databases/increase-the-size-of-a-database.md)  
  
  
