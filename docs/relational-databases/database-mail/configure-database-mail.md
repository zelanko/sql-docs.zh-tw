---
title: 設定 Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlimail.profileandaccountmanagement.f1
- sql13.swb.sqlimail.newaccount.f1
- sql13.swb.dbmail. manageprofilesecurity.profileview.f1
- sql13.swb.sqlimail.manageexistingprofile.f1
- sql13.swb.sqlimail.addaccounttoprofile.f1
- sql13.swb.dbmail.manageexistingaccount.f1
- sql13.swb.sqlimail.manageprofilesecurity.profileview.f1
- sql13.swb.sqlimail.welcome.f1
- sql13.swb.sqlimail.manageprofilesecurity.principalview.f1
- sql13.swb.sqlimail.newsqlimailaccount.f1
- sql13.swb.sqlimail.selectconfiguration.f1
- sql13.swb.dbmail.completewizard.f1
- sql13.swb.dbmail.sendtestemail.test.f1
- sql13.swb.sqlimail.newprofile.f1
- sql13.swb.dbmail.addaccounttoprofile.f1
- sql13.swb.dbmail.newprofile.f1
- sql13.swb.sqlimail.manageexistingaccount.f1
- sql13.swb.dbmail.welcome.f1
- sql13.swb.dbmail.newaccount.f1
- sql13.swb.dbmail.profileandaccountmanagement.f1
- sql13.swb.dbmail.selectconfiguration.f1
- sql13.swb.dbmail.sendtestemail.f1
- sql13.swb.sqlimail.completewizard.f1
- sql13.swb.dbmail.configuresystem.f1
- sql13.swb.sqlimail.configuresystem.f1
- sql13.swb.dbmail.newsqlimailaccount.f1
- sql13.swb.dbmail.manageexistingprofile.f1
- sql13.swb.dbmail.manageprofilesecurity.principalview.f1
ms.assetid: 7edc21d4-ccf3-42a9-84c0-3f70333efce6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7f57825d1c4458761724c2e02c243a32a89dc018
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134581"
---
# <a name="configure-database-mail"></a>設定 Database Mail
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題說明如何使用 Database Mail 組態精靈來啟用及設定 Database Mail，並使用範本建立 Database Mail 組態指令碼。  
  
