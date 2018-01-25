---
title: "資料庫 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data warehouse [SQL Server]
- OLTP databases [SQL Server]
- databases [SQL Server], about databases
ms.assetid: 316eea58-81b8-4bf3-a1fc-801946740e94
caps.latest.revision: "27"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 947bbd87fca45f0647bffe38af8e51591799778c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="databases"></a>資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料庫是由資料表集合所組成，該集合內儲存了一組特定的結構資料。 而資料表中則包含資料列集合 (也稱為記錄或 Tuple) 和資料行 (也稱為屬性) 集合。 資料表中的每個資料行都是為了儲存某類型資訊而設計，例如，日期、名稱、金額和數字。  
  
## <a name="basic-information-about-databases"></a>資料庫的基本資訊  
 一部電腦可以安裝一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體都可以包含一個或多個資料庫。  在資料庫內，存在一個或多個物件擁有權群組 (稱為結構描述)。 在每個結構描述內，都會包含資料庫物件 (例如資料表、檢視及預存程序)。 部分物件 (例如憑證和非對稱金鑰) 是包含在資料庫內，但未包含在結構描述內。 如需有關建立資料表的詳細資訊，請參閱＜ [Tables](../../relational-databases/tables/tables.md)＞。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫是儲存在檔案系統的檔案中。 檔案可以分組為檔案群組。 如需有關檔案和檔案群組的詳細資訊，請參閱＜ [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)＞。  
  
 使用者在取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的存取權時會視為已登入。 使用者在取得資料庫的存取權時會視為資料庫使用者。 資料庫使用者可以根據登入來建立。 若啟用自主資料庫，則可建立不是根據登入的資料庫使用者。 如需使用者的詳細資訊，請參閱 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)。  
  
 具有資料庫存取權的使用者可以獲得存取資料庫中物件的權限。 雖然權限可以授與個別使用者，但是建議建立資料庫角色，並將資料庫使用者加入至角色，然後授與角色的存取權。 授與角色的權限，而非使用者的權限，如此即可在使用者數目成長並持續變更時，更輕鬆地保持權限的一致性，且使權限更容易了解。 如需角色權限的詳細資訊，請參閱 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md) 和[主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)。  
  
## <a name="working-with-databases"></a>使用資料庫  
 使用資料庫的大多數使用者都會使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 工具。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 工具具有用於建立資料庫和資料庫中物件的圖形化使用者介面。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 也具有查詢編輯器，可透過寫入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式與資料庫互動。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝磁碟進行安裝，或從 MSDN 進行下載。  
  
## <a name="in-this-section"></a>本節內容  
  
|||  
|-|-|  
|[系統資料庫](../../relational-databases/databases/system-databases.md)|[刪除資料庫的資料或記錄檔](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)|  
|[自主資料庫](../../relational-databases/databases/contained-databases.md)|[顯示資料庫的資料和記錄空間資訊](../../relational-databases/databases/display-data-and-log-space-information-for-a-database.md)|  
|[Microsoft Azure 中的 SQL Server 資料檔案](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)|[增加資料庫的大小](../../relational-databases/databases/increase-the-size-of-a-database.md)|  
|[資料庫檔案與檔案群組](../../relational-databases/databases/database-files-and-filegroups.md)|[重新命名資料庫](../../relational-databases/databases/rename-a-database.md)|  
|[資料庫狀態](../../relational-databases/databases/database-states.md)|[將資料庫設定為單一使用者模式](../../relational-databases/databases/set-a-database-to-single-user-mode.md)|  
|[檔案狀態](../../relational-databases/databases/file-states.md)|[壓縮資料庫](../../relational-databases/databases/shrink-a-database.md)|  
|[估計資料庫的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)|[壓縮檔案](../../relational-databases/databases/shrink-a-file.md)|  
|[複製資料庫至其他伺服器](../../relational-databases/databases/copy-databases-to-other-servers.md)|[檢視或變更資料庫的屬性](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)|  
|[資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)|[檢視 SQL Server 執行個體上的資料庫清單](../../relational-databases/databases/view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[將資料或記錄檔加入資料庫](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)|[檢視或變更資料庫的相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)|  
|[變更資料庫的組態設定](../../relational-databases/databases/change-the-configuration-settings-for-a-database.md)|[使用維護計畫精靈](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[建立資料庫](../../relational-databases/databases/create-a-database.md)|[建立使用者定義資料類型別名](../../relational-databases/databases/create-a-user-defined-data-type-alias.md)|  
|[刪除資料庫](../../relational-databases/databases/delete-a-database.md)|[資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a>相關內容  
 [索引](../../relational-databases/indexes/indexes.md)  
  
 [檢視](../../relational-databases/views/views.md)  
  
 [預存程序 &#40;Database Engine&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  
