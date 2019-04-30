---
title: 設定全文檢索篩選背景程式啟動器的服務帳戶 | Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d702e1dcf8bc710324e7593ebe469317d9f43e68
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63237909"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>設定全文檢索篩選背景程式啟動器的服務帳戶
  此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來為 SQL 全文檢索篩選背景程式啟動器服務 (MSSQLFDLauncher) 設定服務帳戶。 ssNoVersion 全文檢索搜尋使用 SQL 全文檢索篩選背景程式啟動器服務，來啟動篩選背景程式主機處理序，以便處理全文檢索搜尋篩選和斷詞。 若要使用全文檢索搜尋，您必須執行這個服務。  
  
 SQL 全文檢索篩選背景程式啟動器服務是與特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體相關聯的執行個體感知服務。 SQL 全文檢索篩選背景程式啟動器服務會將服務帳戶資訊傳播給每個篩選背景程式主機處理序。  
  
  
##  <a name="setting"></a> 設定服務帳戶  
  
#### <a name="to-set-the-sql-full-text-filter-daemon-launcher-service-account-for-full-text-search"></a>設定全文檢索搜尋的 SQL 全文檢索篩選背景程式啟動器服務帳戶  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
2.  在  **SQL Server 組態管理員**，按一下**SQL Server 服務**，以滑鼠右鍵按一下**SQL 全文檢索篩選背景程式啟動器 (*`instance name`*)**，然後按一下**屬性**。  
  
3.  按一下對話方塊的 [登入] 索引標籤，然後選取或輸入用以執行 SQL 全文檢索篩選背景程式啟動器服務所建立之每個處理序的帳戶。  
  
4.  在您關閉對話方塊之後，請按一下 [重新啟動]  重新啟動 SQL 全文檢索篩選背景程式啟動器服務。  
  
  
##  <a name="error"></a> 如果 SQL 全文檢索篩選背景程式啟動器服務就無法啟動  
 若未啟動 SQL 全文檢索篩選背景程式啟動器服務，則可能是下列其中一個或多個原因所造成：  
  
-   與 SQL 全文檢索篩選背景程式啟動器服務帳戶相關聯的密碼已過期。  
  
     若您針對 SQL 全文檢索篩選背景程式啟動器服務使用本機使用者帳戶，而且密碼已過期，您就必須：  
  
    1.  設定帳戶的新 Windows 密碼。  
  
    2.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中，更新 SQL 全文檢索篩選背景程式啟動器服務以使用新的密碼。  
  
-   服務帳戶的使用者帳戶或密碼不正確。  
  
     SQL 全文檢索篩選背景程式啟動器服務可能嘗試使用不正確的使用者帳戶和密碼登入。 請遵循以上程序，確認此服務的使用者帳戶尚未變更。  
  
-   用於登入此服務的帳戶沒有權限。  
  
     您可能使用了在安裝伺服器執行個體的電腦上沒有登入權限的帳戶。 請確認您用於登入的帳戶確實具有本機電腦的使用者權限。  
  
-   相同具名管道的另一個執行個體已經在執行中。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務會當做 SQL 全文檢索篩選背景程式啟動器服務用戶端的具名管道伺服器。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動之前已經由另一個處理序建立此具名管道，則會有錯誤記錄到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔和 Windows 事件記錄檔中，而且將無法使用全文檢索搜尋。  請判斷哪一個處理序或應用程式正在嘗試使用相同的具名管道，並停止應用程式。  
  
-   SQL 全文檢索篩選背景程式啟動器服務的設定不正確。  
  
     本機電腦上可能未正確設定此服務。  
  
     如果本機電腦上已停用具名管道功能，或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已設定成使用非預設具名管道的具名管道，則 SQL 全文檢索篩選背景程式啟動器服務可以無法啟動。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務群組沒有啟動 SQL 全文檢索篩選背景程式啟動器服務的權限。  
  
     在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝期間，會將管理、查詢及啟動 SQL 全文檢索篩選背景程式啟動器服務的預設權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務群組。 如果在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後已經移除 SQL 全文檢索篩選背景程式啟動器服務帳戶的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務群組權限，SQL 全文檢索篩選背景程式啟動器服務將不會啟動，而且全文檢索搜尋將會停用。 請確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務群組具有 SQL 全文檢索篩選背景程式啟動器服務帳戶的權限。  
  
  
## <a name="see-also"></a>另請參閱  
 [管理服務的如何主題 &#40;SQL Server 組態管理員&#41;](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)  
 [升級全文檢索搜尋](upgrade-full-text-search.md)  
  
  
