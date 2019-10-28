---
title: 允許非管理員使用複寫監視器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: c5cd21759b7a59a639dbecea1b3e65109d3d4ff2
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908135"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>允許非管理員使用複寫監視器
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  本主題描述如何允許非管理員藉由使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中使用複寫監視器。 「複寫監視器」可供身為下列角色成員的使用者使用：  
  
-   **系統管理員 (sysadmin)** 固定伺服器角色。  
  
     這些使用者可監視複寫，並且擁有變更複寫屬性的完全控制，例如，代理程式排程、代理程式設定檔等。  
  
-   散發資料庫中的 **replmonitor** 資料庫角色。  
  
     這些使用者可監視複寫，但無法變更任何複寫屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要允許非管理員使用複寫監視器，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 若要允許非管理員的人使用「複寫監視器」， **系統管理員 (sysadmin)** 固定伺服器角色的成員必須將使用者加入至散發資料庫，並將該使用者指派至 **replmonitor** 角色。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>允許非管理員使用複寫監視器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中連接到散發者，然後展開伺服器節點。  
  
2.  展開 **[資料庫]** ，展開 **[系統資料庫]** ，並且展開散發資料庫 (預設名稱為 **distribution** )。  
  
3.  展開 **[安全性]** ，以滑鼠右鍵按一下 **[使用者]** ，再按一下 **[新增使用者]** 。  
  
4.  輸入使用者名稱及使用者的登入。  
  
5.  選取 **[replmonitor]** 的預設結構描述。  
  
6.  在 **[資料庫角色成員資格]** 方格中選取 **[replmonitor]** 。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>若要將使用者加入至 replmonitor 固定資料庫角色  
  
1.  在散發資料庫的「散發者」端，執行 [sp_helpuser &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)。 如果使用者未列於結果集中的 **UserName**，則必須使用 [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md) 陳述式，授與使用者散發資料庫的存取權。  
  
2.  在散發資料庫的散發者端執行 [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)，並針對 `@rolename` 參數指定 **replmonitor** 的值。 如果使用者列於結果集中的 **MemberName** ，則該使用者已屬於此角色。  
  
3.  如果使用者不屬於 **replmonitor** 角色，請在散發資料庫的「散發者」端執行 [sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)。 針對 `@rolename` 指定 **replmonitor** 的值和資料庫使用者的名稱，或為 `@membername` 新增 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 登入。  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>若要從 replmonitor 固定資料庫角色移除使用者  
  
1.  若要確認使用者屬於 **replmonitor** 角色，請在散發資料庫的散發者端執行 [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)，並針對 `@rolename` 指定 **replmonitor** 的值。 如果使用者未列於結果集中的 **MemberName** ，則該使用者目前不屬於此角色。  
  
2.  如果使用者屬於 **replmonitor** 角色，請在散發資料庫的「散發者」端執行 [sp_droprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)。 針對 `@rolename` 指定 **replmonitor** 的值和資料庫使用者名稱，或針對 `@membername` 指定正在移除的 Windows 登入。 
  
  
