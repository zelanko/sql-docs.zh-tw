---
title: "建立中央管理伺服器和伺服器群組 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: configuration server
ms.assetid: da265482-3953-440a-ac23-0ab7e42a55eb
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 712440c9f508da793757ba2f4097eef46426df91
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-central-management-server-and-server-group"></a>建立中央管理伺服器和伺服器群組
  本主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體指定為 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的中央管理伺服器。 中央管理伺服器會儲存組織成一個或多個中央管理伺服器群組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體清單。 使用中央管理伺服器群組所採取的動作將會在伺服器群組中的所有伺服器上運作。 這包括使用 [物件總管] 來連接至伺服器，以及同時在多部伺服器上執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式和以原則為基礎的管理原則。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本無法指定為中央管理伺服器。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **使用下列方法建立中央管理伺服器和伺服器群組：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 msdb 資料庫中的兩個資料庫角色會授與中央管理伺服器的存取權。 只有 ServerGroupAdministratorRole 角色的成員可以管理中央管理伺服器。 您需要 ServerGroupReaderRole 角色的成員資格才能連接至中央管理伺服器。  
  
 由於中央管理伺服器所維護的連接會在使用者的內容中執行，所以使用 Windows 驗證時，已註冊之伺服器上的有效權限可能會不同。 例如，雖然使用者可能是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A 執行個體上系統管理員 (sysadmin) 固定伺服器角色的成員，但是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B 執行個體上具有有限的權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 下列程序描述如何執行下列步驟。  
  
1.  建立中央管理伺服器。  
  
2.  將一個或多個伺服器群組加入至中央管理伺服器，並將一個或多個已註冊的伺服器加入至伺服器群組。  
  
#### <a name="create-a-central-management-server"></a>建立中央管理伺服器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 **[檢視]** 功能表中，按一下 **[已註冊的伺服器]**。  
  
2.  在 [已註冊的伺服器] 中，展開 [Database Engine]，以滑鼠右鍵按一下 [中央管理伺服器]，然後按一下 [註冊中央管理伺服器]。  
  
3.  在 [新增伺服器註冊] 對話方塊中，從伺服器下拉式清單中選取您想要成為中央管理伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 中央管理伺服器必須使用 Windows 驗證。  
  
4.  在 **[已註冊的伺服器]**，輸入伺服器名稱和選擇性描述。  
  
5.  從 **[連接屬性]** 索引標籤，檢閱或修改網路和連接屬性。 如需詳細資訊，請參閱[連接到伺服器 &#40;連接屬性頁面&#41; Database Engine](http://msdn.microsoft.com/library/edc1143c-6a47-4b02-92ab-441bdea8ea8a)  
  
6.  按一下 **[測試]**測試連接。  
  
7.  按一下 **[儲存]**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會出現在 **[中央管理伺服器]** 資料夾底下。  
  
#### <a name="create-a-new-server-group-and-add-servers-to-the-group"></a>建立新的伺服器群組並將伺服器加入至群組  
  
1.  從 **[已註冊的伺服器]**，展開 **[中央管理伺服器]**。 以滑鼠右鍵按一下上述程序中加入的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，然後選取 [新增伺服器群組]。  
  
2.  在 **[新增伺服器群組屬性]**，輸入群組名稱和選擇性描述。  
  
3.  在 [已註冊的伺服器] 中，以滑鼠右鍵按一下伺服器群組，然後按一下 [新增伺服器註冊]。  
  
4.  從 [新增伺服器註冊]，選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱[建立新的已註冊伺服器 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)。 適當地加入其他伺服器。  
  
#### <a name="to-execute-queries-against-several-configuration-targets-at-the-same-time"></a>若要同時針對數個組態目標執行查詢  
  
-   在您建立中央管理伺服器、一個或多個伺服器群組以及一個或多個已註冊的伺服器之後，就可以同時針對整個群組執行查詢。 如需有關如何同時執行伺服器群組中伺服器之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的詳細資訊，請參閱[同時針對多部伺服器執行陳述式 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/execute-statements-against-multiple-servers-simultaneously.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用中央管理伺服器管理多部伺服器](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