-   **開始之前：** [限制事項](#Restrictions)、[安全性](#Security)  
  
-   **使用以下方式設定 Database Mail：** [Database Mail 組態精靈](#DBWizard)、[使用範本](#Template)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 使用 [DatabaseMail XP]  選項，可在此伺服器上啟用 Database Mail。 如需詳細資訊，請參閱 [Database Mail XPs 伺服器組態選項](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) 參考主題。  
  
###  <a name="Restrictions"></a> 限制事項  
 在任何資料庫中啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker 都需要資料庫鎖定。 如果已在 **msdb**中停用 Service Broker，則啟用 Database Mail 的第一步是停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，好讓 Service Broker 可以取得必要的鎖定。  
  
###  <a name="Security"></a> 安全性  
 若要設定 Database Mail，您必須是 **系統管理員** 固定伺服器角色的成員。 若要傳送 Database Mail，您必須是 **msdb** 資料庫之 **DatabaseMailUserRole** 資料庫角色的成員。  
  
##  <a name="DBWizard"></a> 使用 Database Mail 組態精靈  
 **若要使用精靈設定 Database Mail**  
  
1.  在物件總管中，展開您想要設定 Database Mail 之執行個體的節點。  
  
2.  展開 **[管理]** 節點。  
  
3.  以滑鼠右鍵按一下 [Database Mail]  ，然後按一下 [設定 Database Mail]  。  
  
4.  完成精靈對話方塊  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    -   [歡迎頁面](#Welcome)  
  
    -   [選取組態工作頁面](#ConfigTask)  
  
    -   [新增帳戶頁面](#NewAccount)  
  
    -   [管理現有的帳戶頁面](#ExistingAccount)  
  
    -   [新增設定檔頁面](#NewProfile)  
  
    -   [管理現有的設定檔頁面](#ExistingProfile)  
  
    -   [將帳戶加入至設定檔頁面](#AddAccount)  
  
    -   [管理帳戶和設定檔頁面](#AccountsProfiles)  
  
    -   [管理設定檔安全性、公用索引標籤](#ProfileSecurityPublic)  
  
    -   [管理設定檔安全性、私用索引標籤](#ProfileSecurityPrivate)  
  
    -   [設定系統參數頁面](#SystemParameters)  
  
    -   [完成精靈頁面](#CompleteWizard)  
  
    -   [傳送測試電子郵件頁面](#TestEmail)  
  
###  <a name="Welcome"></a> 歡迎頁面  
 此頁說明設定 Database Mail 的步驟。  
  
 **不要再顯示此頁面** - 若將來要略過此歡迎頁面，請核取此選項。  
  
 **下一步** - 繼續 [選取組態工作]  頁面。  
  
 **取消** - 終止精靈，而不設定 Database Mail  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="ConfigTask"></a> 選取組態工作  
 使用 [選取組態工作]  頁面可指出您每次使用精靈時，會完成哪個工作。 如果您在完成精靈之前變更了主意，請使用 [上一步]  按鈕回到此頁面，然後選取不同的工作。  
  
> [!NOTE]  
>  如果尚未啟用 Database Mail，您就會收到下列訊息：**無法使用 Database Mail 功能。您要啟用此功能嗎?** 回應 [是]  就相當於使用 **sp_configure** 系統預存程序的 [Database Mail XP 選項](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)來啟用 Database Mail。  
  
 **執行下列工作來設定 Database Mail**  
 執行第一次設定 Database Mail 所需的所有工作。 此選項包含所有其他三個選項。  
  
 **管理 Database Mail 帳戶和設定檔**  
 建立新的 Database Mail 帳戶和設定檔，或是檢視、變更或刪除現有的 Database Mail 帳戶和設定檔。  
  
 **管理設定檔安全性**  
 設定哪些使用者才能夠存取 Database Mail 設定檔。  
  
 **檢視或變更系統參數**  
 設定 Database Mail 系統參數，例如附件的檔案大小上限。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="NewAccount"></a> 新增帳戶頁面  
 使用這個頁面建立新的 Database Mail 帳戶。 Database Mail 帳戶包含傳送電子郵件到 SMTP 伺服器的資訊。  
  
 Database Mail 帳戶包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來傳送電子郵件訊息到 SMTP 伺服器的資訊。 每個帳戶包含一個電子郵件伺服器的資訊。  
  
 Database Mail 帳戶僅供 Database Mail 使用。 Database Mail 帳戶不會對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶或 Microsoft Windows 帳戶。 Database Mail 可以使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的認證、使用您提供的其他認證或以匿名方式傳送。 使用基本驗證時，Database Mail 帳戶中的名稱和密碼僅用於電子郵件伺服器的驗證。 帳戶不需要對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者，或在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之電腦上的使用者。  
  
 **帳戶名稱**  
 輸入新帳戶的名稱。  
  
 **說明**  
 輸入帳戶的描述。 描述是選擇性的。  
  
 **電子郵件地址**  
 鍵入帳戶電子郵件地址的名稱。 這是電子郵件傳送來自的電子郵件地址。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的帳戶可能會從 SqlAgent@Adventure-Works.com。  
  
 **顯示名稱**  
 鍵入顯示於由這個帳戶傳送之電子郵件訊息上的名稱。 顯示名稱是選擇性的。 這是顯示於由這個帳戶傳送之訊息上的名稱。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的帳戶在電子郵件訊息上顯示的名稱可能會是「SQL Server Agent Automated Mailer」。  
  
 **回覆電子郵件**  
 鍵入將用來回覆給由這個帳戶傳送之電子郵件訊息的電子郵件地址。 回覆電子郵件是選擇性的。 例如，回覆給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 帳戶的郵件，可能會傳送給資料庫管理員 danw@Adventure-Works.com。  
  
 **伺服器名稱**  
 輸入帳戶用來傳送電子郵件的 SMTP 伺服器名稱或 IP 位址。 一般而言，此格式類似於 **smtp.<貴公司>**  **.com**。 如需相關說明，請洽詢您的郵件管理員。  
  
 **通訊埠編號**  
 輸入此帳戶之 SMTP 伺服器的通訊埠編號。 多數的 SMTP 伺服器使用通訊埠 25。  
  
 **這個伺服器需要安全連接 (SSL)**  
 使用安全通訊端層 (SSL) 將通訊加密。  
  
 **使用 Database Engine 服務認證的 Windows 驗證**  
 使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務設定的認證，來建立 SMTP 伺服器的連接。  
  
 **基本驗證**  
 指定 SMTP 伺服器所需的使用者名稱和密碼。  
  
 **使用者名稱**  
 鍵入 Database Mail 用來登入 SMTP 伺服器的使用者名稱。 如果 SMTP 伺服器需要基本驗證，則使用者名稱是必要的。  
  
 **密碼**  
 鍵入 Database Mail 用來登入 SMTP 伺服器的密碼。 如果 SMTP 伺服器需要基本驗證，則密碼是必要的。  
  
 **確認密碼**  
 再次輸入密碼，以便確認密碼。 如果 SMTP 伺服器需要基本驗證，則密碼是必要的。  
  
 **匿名驗證**  
 郵件傳送到 SMTP 伺服器時，不使用登入認證。 當 SMTP 伺服器不需要驗證時，請使用此選項。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="ExistingAccount"></a> 管理現有的帳戶頁面  
 使用此頁面來管理現有的 Database Mail 帳戶。  
  
 **帳戶名稱**  
 選取要檢視、更新或刪除的帳戶。  
  
 **刪除**  
 刪除選取的帳戶。 您必須從相關聯的設定檔移除這個帳戶，或先刪除相關聯的設定檔，再刪除選取的帳戶。  
  
 **說明**  
 檢視或更新帳戶的描述。 描述是選擇性的。  
  
 **電子郵件地址**  
 檢視或更新帳戶之電子郵件地址的名稱。 這是電子郵件傳送來自的電子郵件地址。 例如，Microsoft SQL Server Agent 的帳戶可能會從 **SqlAgent@Adventure-Works.com** 之電腦上的使用者。  
  
 **顯示名稱**  
 檢視或更新名稱，以顯示在由這個帳戶傳送的電子郵件訊息上。 顯示名稱是選擇性的。 這是顯示於由這個帳戶傳送之訊息上的名稱。 例如，SQL Server Agent 的帳戶在電子郵件訊息上顯示的名稱可能會是 **SQL Server Agent Automated Mailer** 。  
  
 **回覆電子郵件**  
 檢視或更新電子郵件地址，這將用於回覆給由這個帳戶傳送的電子郵件訊息。 回覆電子郵件是選擇性的。 例如，回覆給 SQL Server Agent 帳戶的郵件，可能會傳送給資料庫管理員 **danw@Adventure-Works.com** 之電腦上的使用者。  
  
 **伺服器名稱**  
 檢視或更新帳戶用來傳送電子郵件的 SMTP 伺服器名稱。 一般而言，此格式類似於 **smtp.<貴公司>.com**。 如需相關說明，請洽詢您的郵件管理員。  
  
 **通訊埠編號**  
 檢視或更新此帳戶的 SMTP 伺服器的通訊埠編號。 多數的 SMTP 伺服器使用通訊埠 25。  
  
 **這個伺服器需要安全連接 (SSL)**  
 使用安全通訊端層 (SSL) 將通訊加密。  
  
 **使用 Database Engine 服務認證的 Windows 驗證**  
 使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務設定的認證，來建立 SMTP 伺服器的連接。  
  
 **基本驗證**  
 指定 SMTP 伺服器所需的使用者名稱和密碼。  
  
 **User name**  
 檢視或更新 Database Mail 用來登入 SMTP 伺服器的使用者名稱。 如果 SMTP 伺服器需要基本驗證，則使用者名稱是必要的。  
  
 **密碼**  
 變更 Database Mail 用來登入 SMTP 伺服器的密碼。 如果 SMTP 伺服器需要基本驗證，則密碼是必要的。  
  
 **確認密碼**  
 再次輸入密碼，以便確認密碼。 如果 SMTP 伺服器需要基本驗證，則密碼是必要的。  
  
 **匿名驗證**  
 郵件傳送到 SMTP 伺服器時，不使用登入認證。 當 SMTP 伺服器不需要驗證時，請使用此選項。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="NewProfile"></a> 新增設定檔頁面  
 使用此頁面可建立 Database Mail 設定檔。 Database Mail 設定檔是 Database Mail 帳戶的集合。 設定檔會在電子郵件伺服器無法連接時，提供替代的 Database Mail 帳戶，加強可靠性。 至少需要一個 Database Mail 帳戶。 如需在設定檔中設定 Database Mail 帳戶之優先權的詳細資訊，請參閱[建立 Database Mail 設定檔](../../relational-databases/database-mail/create-a-database-mail-profile.md)。  
  
 使用 [上移]  和 [下移]  按鈕，即可變更使用 Database Mail 帳戶的順序。 此順序是由一個值 (稱為序號) 決定。 [上移]  會減少序號，而 [下移]  會增加序號。 序號決定了 Database Mail 使用設定檔中之帳戶的順序。 如果是新的電子郵件訊息，Database Mail 會從序號最低的帳戶開始。 如果這個帳戶失敗，Database Mail 會使用序號次高的帳戶，依此類推，直到 Database Mail 傳送訊息成功為止，或直到序號最高的帳戶失敗為止。 如果序號最高的帳戶失敗，Database Mail 會暫停嘗試傳送郵件一段時間，這段時間是在 Database Mail **AccountRetryDelay** 參數中設定，然後從最低序號開始，再次開始嘗試傳送郵件。 使用 Database Mail **AccountRetryAttempts** 參數，即可設定外部郵件處理序使用指定之設定檔內的每個帳戶，嘗試傳送電子郵件訊息的次數。 您可以在 Database Mail 組態精靈的 [設定系統參數]  頁面上，設定 **AccountRetryDelay** 和 **AccountRetryAttempts** 參數。  
  
 **設定檔名稱**  
 輸入新設定檔的名稱。 系統會使用此名稱來建立設定檔。 請勿使用現有設定檔的名稱。  
  
 **說明**  
 鍵入設定檔的描述。 描述是選擇性的。  
  
 **SMTP 帳戶**  
 為設定檔選擇一或多個帳戶。 優先權會設定 Database Mail 使用這些帳戶的順序。 如果沒有列出任何帳戶，您必須按一下 [加入]  才能繼續，然後加入新的 SMTP 帳戶。  
  
 **[加入]**  
 將帳戶加入至設定檔。  
  
 **移除**  
 從設定檔移除選取的帳戶。  
  
 **上移**  
 增加選取之帳戶的優先權。  
  
 **下移**  
 減少選取之帳戶的優先權。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="ExistingProfile"></a> 管理現有的設定檔頁面  
 使用此頁面可管理現有的 Database Mail 設定檔。 Database Mail 設定檔是 Database Mail 帳戶的集合。 設定檔會在電子郵件伺服器無法連接時，提供替代的 Database Mail 帳戶，加強可靠性。 至少需要一個 Database Mail 帳戶。 如需在設定檔中設定 Database Mail 帳戶之優先權的詳細資訊，請參閱[建立 Database Mail 設定檔](../../relational-databases/database-mail/create-a-database-mail-profile.md)。  
  
 使用 [上移]  和 [下移]  按鈕，即可變更使用 Database Mail 帳戶的順序。 此順序是由一個值 (稱為序號) 決定。 [上移]  會減少序號，而 [下移]  會增加序號。 序號決定了 Database Mail 使用設定檔中之帳戶的順序。 如果是新的電子郵件訊息，Database Mail 會從序號最低的帳戶開始。 如果這個帳戶失敗，Database Mail 會使用序號次高的帳戶，依此類推，直到 Database Mail 傳送訊息成功為止，或直到序號最高的帳戶失敗為止。 如果序號最高的帳戶失敗，Database Mail 會暫停嘗試傳送郵件一段時間，這段時間是在 Database Mail **AccountRetryDelay** 參數中設定，然後從最低序號開始，再次開始嘗試傳送郵件。 使用 Database Mail **AccountRetryAttempts** 參數，即可設定外部郵件處理序使用指定之設定檔內的每個帳戶，嘗試傳送電子郵件訊息的次數。 您可以在 Database Mail 組態精靈的 [設定系統參數]  頁面上，設定 **AccountRetryDelay** 和 **AccountRetryAttempts** 參數。  
  
 **設定檔名稱**  
 選取要管理之設定檔的名稱。  
  
 **刪除**  
 刪除選取的設定檔。 系統會提示您選取 [是]  來刪除選取的設定檔，並將任何未送出的郵件設為失敗，或選取 [否]  ，只有在沒有未送出的郵件時才刪除選取的設定檔。  
  
 **說明**  
 檢視或變更選取之設定檔的描述。 描述是選擇性的。  
  
 **SMTP 帳戶**  
 為設定檔選擇一或多個帳戶。 容錯移轉優先權會設定在發生容錯移轉時，Database Mail 使用帳戶的順序。  
  
 **[加入]**  
 將帳戶加入至設定檔。  
  
 **移除**  
 從設定檔移除選取的帳戶。  
  
 **上移**  
 增加選取之帳戶的容錯移轉優先權。  
  
 **下移**  
 減少選取之帳戶的容錯移轉優先權。  
  
 **優先權**  
 檢視帳戶的目前容錯移轉優先權。  
  
 **帳戶名稱**  
 檢視帳戶的名稱。  
  
 **E-mail Address**  
 檢視帳戶的電子郵件地址。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="AddAccount"></a> Add Account to Profile Page  
 使用此頁面可選擇要加入至設定檔的帳戶。 從 [帳戶名稱]  方塊中選擇現有的帳戶，或是按一下 [新增帳戶]   
  
 **帳戶名稱**  
 選取要加入至設定檔之帳戶的名稱。  
  
 **電子郵件地址**  
 檢視選取之帳戶的電子郵件地址。 您無法從此頁面中變更電子郵件地址。 若要變更帳戶的電子郵件地址，請回到精靈的主要頁面，然後選取 [管理 Database Mail 帳戶和設定檔]  選項。  
  
 **伺服器名稱**  
 檢視選取之帳戶的郵件伺服器名稱。 您無法從此頁面中變更伺服器名稱。 若要變更帳戶的伺服器名稱，請回到精靈的主要頁面，然後選取 [管理 Database Mail 帳戶和設定檔]  選項。  
  
 **新增帳戶**  
 建立新帳戶。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="AccountsProfiles"></a> 管理帳戶和設定檔頁面  
 使用此頁面可選擇用來管理設定檔或帳戶的工作。  
  
 **建立新帳戶**  
 建立新帳戶。  
  
 **檢視、變更或刪除現有的帳戶**  
 管理或刪除現有的帳戶。  
  
 **建立新設定檔**  
 建立新的設定檔。  
  
 **檢視、變更或刪除現有的設定檔。您也可以管理與設定檔相關聯的帳戶。**  
 更新或刪除現有的設定檔。 此選項也可讓您管理與設定檔相關聯的帳戶。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="ProfileSecurityPublic"></a> 管理設定檔安全性、公用索引標籤  
 使用此頁面來設定公用設定檔。  
  
 設定檔是公用或私人的。 私人設定檔只有特定使用者或角色能夠存取。 公用設定檔允許擁有郵件主機資料庫 (**msdb**) 存取權的任何使用者或角色，使用該設定檔傳送電子郵件。  
  
 設定檔可能是預設設定檔。 在此情況下，使用者或角色不必明確指定設定檔，就能使用設定檔傳送電子郵件。 如果傳送電子郵件訊息的使用者或角色有預設的私人設定檔，Database Mail 就會使用該設定檔。 如果使用者或角色沒有預設的私人設定檔， **sp_send_dbmail** 會使用 **msdb** 資料庫的預設公用設定檔。 如果沒有使用者或角色的預設私人設定檔，而且沒有資料庫的預設公用設定檔， **sp_send_dbmail** 會傳回錯誤。 只有一個設定檔可以標示為預設的設定檔。  
  
 **公用**  
 選取此選項使指定的設定檔成為公用的。  
  
 **Profile Name**  
 顯示設定檔的名稱。  
  
 **預設設定檔**  
 選取此選項使指定的設定檔成為預設的設定檔。  
  
 **只顯示現有的公用設定檔**  
 選取此選項，以便只顯示指定之資料庫中公用的設定檔。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="ProfileSecurityPrivate"></a> 管理設定檔安全性、私用索引標籤  
 使用此頁面來設定私人設定檔。  
  
 設定檔是公用或私人的。 私人設定檔只有特定使用者或角色能夠存取。 公用設定檔允許擁有郵件主機資料庫 (**msdb**) 存取權的任何使用者或角色，使用該設定檔傳送電子郵件。  
  
 設定檔可能是預設設定檔。 在此情況下，使用者或角色不必明確指定設定檔，就能使用設定檔傳送電子郵件。 如果傳送電子郵件訊息的使用者或角色有預設的私人設定檔，Database Mail 就會使用該設定檔。 如果使用者或角色沒有預設的私人設定檔， **sp_send_dbmail** 會使用 **msdb** 資料庫的預設公用設定檔。 如果沒有使用者或角色的預設私人設定檔，而且沒有資料庫的預設公用設定檔， **sp_send_dbmail** 會傳回錯誤。  
  
 **User name**  
 選取 **msdb** 資料庫中使用者或角色的名稱。  
  
 **存取**  
 選取使用者或角色是否能夠存取指定的設定檔。  
  
 **設定檔名稱**  
 檢視設定檔的名稱。  
  
 **是預設的設定檔**  
 選取設定檔是否是使用者或角色的預設設定檔。 每個使用者或角色只可以有一個預設的設定檔。  
  
 **只顯示此使用者的現有私人設定檔**  
 選取此選項，只顯示指定之使用者或角色已經擁有存取權的設定檔。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="SystemParameters"></a> 設定系統參數  
 使用此頁面來指定 Database Mail 系統參數。 檢視系統參數以及每個參數目前的值。 選取參數，以便在資訊窗格中檢視簡短的描述。  
  
 **帳戶重試嘗試**  
 外部郵件處理序嘗試利用指定設定檔中的每個帳戶來傳送電子郵件訊息的次數。  
  
 **帳戶重試延遲 (秒)**  
 外部郵件處理序在使用設定檔中的所有帳戶，來嘗試傳遞訊息之後，其在再次嘗試使用所有帳戶之前，所需等候的時間 (以秒為單位)。  
  
 **檔案大小上限 (位元組)**  
 附件的大小上限 (以位元組為單位)。  
  
 **禁止的附加檔案副檔名**  
 無法作為電子郵件訊息附件來傳送的副檔名清單 (以逗號分隔)。 按一下瀏覽按鈕 ([...]  )，加入其他副檔名。  
  
 **Database Mail 可執行檔最小存留期間 (秒)**  
 外部郵件處理序維持使用中的最短時間 (以秒為單位)。 只要在 Database Mail 佇列中有電子郵件，此處理序就會保持在使用中。 此參數指定當沒有要處理的訊息時，處理序保持在使用中的時間。  
  
 **記錄層級**  
 指定哪些訊息要記錄在 Database Mail 記錄中。 可能的值為：  
  
-   一般 - 只記錄錯誤  
  
-   擴充 - 記錄錯誤、警告以及資訊性訊息  
  
-   詳細資訊 - 記錄錯誤、警告、資訊性訊息、成功訊息以及其他內部訊息。 使用詳細資訊記錄來進行疑難排解。  
  
 預設值是擴充。  
  
 **全部重設**  
 選取此選項，將頁面上的值都重設為預設值。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="CompleteWizard"></a> 完成精靈頁面  
 使用此頁面來檢閱 [Database Mail 組態精靈]  將要執行的動作。 在精靈結束之前將不會做任何變更。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
###  <a name="TestEmail"></a> Send Test E-Mail Page  
 使用 [從 <執行個體名稱>  傳送測試電子郵件]  頁面，以使用指定的 Database Mail 設定檔傳送電子郵件訊息。 只有 **系統管理員** 固定伺服器角色的成員，才可以使用此頁面來傳送測試電子郵件。  
  
 **Database Mail 設定檔**  
 從清單中選取 Database Mail 設定檔。 這是必要的欄位。 如果未顯示任何設定檔，就表示沒有設定檔，或者您沒有設定檔的存取權限。 使用 **[Database Mail 組態精靈]** 來建立及設定設定檔。 如果未列出任何設定檔，請使用 Database Mail 組態精靈來建立供您使用的設定檔。  
  
 **若要**  
 訊息收件者的電子郵件地址。 至少需要一位收件者。  
  
 **主旨**  
 測試電子郵件的主旨列。 變更預設主旨，以便更適當地識別您的電子郵件進行疑難排解。  
  
 **本文**  
 測試電子郵件的本文。 變更預設主旨，以便更適當地識別您的電子郵件進行疑難排解。  
  
 [Database Mail 測試電子郵件]  對話方塊會確認 Database Mail 已嘗試傳送測試訊息，並提供測試電子郵件訊息的 **mailitem_id**。 與收件者聯繫來判斷電子郵件是否送達。 電子郵件一般都會在數分鐘內收到，但是電子郵件可能因為緩慢的網路效能、在郵件伺服器上積存訊息，或伺服器暫時不能使用等原因而延遲。 使用 **mailitem_id** 來進行疑難排解。  
  
 **傳送電子郵件**  
 測試電子郵件訊息的 **mailitem_id** 。  
  
 **疑難排解**  
 按一下以開啟《線上叢書》的 [Database Mail 疑難排解](https://msdn.microsoft.com/library/ms188663.aspx)主題。  
  
 [Database Mail 組態精靈](#DBWizard)  
  
##  <a name="Template"></a> 使用範本  
 **若要建立 Database Mail 組態指令碼**  
  
1.  在 [檢視]  功能表中，選取 [範本總管]  。  
  
2.  在 [範本總管]  視窗中，展開 [Database Mail]  資料夾。  
  
3.  按兩下 [Simple Database Mail 組態]  。 就會在新查詢視窗中開啟範本。  
  
4.  在 [查詢]  功能表上，選取 [指定範本參數的值]  。 即會開啟 [取代範本參數]  視窗。  
  
5.  輸入 **profile_name**、**account_name**、**SMTP_servername**、**email_address** 和 **display_name** 的值。 SQL Server Management Studio 就會將您提供的值填入範本中。  
  
6.  執行指令碼以建立組態。  
  
7.  此指令碼不會將資料庫使用者存取權授與給設定檔。 因此，依預設只有**系統管理員**固定安全性角色的成員才能使用此設定檔。 如需授與設定檔存取權限的詳細資訊，請參閱 [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql.md)。  
  
  
