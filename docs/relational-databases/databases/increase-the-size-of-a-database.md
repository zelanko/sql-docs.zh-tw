---
title: "增加資料庫的大小 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [SQL Server], size
- increasing database size
- database size [SQL Server], increasing
- size [SQL Server], databases
ms.assetid: 14f4206d-3afa-4ba9-9849-23e81d63306d
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 66895e3c9a74b60e570ccc6b451023da0d93da40
ms.lasthandoff: 04/11/2017

---
# <a name="increase-the-size-of-a-database"></a>增加資料庫的大小
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中增加資料庫的大小。 增加現有資料或記錄檔的大小或將新檔案加入資料庫中，可擴充資料庫。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法增加資料庫的大小：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   當 BACKUP 陳述式在執行中，您不能新增或移除檔案。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料庫的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-increase-the-size-of-a-database"></a>若要增加資料庫的大小  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫]，以滑鼠右鍵按一下要增加的資料庫，然後按一下 [屬性]。  
  
3.  在 **[資料庫屬性]**中，選取 **[檔案]** 頁面。  
  
4.  若要增加現有檔案的大小，請在 [初始大小 (MB)] 資料行中增加該檔案的值。 資料庫的大小至少必須增加 1MB。  
  
5.  若要加入新檔案來增加資料庫的大小，請按一下 **[加入]** ，再輸入新檔案的值。 如需詳細資訊，請參閱 [Add Data or Log Files to a Database](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)。  
  
6.  按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-increase-the-size-of-a-database"></a>若要增加資料庫的大小  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這個範例會增加 `test1dat3`檔案的大小。  
  
 [!code-sql[DatabaseDDL#AlterDatabase5](../../relational-databases/databases/codesnippet/tsql/increase-the-size-of-a-d_1.sql)]  
  
 如需其他範例，請參閱 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Add Data or Log Files to a Database](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)   
 [壓縮資料庫](../../relational-databases/databases/shrink-a-database.md)  
  
  
