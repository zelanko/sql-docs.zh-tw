---
title: "設定全文檢索篩選背景程式啟動器的服務帳戶 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4f860080278519f5c9a68619ee5a9e8c0a2292f9
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>設定全文檢索篩選背景程式啟動器的服務帳戶
 此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來為 SQL 全文檢索篩選背景程式啟動器服務 (MSSQLFDLauncher) 設定或變更服務帳戶。 SQL Server 安裝程式所使用的預設服務帳戶是 `NT Service\MSSQLFDLauncher`。
  
  
## <a name="about-the-sql-full-text-filter-daemon-launcher-service"></a>關於 SQL 全文檢索篩選背景程式啟動器服務
SQL Server 全文檢索搜尋使用 SQL 全文檢索篩選背景程式啟動器服務，來啟動篩選背景程式主機處理序，以便處理全文檢索搜尋篩選和斷詞。 若要使用全文檢索搜尋，您必須執行啟動器服務。  
  
SQL 全文檢索篩選背景程式啟動器服務是與特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體相關聯的執行個體感知服務。 SQL 全文檢索篩選背景程式啟動器服務會將服務帳戶資訊傳播給所啟動的每個篩選背景程式主機處理序。  

##  <a name="setting"></a> 設定服務帳戶  
  
1.  在 [開始] 功能表上，指向 [所有程式]，展開 [[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]，然後按一下 [SQL Server 2016 組態管理員]。  
  
2.  在 [SQL Server 組態管理員] 中，按一下 [SQL Server 服務]，以滑鼠右鍵按一下 **[SQL 全文檢索篩選背景程式啟動器 (**執行個體名稱**)]**，然後按一下 [屬性]。  
  
3.  按一下對話方塊的 [登入] 索引標籤，然後選取或輸入用以執行 SQL 全文檢索篩選背景程式啟動器服務所啟動之處理序的帳戶。  
  
4.  在您關閉對話方塊之後，請按一下 [重新啟動]  重新啟動 SQL 全文檢索篩選背景程式啟動器服務。  
  
![SQL 全文檢索篩選背景程式啟動器處理序屬性](../../relational-databases/search/media/sql-full-text-filter-daemon-launch-process-properties.png)
  
##  <a name="error"></a> 針對 SQL 全文檢索篩選背景程式啟動器服務未啟動進行疑難排解  
 若未啟動 SQL 全文檢索篩選背景程式啟動器服務，請檢閱下列可能的原因：  
  
### <a name="permissions-issues"></a>權限問題
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務群組沒有啟動 SQL 全文檢索篩選背景程式啟動器服務的權限。  

     請確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務群組具有 SQL 全文檢索篩選背景程式啟動器服務帳戶的權限。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝期間，會將管理、查詢及啟動 SQL 全文檢索篩選背景程式啟動器服務的預設權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務群組。 如果在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後已經移除 SQL 全文檢索篩選背景程式啟動器服務帳戶的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務群組權限，SQL 全文檢索篩選背景程式啟動器服務將不會啟動，而且全文檢索搜尋將會停用。     

-   用於登入此服務的帳戶沒有權限。  
  
     您可能使用了在安裝伺服器執行個體的電腦上沒有登入權限的帳戶。 請確認您用於登入的帳戶確實具有本機電腦的使用者權限。  

### <a name="service-account-and-password-issues"></a>服務帳戶和密碼問題
-   服務帳戶的使用者帳戶或密碼不正確。  
  
     在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 組態管理員] 中，請確認服務所使用的服務帳戶和密碼正確無虞。  
  
-   與 SQL 全文檢索篩選背景程式啟動器服務帳戶相關聯的密碼已過期。  
  
     若您針對 SQL 全文檢索篩選背景程式啟動器服務使用本機使用者帳戶，而密碼已過期，您就必須：  
  
    1.  設定帳戶的新 Windows 密碼。  
  
    2.  在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 組態管理員] 中，更新 SQL 全文檢索篩選背景程式啟動器服務以使用新的密碼。  
  
### <a name="named-pipes-configuration-issues"></a>具名管道組態問題
-   SQL 全文檢索篩選背景程式啟動器服務的設定不正確。  
  
     如果本機電腦上已停用具名管道功能，或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已設定成使用非預設具名管道的具名管道，則 SQL 全文檢索篩選背景程式啟動器服務可以無法啟動。  
  
-   相同具名管道的另一個執行個體已經在執行中。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務會當做 SQL 全文檢索篩選背景程式啟動器服務用戶端的具名管道伺服器。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動之前已經由另一個處理序建立此具名管道，則會有錯誤記錄到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔和 Windows 事件記錄檔中，而且將無法使用全文檢索搜尋。  請判斷哪一個處理序或應用程式正在嘗試使用相同的具名管道，並停止應用程式。  
  
## <a name="see-also"></a>另請參閱  
 [管理服務的如何主題 &#40;SQL Server 組態管理員&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)   
 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
