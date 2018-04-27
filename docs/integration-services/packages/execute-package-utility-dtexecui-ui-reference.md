---
title: 執行套件公用程式 (dtexecui) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: packages
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.dtexecui.setvalues.f1
- sql13.dts.dtexecui.reporting.f1
- sql13.dts.dtexecui.datasources.f1
- sql13.dts.dtexecui.commandfiles.f1
- sql13.dts.dtexecui.logging.f1
- sql13.dts.dtexecui.general.f1
- sql13.dts.dtexecui.verification.f1
- sql13.dts.dtexecui.executionoptions.f1
- sql13.dts.dtexecui.commandline.f1
- sql13.dts.dtexecui.configuration.f1
helpviewer_keywords:
- DTExecUI utility
ms.assetid: 3d71df39-126b-4c8e-bd77-128bbd5b0887
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dd6097e9c173196466870fea63a0c1334c7a37b5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="execute-package-utility-dtexecui"></a>執行套件公用程式 (dtexecui)
  您可使用 **[執行封裝公用程式]** 來執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 此公用程式會執行儲存在下列三個位置之一的封裝： [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區及檔案系統。 此使用者介面可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 開啟或藉由在命令提示字元輸入 **dtexecui** 加以開啟，作為使用 **DTExec** 命令提示字元工具執行封裝的替代方案。  
  
 封裝會在與 **dtexecui.exe** 公用程式相同的處理序中執行。 由於此公用程式是 32 位元工具，因此封裝會在 Windows on Win32 (WOW) 所執行的 64 位元環境中透過 **dtexecui.exe** 加以執行。 在 64 位元電腦上使用 dtexecui.exe 公用程式開發及測試命令時，應先使用 64 位元版本的 **dtexec.exe** 以 64 位元模式測試命令，然後才在實際伺服器上部署或為命令排程。  
  
 [執行封裝公用程式]  是 **DTExec** 命令提示字元工具的圖形化使用者介面。 該使用者介面可輕易設定選項，並在透過所指定的選項執行封裝時，自動組裝傳送給 **DTExec** 命令提示字元工具的命令列。  
  
 [執行封裝公用程式]  也可用來組裝您在直接執行 **DTExec** 時所使用的命令列。  
  
### <a name="to-open-execute-package-utility-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中開啟執行封裝公用程式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 **[檢視]** 功能表上，按一下 **[物件總管]**。  
  
2.  在 [物件總管] 中，按一下 **[連接]**，然後按一下 **[Integration Services]**。  
  
3.  在 **[連接到伺服器]** 對話方塊的 **[伺服器名稱]** 清單中，輸入伺服器名稱，然後按一下 **[連接]**。  
  
4.  展開 [存放的封裝] 資料夾和子資料夾，以滑鼠右鍵按一下要執行的封裝，然後按一下 [執行封裝]。  
  
### <a name="to-open-the-execute-package-utility-at-the-command-prompt"></a>在命令提示字元下開啟執行封裝公用程式  
  
-   在命令提示字元視窗中，執行 **dtexecui**。  
  
 下列各節將說明 **[執行封裝公用程式]** 對話方塊的各個頁面。  
  
## <a name="general-page"></a>一般頁面  
 使用 **[執行封裝公用程式]** 對話方塊的 **[一般]** 頁面，即可指定封裝名稱和位置。  
  
 即使封裝儲存在遠端伺服器上，執行封裝公用程式 (dtexecui.exe) 會永遠在本機電腦上執行封裝。 如果遠端封裝使用的組態檔也儲存在遠端伺服器上，則執行封裝公用程式可能會找不到組態而導致封裝失敗。 為了避免此問題，必須以通用命名慣例 (UNC) 共用名稱來參考組態，例如 \\\myserver\myfile。  
  
### <a name="static-options"></a>靜態選項  
 **封裝來源**  
 使用下列選項，指定要執行之封裝的位置：  
  
|||  
|-|-|  
|ReplTest1|描述|  
|**[SQL Server]**|當封裝位於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，請選取此選項。 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，並提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的使用者名稱和密碼。 每個使用者名稱和密碼都會將 **/USER** *username* 和 **/PASSWORD** *password* options to the comm和 prompt.|  
|**檔案系統**|當封裝位於檔案系統時，請選取此選項。|  
|**SSIS 封裝存放區**|當封裝位於 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區時，請選取此選項。|  
  
 每一個選取項目都具有下列選項集合。  
  
 **執行**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
### <a name="dynamic-options"></a>動態選項  
  
#### <a name="package-source--sql-server"></a>封裝來源 = SQL Server  
 **Server**  
 輸入封裝所在的伺服器名稱，或從清單中選取伺服器。  
  
 **登入伺服器**  
 指定封裝要使用 Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 建議使用 Windows 驗證，以獲得較佳的安全性。 使用 Windows 驗證，您就不需要指定使用者名稱和密碼。  
  
 **使用 Windows 驗證**  
 選取此選項即可使用 Windows 驗證，並以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者帳戶登入。  
  
 **[使用 SQL Server 驗證]**  
 選取此選項即可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 當使用者透過不信任連接並指定登入名稱和密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行驗證，檢查是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 找不到登入帳戶，驗證將會失敗，且使用者會收到錯誤訊息。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。  
  
 **封裝**  
 請輸入封裝的名稱，或按一下省略符號按鈕 **(…)**，使用 [選取 SSIS 封裝] 對話方塊來尋找封裝。  
  
#### <a name="package-source--file-system"></a>封裝來源 = 檔案系統  
 **封裝**  
 輸入封裝的名稱，或按一下省略符號按鈕 **(…)** ，使用 [開啟] 對話方塊來尋找封裝。 依預設，對話方塊只會列出副檔名為 .dtsx 的檔案。  
  
#### <a name="package-source--ssis-package-store"></a>封裝來源 = SSIS 封裝存放區  
 **Server**  
 輸入封裝所在的電腦名稱，或從清單中選取電腦。  
  
 **登入伺服器**  
 指定封裝是否應該使用 Microsoft Windows 驗證來連接封裝來源。 建議使用 Windows 驗證，以獲得較佳的安全性。 使用 Windows 驗證，您就不需要指定使用者名稱和密碼。  
  
 **[使用 Windows 驗證]**  
 選取此選項即可使用 Windows 驗證，並以 Microsoft Windows 使用者帳戶登入。  
  
 **[使用 SQL Server 驗證]**  
 當您執行儲存在 [SSIS 封裝存放區] 的封裝時，無法使用此選項。  
  
 **封裝**  
 請輸入封裝的名稱，或按一下省略符號按鈕 **(…)**，使用 [選取 SSIS 封裝] 對話方塊來尋找封裝。  
  
## <a name="configurations-page"></a>組態頁面  
 使用 **[執行封裝公用程式]** 對話方塊的 **[組態]** 頁面，即可選取要在執行階段載入的組態檔，並指定載入這些檔案的順序。  
  
### <a name="options"></a>選項。  
 **組態檔**  
 列出封裝使用的組態。 每個組態檔都會將 **/CONFIGFILE filename** 選項加入命令提示字元。  
  
 **方向鍵**  
 選取清單中的組態檔，並使用右邊的箭頭按鍵，即可變更載入的順序。 組態會從清單的頂端開始依序載入。  
  
> [!NOTE]  
>  如果有多個組態會修改同一項屬性，就會採用最後載入的組態。  
  
 **[加入]**  
 按一下即可使用 [開啟] 對話方塊來加入組態。 依預設，對話方塊只會列出具有 .dtsconfig 副檔名的檔案。  
  
 **移除**  
 選取清單中的組態檔，然後按一下 [移除]。  
  
 **執行**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
## <a name="command-files-page"></a>命令檔頁面  
 使用 **[執行封裝公用程式]** 對話方塊的 **[命令檔]** 頁面，即可選取在執行階段要載入的命令檔。  
  
### <a name="options"></a>選項。  
 **Command files**  
 列出封裝所使用的命令檔。 封裝可以使用多個檔案來設定命令列選項。  
  
 **方向鍵**  
 選取清單中的命令檔，並使用右邊的方向鍵來變更載入順序。 命令檔依序載入，從清單的最上方開始。  
  
 **[加入]**  
 按一下即可使用 [開啟] 對話方塊加入命令檔。  
  
 **移除**  
 選取文字方塊中的命令檔，然後使用 [移除] 按鈕將它移除。  
  
 **執行**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
## <a name="connection-managers-page"></a>連接管理員頁面  
 使用 **[執行封裝公用程式]** 對話方塊的 **[連接管理員]** 頁面，即可編輯封裝使用之連接管理員的連接字串。  
  
### <a name="options"></a>選項。  
 **連線管理員**  
 選取其核取方塊即可使 [連接字串] 資料行變成可編輯。  
  
 **說明**  
 檢視每個連接管理員的描述。 無法編輯描述。  
  
 **連接字串**  
 編輯連接管理員的連接字串。 只有選取 **[連接管理員]** 核取方塊時，才可以編輯此欄位。  
  
 **執行**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
## <a name="execution-options-page"></a>執行選項頁面  
 使用 [執行封裝公用程式] 對話方塊的 [執行選項] 頁面，即可為封裝指定執行階段的選項。  
  
### <a name="options"></a>選項。  
 **發生驗證警告時封裝就失敗**  
 指出在發生驗證警告時，封裝是否會失敗。  
  
 **驗證封裝但不執行**  
 指出是否只對封裝進行驗證。  
  
 **最大並行可執行檔數目**  
 指出您是否想要指定可以同時在封裝中執行的最大可執行檔數目。 當您選取此核取方塊之後，請使用微調方塊來指定最大可執行檔數目。  
  
 **啟用封裝檢查點**  
 表示是否要啟用封裝檢查點。  
  
 **檢查點檔案**  
 如果您啟用了封裝檢查點，就會列出封裝使用的檢查點檔案。  
  
 **瀏覽**  
 如果您啟用了封裝檢查點，則按一下瀏覽按鈕 **(…)**，再使用 [開啟] 對話方塊，來找出檢查點檔案。 如果已經指定了檢查點檔案，就會用選取的檔案來取代它。  
  
 **覆寫重新啟動選項**  
 如果您啟用了封裝檢查點，會指出是否要覆寫重新啟動選項。  
  
 **重新啟動選項**  
 如果您覆寫重新啟動選項，選取如何使用檢查點。  
  
 **Execute**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
## <a name="reporting-page"></a>報告頁面  
 使用 **[執行封裝公用程式]** 對話方塊的 **[報表]** 頁面，即可指定封裝執行時，記錄至主控台的事件與封裝的詳細資訊。  
  
### <a name="options"></a>選項。  
 **主控台事件**  
 指出要報告的事件和訊息類型。  
  
 **無**  
 選擇不報告。  
  
 **錯誤**  
 選擇要報告錯誤訊息。  
  
 **警告**  
 選擇要報告警告訊息。  
  
 **自訂事件**  
 選擇要報告自訂事件訊息。  
  
 **管線事件**  
 選擇要報告資料流程事件訊息。  
  
 **資訊**  
 選擇要報告資訊訊息。  
  
 **Verbose**  
 選擇要使用詳細資訊報表。  
  
 **主控台記錄**  
 指定選取的事件發生時，要寫入記錄的資訊。  
  
 **名稱**  
 選擇要報告建立封裝的人員名稱。  
  
 **電腦**  
 選擇要報告正在執行封裝的電腦名稱。  
  
 **運算子**  
 選擇要報告啟動封裝的人員名稱。  
  
 **來源名稱**  
 選擇要報告封裝名稱。  
  
 **來源 GUID**  
 選擇要報告封裝 GUID。  
  
 **執行 GUID**  
 選擇要報告封裝執行個體的 GUID。  
  
 **訊息**  
 選擇要報告訊息。  
  
 **開始時間和結束時間**  
 選擇要報告封裝開始和結束的時間。  
  
 **執行**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
## <a name="logging-page"></a>記錄頁面  
 使用 **[執行封裝公用程式]** 對話方塊的 **[記錄]** 頁面，即可讓封裝在執行階段使用記錄提供者。 提供連接到記錄的封裝記錄提供者類型和連接字串。 每個記錄提供者項目各會新增一個 **/LOGGER***classid* 選項到命令提示字元。  
  
### <a name="options"></a>選項。  
 **記錄提供者**  
 從清單中選取記錄提供者。  
  
 **組態字串**  
 從指向記錄位置的封裝選取連接管理員的名稱，或鍵入連接到記錄提供者的連接字串。  
  
 **移除**  
 選取記錄提供者，然後按一下即可將它移除。  
  
 **執行**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
## <a name="set-values-page"></a>設定值頁面  
 使用 **[執行封裝公用程式]** 對話方塊的 **[設定值]** 頁面，即可藉由輸入屬性的路徑和屬性值，來設定封裝、可執行檔、連接、變數和記錄提供者的屬性值。 每個路徑項目各會新增一個 **/SET***propertypath;value* 選項到命令提示字元。  
  
### <a name="options"></a>選項。  
 **屬性路徑**  
 輸入屬性的路徑。 路徑的語法會使用反斜線 (\\) 來指出下列項目是容器，使用句點 (.) 來指出下列項目是屬性，以及使用方括號來指出集合成員。 可以使用成員的索引或其名稱來識別成員。 例如，封裝變數的屬性路徑為 \Package.Variables[MyVariable].Value。  
  
 **ReplTest1**  
 鍵入屬性的值。  
  
 **移除**  
 選取屬性路徑，然後按一下即可將它移除。  
  
 **執行**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
## <a name="verification-page"></a>驗證頁面  
 使用 **[執行封裝]** 對話方塊的 **[驗證]** 頁面，即可設定驗證封裝的準則。  
  
### <a name="options"></a>選項。  
 **只執行簽署的封裝**  
 選取即可只執行已經簽署的封裝。  
  
 **確認封裝組建**  
 選取即可確認封裝組建。  
  
 建置  
 指定與組建相關聯的循序組建編號。  
  
 **確認封裝識別碼**  
 選取即可確認封裝識別碼。  
  
 封裝識別碼  
 指定封裝識別碼。  
  
 **確認版本識別碼**  
 選取即可確認版本識別碼。  
  
 版本識別碼  
 指定版本識別碼。  
  
 **執行**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
## <a name="command-line-page"></a>命令列頁面  
 使用 **[執行封裝公用程式]** 對話方塊的 **[命令列]** 節點，即可編輯已經由各對話建立之選項所產生的命令列。  
  
### <a name="options"></a>選項。  
 **還原原始選項**  
 按一下即可還原命令列至其原始狀態。 如果已經使用 [手動編輯命令列] 選項進行修改，並且要還原原始命令列選項，請使用此選項。  
  
 **手動編輯命令列**  
 按一下即可編輯 [命令列] 文字方塊中的命令列。  
  
 **命令列**  
 顯示目前的命令列。 如果您選取要以手動編輯命令列的選項，就可以編輯。  
  
 **執行**  
 按一下以執行封裝。  
  
 **關閉**  
 按一下即可關閉 [執行封裝公用程式] 對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)  
  
  
