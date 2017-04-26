---
title: "SQL Server Management Studio - 版本資訊 | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 51e336a22d0c1052c48b8e569330aef26f2af094
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio----release-notes"></a>SQL Server Management Studio -  版本資訊
歡迎使用 SQL Server Management Studio 正式推出版本！  此 SQL Server Management Studio (SSMS) 版本是 SQL Server 版本以外的獨立安裝。 我們的目標是透過新功能、修正，以及對 SQL Server 及 Azure SQL Database 中最新功能的支援，經常加以更新。  
  
若要安裝最新的 SQL Server Management Studio，請參閱[下載 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)。  
  
下列為此版本 SQL Server Management Studio 版本的問題與限制：  

1. **使用 Active Directory 通用驗證的 SSMS 執行個體只能以單一 Azure Active Directory 帳戶進行登入。**  
    此限制僅限於 Active Directory 通用驗證。您可以使用 Active Directory 密碼驗證、Active Directory 整合式驗證或 SQL Server 驗證登入不同的伺服器。
    
    因應措施為使用另一個 SSMS 執行個體來以另一個 Azure Active Directory 帳戶進行登入。 
    
2. **Data-Tier Application Framework (DacFx) 命令和 SSMS 中的結構描述設計工具不支援 Active Directory 通用驗證。**  
    使用 DacFx 的命令 (例如匯入與匯出)、SSMS 中的結構描述設計工具，目前並不支援 Active Directory 通用驗證。
    
    因應措施為使用 SSMS 所提供的其他形式驗證：Active Directory 密碼驗證、Active Directory 整合式驗證或 SQL Server 驗證。

3. **SSMS 只能連線到 SQL Server 2016 Integration Services (SSIS 2016) 執行個體。**  
    SQL Server Integration Services 具有會防止連線到先前版本的已知相容性限制。
    
    此問題的因應措施為使用 [與您的 SSIS 執行個體對齊的 SSMS 版本](../ssms/previous-sql-server-management-studio-releases.md)來連線到您的 SQL Server Integration Service 執行個體。 
  
4. **SSMS 不會儲存 SQL Server 2008 R2 和較早 SQL Server 版本的維護計畫。**  
    這是一個我們希望能於未來解決的已知限制。 在此期間，您可以使用 [SSMS 2014 版本](../ssms/previous-sql-server-management-studio-releases.md) 來儲存維護計畫。  
    
5. **非英文的 SSMS 安裝可能需要安裝額外的安全性套件。**  
非英文的 SSMS 語言版本如果安裝在 Windows 8、Windows 7、Windows Server 2012 及 Windows Server 2008 R2，就需要 [KB 2862966 安全性更新程式封裝](https://support.microsoft.com/en-us/kb/2862966) 。
  
6. **如果用戶端電腦上沒有安裝 SQL Server，SQL Server 組態管理員將無法啟動**  
    如果您沒有在用戶端電腦上安裝 SQL Server，並啟動 SQL Server 組態管理員，您將會看見下列錯誤：   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * 如果您已將 SQL Server 執行個體加入 SSMS 中的 [已註冊的伺服器] 清單：  
        1. 瀏覽到 SSMS 中的 [已註冊的伺服器] 檢視。  
        2. 以滑鼠右鍵按一下您想要設定的 SQL Server 執行個體。  
        3. 從右鍵功能表選取 [SQL Server 組態管理員...]。    
          
      * 如果您尚未將 SQL Server 執行個體加入 SSMS 中的 [已註冊的伺服器] 清單：  
        1. 以系統管理員身分開啟命令提示字元。  
        2. 使用下列命令執行 Mofcomp 工具：  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. 執行 Mofcomp 工具之後，請執行下列命令以重新啟動 WMI 服務讓變更生效：  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  

## <a name="feedback"></a>意見反應  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 用戶端工具論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 記錄問題或建議](https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Management Studio 教學課程](../ssms/use-sql-server-management-studio.md)  
[下載 SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[先前 SQL Server Management Studio 版本](../ssms/previous-sql-server-management-studio-releases.md)  

  

