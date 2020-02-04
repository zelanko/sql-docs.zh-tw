---
title: 同時對多部伺服器執行陳述式
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- executing queries against multiple servers
- queries [SQL Server], multiserver
ms.assetid: 197760f3-0a06-43de-8162-69c27d3fbe56
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/18/2016
ms.openlocfilehash: 89e6e64f4e4dc5f3ae7c8f9adf1db3a392530989
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75246564"
---
# <a name="execute-statements-against-multiple-servers-simultaneously"></a>同時對多部伺服器執行陳述式

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本主題描述如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，透過建立本機伺服器群組或中央管理伺服器及一個或多個伺服器群組，以及位於這些群組內部的一個或多個已註冊的伺服器，然後查詢完整的群組的方式，同時查詢多部伺服器。 

此查詢傳回的結果可以結合到單一結果窗格中，也可以在不同的結果窗格中傳回。 結果集可能包括伺服器名稱以及查詢在每部伺服器上使用之登入的額外資料行。 中央管理伺服器和從屬伺服器可以使用 Windows 驗證來註冊。 本機伺服器群組中的伺服器則可以使用 Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行註冊。  
  
> **注意！** 在您執行下列程序之前，請先建立中央管理伺服器和伺服器群組。 如需詳細資訊，請參閱[建立中央管理伺服器和伺服器群組 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)。  

  
##  <a name="Permissions"></a> 權限  
 由於中央管理伺服器所維護的連接會在使用者的內容中執行，所以使用 Windows 驗證時，已註冊之伺服器上的有效權限可能會不同。 例如，雖然使用者可能是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A 執行個體上系統管理員 (sysadmin) 固定伺服器角色的成員，但是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B 執行個體上具有有限的權限。  
  
 ## <a name="execute-statements-against-multiple-configuration-targets-simultaneously"></a>同時針對多個組態目標執行陳述式  

1.  在 SQL Server Management Studio 的 [檢視]  功能表上，按一下 [已註冊的伺服器]  。  
  
2.  展開中央管理伺服器，以滑鼠右鍵按一下伺服器群組，指向 [連接]  ，然後按一下 [新增查詢]  。  
  
3.  在 [查詢編輯器] 中，輸入並執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，例如下列陳述式：  
  
    ```  
    USE master  
    GO  
    SELECT * FROM sysdatabases;  
    GO  
    ```  
  
     根據預設，結果窗格將會結合伺服器群組中所有伺服器的查詢結果。  
  
#### <a name="to-change-the-multiserver-results-options"></a>變更多伺服器結果選項  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的 **[工具]** 功能表上，按一下 **[選項]** 。  
  
2.  展開 **[查詢結果]** 、展開 **[SQL Server]** ，然後按一下 **[多伺服器結果]** 。  
  
3.  在 **[多伺服器結果]** 頁面上，指定您想要的選項設定，然後按一下 **[確定]** 。  
  
## <a name="see-also"></a>另請參閱  
 [使用中央管理伺服器管理多部伺服器](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
