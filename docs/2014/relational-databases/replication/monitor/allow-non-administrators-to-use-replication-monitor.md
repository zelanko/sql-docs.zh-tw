---
title: 允許非管理員使用複寫監視器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e8f03d12d3ac1695d4f6d000c8eab89a42004fd
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52776690"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>允許非管理員使用複寫監視器
  本主題描述如何允許非管理員藉由使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中使用複寫監視器。 「複寫監視器」可供身為下列角色成員的使用者使用：  
  
-   **系統管理員 (sysadmin)** 固定伺服器角色。  
  
     這些使用者可監視複寫，並且擁有變更複寫屬性的完全控制，例如，代理程式排程、代理程式設定檔等。  
  
-   `replmonitor`散發資料庫中的資料庫角色。  
  
     這些使用者可監視複寫，但無法變更任何複寫屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要允許非管理員使用複寫監視器，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 若要允許非管理員使用複寫監視器，隸屬**sysadmin**固定的伺服器角色必須將使用者新增至散發資料庫，並將指派到該使用者`replmonitor`角色。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>允許非管理員使用複寫監視器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中連接到散發者，然後展開伺服器節點。  
  
2.  展開 **[資料庫]**，展開 **[系統資料庫]**，並且展開散發資料庫 (預設名稱為 **distribution** )。  
  
3.  展開 **[安全性]**，以滑鼠右鍵按一下 **[使用者]**，再按一下 **[新增使用者]**。  
  
4.  輸入使用者名稱及使用者的登入。  
  
5.  選取 預設結構描述`replmonitor`。  
  
6.  選取 `replmonitor`中的核取方塊**資料庫角色成員資格**方格。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>若要將使用者加入至 replmonitor 固定資料庫角色  
  
1.  在散發資料庫的「散發者」端，執行 [sp_helpuser &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpuser-transact-sql)。 如果使用者未列在`UserName`在結果集中，使用者必須被授與散發資料庫使用的存取[USER &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-user-transact-sql)陳述式。  
  
2.  在散發資料庫的散發者端，執行[sp_helprolemember &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)，指定的值是`replmonitor`for **@rolename**參數。 如果使用者列於`MemberName`結果集中，使用者已屬於此角色。  
  
3.  如果使用者不屬於`replmonitor`角色中，執行[sp_addrolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)散發者端的散發資料庫。 指定的值為`replmonitor`for **@rolename**和資料庫使用者的名稱或[!INCLUDE[msCoName](../../../includes/msconame-md.md)]所新增的 Windows 登入**@membername**。  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>若要從 replmonitor 固定資料庫角色移除使用者  
  
1.  若要確認使用者屬於`replmonitor`角色，執行[sp_helprolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)的散發者上散發資料庫中，並指定其值為`replmonitor`如**@rolename**. 如果使用者未列於結果集中的 `MemberName`，則該使用者目前不屬於此角色。  
  
2.  如果使用者屬於`replmonitor`角色中，執行[sp_droprolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)散發者端的散發資料庫。 指定的值為`replmonitor`針對**@rolename**和 資料庫使用者或所移除的 Windows 登入的名稱**@membername**。  
  
  
