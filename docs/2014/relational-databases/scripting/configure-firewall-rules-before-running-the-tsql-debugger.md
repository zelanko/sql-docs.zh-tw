---
title: 設定 Transact-SQL 偵錯工具
ms.custom: seo-lt-2019
ms.date: 10/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vs.debug.error.sqlde_register_failed
- vs.debug.error.sqlde_accessdenied
- vs.debug.error.sqlde_firewall.remotemachines
helpviewer_keywords:
- Transact-SQL debugger, remote connections
- Windows Firewall [Database Engine], Transact-SQL debugger
- Transact-SQL debugger, Windows Firewall
- Transact-SQL debugger, configuring
- ports [SQL Server], Transact-SQL debugger
- TCP/IP [SQL Server], port numbers
ms.assetid: f50e0b0d-eaf0-4f4a-be83-96f5be63e7ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60d5af2752a426faca3069541deeae3a6aa4f495
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245194"
---
# <a name="configure-the-transact-sql-debugger"></a>設定 Transact-SQL 偵錯工具
  當連接的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 執行個體與 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器在不同的電腦上執行時，就必須設定 Windows 防火牆規則才能啟用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 偵錯。  
  
## <a name="configuring-the-transact-sql-debugger"></a>設定 Transact-SQL 偵錯工具  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具同時包含伺服器端和用戶端元件。 伺服器端的偵錯工具元件會隨著 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 (SP2) 或更新版本中的每個 Database Engine 執行個體一起安裝。 包括用戶端偵錯工具元件的情況：  
  
-   當您從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本安裝用戶端工具時。  
  
-   當您安裝 Microsoft Visual Studio 2010 或更新版本時。  
  
-   當您從 Web 下載安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 時。  
  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 與 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 執行個體在同一部電腦上執行時，沒有任何執行 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]偵錯工具的組態需求。 不過，當連接至遠端 [!INCLUDE[tsql](../../includes/tsql-md.md)] 執行個體時，若要執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)]偵錯工具，就必須在這兩部電腦上啟用 Windows 防火牆中的程式和通訊埠規則。 這些規則可以由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式建立。 如果您嘗試開啟遠端偵錯工作階段時發生錯誤，請確定您的電腦上已定義下列防火牆規則。  
  
 使用 [具有進階安全性的 Windows 防火牆]**** 應用程式來管理防火牆規則。 在 [!INCLUDE[win7](../../includes/win7-md.md)] 和 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 中，開啟 [控制台]****，開啟 [Windows 防火牆]****，然後選取 [進階設定]****。 在 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 中，您也可以開啟 [服務管理員]****，然後展開左窗格中的 [組態]****，再展開 [具有進階安全性的 Windows 防火牆]****。  
  
> [!CAUTION]  
>  在 [Windows 防火牆] 中啟用規則可能會讓您的電腦暴露在防火牆設計可封鎖的安全性威脅下。 啟用遠端偵錯規則會解除封鎖本主題中列出的通訊埠和程式。  
  
## <a name="firewall-rules-on-the-server"></a>伺服器上的防火牆規則  
 在執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的電腦上，使用 [具有進階安全性的 Windows 防火牆]**** 指定下列資訊：  
  
-   加入 sqlservr.exe 的輸入程式規則。 每一個需要支援遠端偵錯工作階段的執行個體都必須有一項規則。  
  
    1.  在 [具有進階安全性的 Windows 防火牆]**** 的左窗格中，以滑鼠右鍵按一下 [輸入規則]****，再從動作窗格選取 [新增規則]****。  
  
    2.  在 [規則類型]**** 對話方塊中，選取 [程式]****，然後按一下 [下一步]****。  
  
    3.  在 [程式]**** 對話方塊中，選取 [這個程式路徑]****，然後輸入此執行個體的 sqlservr.exe 完整路徑。 根據預設，sqlservr.exe 安裝在 C:\Program Files\Microsoft SQL Server\MSSQL12. 中。*Instancename*\MSSQL\Binn，其中*instancename*是預設實例的 MSSQLSERVER，以及任何已命名實例的實例名稱。  
  
    4.  在 [動作]**** 對話方塊中，選取 [允許連線]****，然後按一下 [下一步]****。  
  
    5.  在 [設定檔]**** 對話方塊中，選取描述您想要開啟執行個體之偵錯工作階段時電腦連線環境的任何設定檔，然後按一下 [下一步]****。  
  
    6.  在 [名稱]**** 對話方塊中，輸入此規則的名稱和描述，然後按一下 [完成]****。  
  
    7.  在 [輸入規則]**** 清單中，以滑鼠右鍵按一下您建立的規則，然後選取動作窗格中的 [屬性]****。  
  
    8.  選取 [通訊協定及連接埠]**** 索引標籤。  
  
    9. 在 [通訊協定類型:]**** 方塊中選取 [TCP]****，在 [本機通訊埠:]**** 方塊中選取 [RPC 動態通訊埠]****，按一下 [套用]****，再按一下 [確定]****。  
  
