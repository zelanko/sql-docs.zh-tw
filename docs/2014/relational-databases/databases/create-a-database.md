---
title: 建立資料庫 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], creating
- database creation [SQL Server], SQL Server Management Studio
- creating databases
ms.assetid: 4c4beea2-6cbc-4352-9db6-49ea8130bb64
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d93e6cfa3ce6e958b31c1156cd4fc5fa046ad5ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62872271"
---
# <a name="create-a-database"></a>建立資料庫
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立資料庫。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [必要條件](#Prerequisites)  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **使用下列方法建立資料庫：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的一個執行個體上，最多可以指定 32,767 個資料庫。  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   CREATE DATABASE 陳述式必須在自動認可模式 (預設交易管理模式) 下執行，而且不能用於明確或隱含的交易。  
  
###  <a name="Recommendations"></a> 建議  
  
-   每當建立、修改或卸除使用者資料庫時，都應該備份 [master](master-database.md) 資料庫。  
  
-   當您建立資料庫時，請根據您預期之資料庫中的資料量上限，盡量使資料檔案有足夠的空間。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 master 資料庫的 CREATE DATABASE 權限，或需要 CREATE ANY DATABASE 或 ALTER ANY DATABASE 權限。  
  
 為了維護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的磁碟控制，通常只有少數登入帳戶有建立資料庫的權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-database"></a>若要建立資料庫  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [資料庫]，然後按一下 [新增資料庫]。  
  
3.  在 **[新增資料庫]** 中，輸入資料庫名稱。  
  
4.  若要使用所有預設值來建立資料庫，請按一下 **[確定]**，否則繼續執行下列選擇性步驟。  
  
5.  若要變更擁有者名稱，請按一下 (**…**) 來選取其他擁有者。  
  
    > [!NOTE]  
    >  [使用全文檢索索引] 選項一定是核取狀態而且呈暗灰色，因為從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，所有使用者資料庫都會啟用全文檢索。  
  
6.  若要變更主要資料與交易記錄檔的預設值，請在 **[資料庫檔案]** 方格中按一下適當的資料格，並輸入新的值。 如需詳細資訊，請參閱 [將資料或記錄檔加入資料庫](add-data-or-log-files-to-a-database.md)。  
  
7.  若要變更資料庫的定序，請選取 **[選項]** 頁面，然後從清單中選取定序。  
  
8.  若要變更復原模式，請選取 **[選項]** 頁面，並從清單中選取復原模式。  
  
9. 若要變更資料庫選項，請選取 **[選項]** 頁面，然後修改資料庫選項。 如需每個選項的說明，請參閱 [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
10. 若要加入新的檔案群組，請按一下 **[檔案群組]** 頁面。 按一下 **[加入]** ，然後輸入檔案群組的值。  
  
11. 若要將擴充屬性加入至資料庫，請選取 **[擴充屬性]** 頁面。  
  
    1.  在 **[名稱]** 資料行中，輸入擴充屬性的名稱。  
  
    2.  在 **[值]** 資料行中，輸入擴充屬性文字。 例如，輸入一個或多個可說明資料庫的陳述。  
  
12. 若要建立資料庫，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-database"></a>若要建立資料庫  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會建立 `Sales`資料庫。 因為沒有使用關鍵字 PRIMARY，所以第一個檔案 (`Sales`_`dat`) 會成為主要檔案。 因為 `Sales`\_`dat` 檔的 SIZE 參數中沒有指定 MB 或 KB，所以它會使用 MB 並 MB 來配置。 每當建立、修改或卸除使用者資料庫時，都應該備份 `Sales`\_`log` 檔會以 MB 為單位配置，因為 `MB` 參數中明確陳述 `SIZE` 後置詞。  
  
```sql  
USE master ;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
 如需範例，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫檔案與檔案群組](database-files-and-filegroups.md)   
 [資料庫卸離和附加 &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [將資料或記錄檔加入資料庫](add-data-or-log-files-to-a-database.md)  
  
  
