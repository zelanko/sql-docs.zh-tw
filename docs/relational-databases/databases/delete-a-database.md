---
title: 刪除資料庫 | Microsoft 文件
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL，在 SQL Server 內 SQL Server Management Studio 中刪除使用者定義的資料庫。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database removal [SQL Server], SQL Server Management Studio
- removing databases
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- database removal [SQL Server]
ms.assetid: 1fd8c0f5-03e1-449a-af45-b8cacb479d9c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4a4665cd3b3f554c33a1c8640ee47dea94f911d6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85630664"
---
# <a name="delete-a-database"></a>刪除資料庫
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [!INCLUDE[tsql](../../includes/tsql-md.md)]刪除使用者定義資料庫。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [先決條件](#Prerequisites)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法刪除資料庫：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [刪除資料庫之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   您無法刪除系統資料庫。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   刪除資料庫上的資料庫快照集。 如需詳細資訊，請參閱 [卸除資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)執行個體。  
  
-   如果資料庫有相關的記錄傳送，請移除記錄傳送。  
  
-   如果資料庫已發行供異動複寫之用，或已發行至或訂閱合併式複寫，請移除資料庫的複寫。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   請考慮為資料庫進行完整備份。 已刪除的資料庫只能透過還原備份來重新建立。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 若要執行 DROP DATABASE，使用者至少必須對該資料庫具備 CONTROL 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-database"></a>若要刪除資料庫  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[資料庫]** ，以滑鼠右鍵按一下要刪除的資料庫，再按一下 **[刪除]** 。  
  
3.  確認已選取正確的資料庫，再按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-database"></a>若要刪除資料庫  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例會移除 `Sales` 和 `NewSales` 資料庫。  
  
```sql  
USE master ;  
GO  
DROP DATABASE Sales, NewSales ;  
GO  
```  
  
##  <a name="follow-up-after-deleting-a-database"></a><a name="FollowUp"></a> 後續操作：刪除資料庫之後  
 備份 **master** 資料庫。 如果必須還原 **master** ，在上次備份 **master** 之後被刪除的資料庫，還是會在系統目錄檢視中留有參考，並可能會造成錯誤訊息出現。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