-   加入 svchost.exe 的輸入程式規則可啟用來自遠端偵錯工具工作階段的 DCOM 通訊。  
  
    1.  在 [具有進階安全性的 Windows 防火牆]**** 的左窗格中，以滑鼠右鍵按一下 [輸入規則]****，再從動作窗格選取 [新增規則]****。  
  
    2.  在 [規則類型]**** 對話方塊中，選取 [程式]****，然後按一下 [下一步]****。  
  
    3.  在 [程式]**** 對話方塊中，選取 [這個程式路徑:]****，然後輸入 svchost.exe 的完整路徑。 根據預設，svchost.exe 安裝於 %systemroot%\System32\svchost.exe。  
  
    4.  在 [動作]**** 對話方塊中，選取 [允許連線]****，然後按一下 [下一步]****。  
  
    5.  在 [設定檔]**** 對話方塊中，選取描述您想要開啟執行個體之偵錯工作階段時電腦連線環境的任何設定檔，然後按一下 [下一步]****。  
  
    6.  在 [名稱]**** 對話方塊中，輸入此規則的名稱和描述，然後按一下 [完成]****。  
  
    7.  在 [輸入規則]**** 清單中，以滑鼠右鍵按一下您建立的規則，然後選取動作窗格中的 [屬性]****。  
  
    8.  選取 [通訊協定及連接埠]**** 索引標籤。  
  
    9. 在 [通訊協定類型:]**** 方塊中選取 [TCP]****，在 [本機通訊埠:]**** 方塊中選取 [RPC 端點對應程式]****，按一下 [套用]****，再按一下 [確定]****。  
  
-   如果網域原則要求透過 IPsec 完成網路通訊，您也必須加入開啟 UDP 通訊埠 4500 和 UDP 通訊埠 500 的輸入規則。  
  
## <a name="firewall-rules-on-the-client"></a>用戶端上的防火牆規則  
 在執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器的電腦上，SQL Server 安裝程式或 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 安裝程式可能已將 Windows 防火牆設定為允許遠端偵錯。  
  
 如果您嘗試開啟遠端偵錯工作階段時發生錯誤，可以使用 [具有進階安全性的 Windows 防火牆]**** 設定防火牆規則，手動設定程式和通訊埠例外狀況：  
  
-   加入 svchost 的程式項目：  
  
    1.  在 [具有進階安全性的 Windows 防火牆]**** 的左窗格中，以滑鼠右鍵按一下 [輸入規則]****，再從動作窗格選取 [新增規則]****。  
  
    2.  在 [規則類型]**** 對話方塊中，選取 [程式]****，然後按一下 [下一步]****。  
  
    3.  在 [程式]**** 對話方塊中，選取 [這個程式路徑:]****，然後輸入 svchost.exe 的完整路徑。 根據預設，svchost.exe 安裝於 %systemroot%\System32\svchost.exe。  
  
    4.  在 [動作]**** 對話方塊中，選取 [允許連線]****，然後按一下 [下一步]****。  
  
    5.  在 [設定檔]**** 對話方塊中，選取描述您想要開啟執行個體之偵錯工作階段時電腦連線環境的任何設定檔，然後按一下 [下一步]****。  
  
    6.  在 [名稱]**** 對話方塊中，輸入此規則的名稱和描述，然後按一下 [完成]****。  
  
    7.  在 [輸入規則]**** 清單中，以滑鼠右鍵按一下您建立的規則，然後選取動作窗格中的 [屬性]****。  
  
    8.  選取 [通訊協定及連接埠]**** 索引標籤。  
  
    9. 在 [通訊協定類型:]**** 方塊中選取 [TCP]****，在 [本機通訊埠:]**** 方塊中選取 [RPC 端點對應程式]****，按一下 [套用]****，再按一下 [確定]****。  
  
