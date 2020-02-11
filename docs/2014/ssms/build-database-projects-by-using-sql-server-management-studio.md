---
title: 使用 SQL Server Management Studio 建置資料庫專案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], database projects
- database projects [SQL Server]
- projects [SQL Server Management Studio], about projects
- projects [SQL Server Management Studio]
ms.assetid: c2e80045-894d-44cf-b65c-e547ed738947
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 134ac290601e463063f78a59ea8fd5923d095663
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211261"
---
# <a name="build-database-projects-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 建置資料庫專案
  資料庫指令碼專案是一組有組織的指令碼、連接資訊及範本，而且全都與資料庫或資料庫某一部分有所關聯。 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]提供， [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]以便在腳本專案[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的內容中管理及設計資料庫。 
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 包含設計工具、編輯器、指南及精靈，可協助使用者開發、部署及維護資料庫。  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是一套系統管理工具，用以管理屬於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的元件。 這個整合式環境可讓使用者執行各種工作，如備份資料、編輯查詢，以及自動執行單一介面內的一般功能。  
  
 
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 包括下列工具：  
  
-   程式碼編輯器是一個豐富的指令碼編輯器，用以撰寫及編輯指令碼。 
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 提供四種版本的程式碼編輯器：適用於 [!INCLUDE[ssDE](../includes/ssde-md.md)] 指令碼的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢編輯器、DMX 查詢編輯器、MDX 查詢編輯器及 XML/A 查詢編輯器。  
  
-   物件總管，用以尋找、修改、執行屬於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的物件，或撰寫該物件的指令碼。  
  
-   範本總管，用以尋找範本及撰寫範本的指令碼。  
  
-   方案總管，用以組織相關的指令碼並將其儲存為專案的一部分。  
  
-   屬性視窗，用以顯示所選物件的目前屬性。  
  
 
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 藉由提供下列項目，支援有效率的工作程序：  
  
-   已中斷連接的存取。 您不需連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體，即可撰寫及編輯指令碼。  
  
-   從任何對話方塊撰寫指令碼。 您可以從任何對話方塊建立指令碼，以便可在建立指令碼之後加以讀取、修改及重複使用。  
  
-   非典型對話方塊。 當您存取 UI 對話方塊時，不需關閉此對話方塊，即可瀏覽 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的其他資源。  
  
## <a name="solutions-and-script-projects"></a>方案及指令碼專案  
 方案總管是用以儲存及重新開啟資料庫方案的公用程式。 方案會組織相關的指令碼專案及檔案。 指令碼專案會儲存 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 指令碼檔案、SQL 範本、連接資訊以及其他檔案。 當指令碼儲存到指令碼專案後，使用者可以：  
  
-   維護指令碼的版本控制。  
  
-   利用指令碼儲存結果選項。  
  
-   在單一指令碼專案中組織相關的指令碼。  
  
-   利用指令碼儲存連接資訊。  
  
 [方案總管] 為開發人員所適用的工具，他們會建立及重複使用與同一專案相關的指令碼。 如果稍後需要類似工作，您可以使用已儲存在專案中的指令碼群組。 如果您已使用[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]建立應用程式，您會發現方案總管非常熟悉。  
  
 方案是由一或多個指令碼專案所組成。 專案是由一或多個指令碼或連接所組成。 專案也可包含非指令碼檔案。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)   
 [查詢和文字編輯器 &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [方案 &#40;SQL Server Management Studio&#41;](solution/solutions-sql-server-management-studio.md)  
  
  
