---
title: "SQL Server Management Studio - 版本資訊 | Microsoft Docs"
ms.custom: 
ms.date: 06/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b95337b-80bf-4624-8f5d-cdaf6181d3b8
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: fe6de2b16b9792a5399b1c014af72a2a5ee52377
ms.openlocfilehash: f593303a681e2f52161777fc48f0fb1b479d20d9
ms.contentlocale: zh-tw
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-management-studio----release-notes"></a>SQL Server Management Studio -  版本資訊
歡迎使用 SQL Server Management Studio 正式推出版本！  此 SQL Server Management Studio (SSMS) 版本是 SQL Server 版本以外的獨立安裝。 我們的目標是透過新功能、修正，以及對 SQL Server 及 Azure SQL Database 中最新功能的支援，經常加以更新。  
  
若要安裝最新的 SQL Server Management Studio，請參閱[下載 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)。  
  
下列為此版本 SQL Server Management Studio 版本的問題與限制：  

1. **還原資料庫精靈會產生不正確的目的地資料庫檔案位置的路徑模式**
   這是已知的問題，當 SSMS 連接到 Linux 伺服器。 即使路徑看起來不正確/奇數，就會正確處理伺服器端上，也就是沒有任何功能的問題。

2. **檔案瀏覽器的問題**
    - 時使用的 Windows 基礎 SQL Server 2017 CTP 2.0 的執行個體，可能無法開啟空的磁碟機或固定的磁碟受安裝 Bitlocker 保護之伺服器是否檔案瀏覽器在 SSMS 中的 UI。 
    - 檔案瀏覽器 UI 已不再支援 SQL Server 2017 CTP 2.0 之前的版本。
    


3. **使用 Active Directory 通用驗證的 SSMS 執行個體只能以單一 Azure Active Directory 帳戶進行登入。**  
    此限制僅限於 Active Directory 通用驗證。您可以使用 Active Directory 密碼驗證、Active Directory 整合式驗證或 SQL Server 驗證登入不同的伺服器。
    
    因應措施為使用另一個 SSMS 執行個體來以另一個 Azure Active Directory 帳戶進行登入。 
    
4. **Data-Tier Application Framework (DacFx) 命令和 SSMS 中的結構描述設計工具不支援 Active Directory 通用驗證。**  
    使用 DacFx 的命令 (例如匯入與匯出)、SSMS 中的結構描述設計工具，目前並不支援 Active Directory 通用驗證。
    
    因應措施為使用 SSMS 所提供的其他形式驗證：Active Directory 密碼驗證、Active Directory 整合式驗證或 SQL Server 驗證。

5. **SSMS 只能連線到 SQL Server 2016 Integration Services (SSIS 2016) 執行個體。**  
    SQL Server Integration Services 具有會防止連線到先前版本的已知相容性限制。
    
    此問題的因應措施為使用 [與您的 SSIS 執行個體對齊的 SSMS 版本](../ssms/previous-sql-server-management-studio-releases.md)來連線到您的 SQL Server Integration Service 執行個體。 
  
5. **SSMS 不會儲存 SQL Server 2008 R2 和較早 SQL Server 版本的維護計畫。**  
    這是一個我們希望能於未來解決的已知限制。 在此期間，您可以使用 [SSMS 2014 版本](../ssms/previous-sql-server-management-studio-releases.md) 來儲存維護計畫。  
    
5. **非英文的 SSMS 安裝可能需要安裝額外的安全性套件。**  
非英文的 SSMS 語言版本如果安裝在 Windows 8、Windows 7、Windows Server 2012 及 Windows Server 2008 R2，就需要 [KB 2862966 安全性更新程式封裝](https://support.microsoft.com/en-us/kb/2862966) 。

5. **按一下 [說明] 或按 F1 鍵不會開啟說明**  
某些環境按一下 [說明] 或按下 F1 鍵時會顯示以下內容：**開啟 ms-xhelp 需要新的應用程式**。 這個錯誤是已知問題，會於近期版本中修正。
  
## <a name="feedback"></a>意見反應  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 用戶端工具論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 記錄問題或建議](https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Management Studio 教學課程](../ssms/use-sql-server-management-studio.md)  
[下載 SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[先前 SQL Server Management Studio 版本](../ssms/previous-sql-server-management-studio-releases.md)  

  