-   針對裝載 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器的應用程式加入程式項目。 如果您需要在同一部電腦上同時從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 開啟遠端偵錯工作階段，則必須針對兩者加入程式規則：  
  
    1.  在 [具有進階安全性的 Windows 防火牆]**** 的左窗格中，以滑鼠右鍵按一下 [輸入規則]****，再從動作窗格選取 [新增規則]****。  
  
    2.  在 [規則類型]**** 對話方塊中，選取 [程式]****，然後按一下 [下一步]****。  
  
    3.  在 [程式]**** 對話方塊中，選取 [這個程式路徑:]****，然後輸入下列三個值的其中一個。  
  
        -   針對 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]輸入 ssms.exe 的完整路徑。 根據預設，ssms.exe 安裝於 C:\Program Files (x86)\Microsoft SQL Server\120\Tools\Binn\Management Studio。  
  
        -   針對 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 輸入 devenv.exe 的完整路徑：  
  
            1.  根據預設，Visual Studio 2010 的 devenv.exe 位於 C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE。  
  
            2.  根據預設，Visual Studio 2012 的 devenv.exe 位於 C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE  
  
            3.  您可以從用來啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的捷徑找到 ssms.exe 的路徑。 您可以從用來啟動 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的捷徑找到 devenv.exe 的路徑。 以滑鼠右鍵按一下捷徑，然後選取 [屬性]****。 可執行檔和路徑會在 [目標]**** 方塊中列出。  
  
    4.  在 [動作]**** 對話方塊中，選取 [允許連線]****，然後按一下 [下一步]****。  
  
    5.  在 [設定檔]**** 對話方塊中，選取描述您想要開啟執行個體之偵錯工作階段時電腦連線環境的任何設定檔，然後按一下 [下一步]****。  
  
    6.  在 [名稱]**** 對話方塊中，輸入此規則的名稱和描述，然後按一下 [完成]****。  
  
    7.  在 [輸入規則]**** 清單中，以滑鼠右鍵按一下您建立的規則，然後選取動作窗格中的 [屬性]****。  
  
    8.  選取 [通訊協定及連接埠]**** 索引標籤。  
  
    9. 在 [通訊協定類型:]**** 方塊中選取 [TCP]****，在 [本機通訊埠:]**** 方塊中選取 [RPC 動態通訊埠]****，按一下 [套用]****，再按一下 [確定]****。  
  
## <a name="requirements-for-starting-the-debugger"></a>啟動偵錯工具的需求  
 啟動 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具的所有嘗試也必須符合下列需求：  
  
* 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 必須在屬於系統管理員固定伺服器角色成員的 Windows 帳戶底下執行。  
  
* 您必須使用屬於系統管理員 (sysadmin) 固定伺服器角色成員的 Windows 驗證或 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 驗證登入來連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢編輯器視窗。  
  
* 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器視窗必須連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Service Pack 2 (SP2) 或更新版本中的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體。 當 [查詢編輯器] 視窗連接至處於單一使用者模式下的執行個體時，您就無法執行偵錯工具。

* 伺服器必須透過 RPC 回應用戶端。 執行 SQL Server 服務的帳戶應該要有用戶端的驗證許可權。  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 偵錯工具](transact-sql-debugger.md)   
 [執行 Transact-sql 偵錯工具](run-the-transact-sql-debugger.md)   
 [逐步執行 Transact-sql 程式碼](step-through-transact-sql-code.md)   
 [Transact-SQL 偵錯工具資訊](transact-sql-debugger-information.md)   
 [Database Engine 查詢編輯器 &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)  
  
  
