---
title: 檢視離線記錄檔 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer, viewing offline logs
- offline log files
ms.assetid: 9223e474-f224-4907-a4f2-081e11db58f5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 814bfdd9c44170cc25f8dbd7eabcfd78ebde2a7d
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908562"
---
# <a name="view-offline-log-files"></a>檢視離線記錄檔
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，當目標執行個體已離線或無法啟動時，您就可以從本機或遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔。  
  
 您可以從 [已註冊的伺服器] 存取離線記錄檔，也可以透過 WMI 和 WQL (WMI 查詢語言) 查詢以程式設計方式存取。  
  
> [!NOTE]  
>  此外，您還可以使用這些方法來連接至已離線，但由於某些原因而無法透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接進行連接的執行個體。  
  
## <a name="before-you-begin"></a>開始之前  
 若要連接至離線記錄檔， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體必須安裝在您用來檢視離線記錄檔的電腦上以及您想要檢視之記錄檔所在的電腦上。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體安裝在這兩部電腦上，您就可以檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的離線記錄檔，以及在任何一部電腦上執行舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之執行個體的離線記錄檔。  
  
 如果您在使用 [已註冊的伺服器]，則所要連接的目標執行個體就必須在 [本機伺服器群組]  或 [中央管理伺服器]  底下註冊。 (此執行個體可獨立註冊，或成為伺服器群組的成員)。如需有關如何將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體加入至 [已註冊的伺服器] 的詳細資訊，請參閱下列主題：  
  
-   [建立或編輯伺服器群組 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [註冊連接的伺服器 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/register-a-connected-server-sql-server-management-studio.md)  
  
-   [建立中央管理伺服器與伺服器群組 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)  
  
 如需有關如何透過 WMI 和 WQL 查詢以程式設計方式檢視離線記錄檔的詳細資訊，請參閱下列主題：  
  
-   [SqlErrorLogEvent Class](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md) (此主題會示範如何擷取指定之記錄檔中已記錄事件的值)。  
  
-   [SqlErrorLogFile Class](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md) (此主題會示範如何擷取有關指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔的資訊)。  
  
##  <a name="BeforeYouBegin"></a> 權限  
 若要連接至離線記錄檔，您必須在本機和遠端電腦上具有下列權限：  
  
-   **Root\Microsoft\SqlServer\ComputerManagement12** WMI 命名空間的讀取權限。 根據預設，每個人都可從啟用帳戶權限取得讀取權限。 如需詳細資訊，請參閱本節後面的＜若要確認 WMI 權限＞程序。  
  
-   包含錯誤記錄檔之資料夾的讀取權限。 根據預設，錯誤記錄檔會位於下列路徑 (其中 \<磁碟機>  表示已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的磁碟機，\<執行個體名稱  > 則是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體名稱)：  
  
     **\<磁碟機>:\Program Files\Microsoft SQL Server\MSSQL13.\<執行個體名稱>\MSSQL\Log**  
  
 若要確認 WMI 命名空間安全性設定，您可以使用 [WMI 控制] 嵌入式管理單元。  
  
#### <a name="to-verify-wmi-permissions"></a>若要確認 WMI 權限  
  
1.  開啟 [WMI 控制] 嵌入式管理單元。 若要這樣做，請根據作業系統執行下列其中一項作業：  
  
    -   按一下 [開始]  ，在 [開始搜尋]  方塊中輸入 **wmimgmt.msc** ，然後按 ENTER 鍵。  
  
    -   依序按一下 [開始]  和 [執行]  ，輸入 **wmimgmt.msc**，然後按 ENTER 鍵。  
  
2.  根據預設，[WMI 控制] 嵌入式管理單元會管理本機電腦。  
  
     如果您想要連接至遠端電腦，請遵循下列步驟：  
  
    1.  以滑鼠右鍵按一下 [WMI 控制 (本機)]  ，然後按一下 [連線到另一台電腦]  。  
  
    2.  在 [變更受管理的電腦]  對話方塊中，按一下 [另一台電腦]  。  
  
    3.  輸入遠端電腦名稱，然後按一下 [確定]  。  
  
3.  以滑鼠右鍵按一下 [WMI 控制 (本機)]  或 **[WMI 控制 (** _遠端電腦名稱_ **)]** ，然後按一下 [內容]  。  
  
4.  在 [WMI Control Properties (WMI 控制內容)]  對話方塊中，按一下 [安全性]  索引標籤。  
  
5.  在命名空間樹狀目錄中，找出下列命名空間，然後按一下：  
  
     **Root\Microsoft\SqlServer\ComputerManagement10**  
  
6.  按一下 **[安全性]** 。  
  
7.  確定將要使用的帳戶擁有 [啟用帳戶]  權限。 此權限允許對 WMI 物件進行讀取存取。  

### <a name="view-log-files"></a>檢視記錄檔  
 下列程序會示範如何透過 [已註冊的伺服器] 檢視離線記錄檔。 此程序會假設下列條件：  
  
 您想要連接的目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體已經在 [已註冊的伺服器] 中註冊。  
  
##### <a name="to-view-log-files-for-instances-that-are-offline"></a>若要檢視已離線之執行個體的記錄檔  
  
1.  如果您想要檢視本機執行個體的離線記錄檔，請確定您使用更高的權限來啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。 若要這樣做，請在啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]時，以滑鼠右鍵按一下 [SQL Server Management Studio]  ，然後按一下 [以系統管理員身分執行]  。  
  
2.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 **[檢視]** 功能表中，按一下 **[已註冊的伺服器]** 。  
  
3.  在主控台樹狀目錄中，找出您想要檢視離線檔案的執行個體。  
  
4.  執行下列其中之一：  
  
    -   如果此執行個體位於 [本機伺服器群組]  底下，請依序展開 [本機伺服器群組]  和伺服器群組 (如果此執行個體是群組成員)，以滑鼠右鍵按一下執行個體，然後按一下 [檢視 SQL Server 記錄檔]  。  
  
    -   如果此執行個體是中央管理伺服器本身，請展開 [中央管理伺服器]  ，以滑鼠右鍵按一下執行個體，指向 [中央管理伺服器動作]  ，然後按一下 [檢視 SQL Server 記錄檔]  。  
  
    -   如果此執行個體位於 [中央管理伺服器]  底下，請依序展開 [中央管理伺服器]  和中央管理伺服器，以滑鼠右鍵按一下執行個體 (或展開伺服器群組並以滑鼠右鍵按一下執行個體)，然後按一下 [檢視 SQL Server 記錄檔]  。  
  
5.  如果您要連接至本機執行個體，就會使用目前使用者認證來建立連接。  
  
     如果您要連接至遠端執行個體，請在 [記錄檔檢視器 - 連接身分]  對話方塊中，執行下列其中一項作業：  
  
    -   若要以目前使用者的身分連接，請確定已清除 [以其他使用者身分連接]  核取方塊，然後按一下 [確定]  。  
  
    -   若要以其他使用者的身分連接，請選取 [以其他使用者身分連接]  核取方塊，然後按一下 [設定使用者]  。 當您收到提示時，請輸入使用者認證 (採用 *網域名稱*\\*使用者名稱*格式的使用者名稱)，按一下 [確定]  ，然後再按一下 [確定]  連接。  
  
    > [!NOTE]  
    >  如果載入記錄檔所花費的時間太長，您可以在 [記錄檔檢視器] 工具列上按一下 [停止]  。  
  
## <a name="see-also"></a>另請參閱  
 [記錄檔檢視器](../../relational-databases/logs/log-file-viewer.md)  
  
  
