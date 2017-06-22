---
title: "設定報表伺服器進行遠端管理 |Microsoft 文件"
ms.date: 09/14/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reporting Services Configuration tool
- WMI provider [Reporting Services], remote configuration
- configuration management [WMI]
- report servers [Reporting Services], configuring
- remote server administration [Reporting Services]
ms.assetid: 8c7f145f-3ac2-4203-8cd6-2a4694395d09
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 69e4b50bdfd9dcffd285dbd7a37e095efdca621c
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="configure-a-report-server-for-remote-administration"></a>設定報表伺服器來進行遠端管理
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，您可以在本機或遠端設定報表伺服器執行個體。 若要設定遠端報表伺服器執行個體，您可以使用 Reporting Services 組態工具，或是撰寫使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows Management Instrumentation (WMI) 提供者的自訂程式碼。 Reporting Services 組態工具提供了 WMI 提供者的圖形介面，好讓您不需要撰寫程式碼就可以設定報表伺服器。 當您啟動這個工具時，可以指定要連接的遠端伺服器。  
  
 在您可以使用此工具來設定遠端報表伺服器以前，您必須遵循本主題的指示，在 Windows 防火牆中啟用通訊埠、啟用遠端連接，以及啟用 WMI 要求。  
  
 適當的組態設定可協助您避免下列錯誤：  
  
 `The machine could not be found.`  
  
 `"The RPC server is unavailable. (Exception from HRESULT: 0x800706BA)".`  
  
## <a name="prerequisites"></a>必要條件  
 若要修改防火牆設定，您必須在本機登入，而且必須是本機管理員群組的成員； 您不能透過遠端連接修改遠端電腦的 Windows 防火牆設定。  
  
 如果您想要針對非管理員的使用者啟用遠端管理，必須將遠端啟動權限授與給「分散式元件物件模型」(DCOM) 帳戶。 本主題有提供針對非管理員存取權設定伺服器的指示。  
  
 某些組織有一些群組原則，可防止某些作業系統或使用者管理遠端伺服器。 在您開始修改防火牆設定之前，請先洽詢網路管理員，以確認遠端管理是否有任何限制。  
  
 如需詳細資訊，請參閱 MSDN 上 Platform SDK 文件集內的 [通過 Windows 防火牆進行連接](http://go.microsoft.com/fwlink/?LinkId=63615) 。  
  
## <a name="tasks"></a>工作  
 啟用遠端報表伺服器組態的工作包括以下項目：  
  
-   在 Windows 防火牆中啟用通訊埠，以允許報表伺服器和 SQL Server Database Engine 執行個體所使用的通訊埠要求。  請參閱＜ [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) ＞和＜ [Configure a Windows Firewall for Database Engine Access](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)＞。  
  
-   啟用與主控報表伺服器資料庫之 Database Engine 執行個體之間的遠端連接。 如果要設定報表伺服器資料庫連接及管理加密金鑰，必須要有遠端連接；  
  
-   啟用要通過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 防火牆傳遞的遠端 WMI 要求。  
  
-   如果您要設定遠端報表伺服器供非管理使用者進行管理，您必須設定 DCOM 權限，好讓遠端 WMI 可存取標準 Windows 使用者帳戶。 由於 WMI 會使用 DCOM 當做遠端呼叫的傳輸，所以您必須設定 DCOM 權限，好讓不是以本機管理員身分登入的使用者可以設定伺服器。  
  
-   如果您要設定遠端報表伺服器供非管理使用者進行管理，您也必須設定報表伺服器 WMI 命名空間的 WMI 權限。 依預設，本機管理員群組的所有成員都有權存取報表伺服器 WMI 命名空間； 如果您將存取權授與非管理員，則必須設定權限。  
  
 本主題將提供如何執行這些工作的相關指示。  
  
### <a name="to-configure-remote-connections-to-the-report-server-database"></a>設定與報表伺服器資料庫的遠端連接  
  
1.  按一下 **[開始]**，並依序指向 **[程式集]**、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，然後按一下 **[SQL Server 組態管理員]**。  
  
2.  在左窗格中，展開 **[SQL Server 網路組態]**，然後針對  的執行個體按一下 [通訊協定] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
3.  在詳細資料窗格中，啟用 TCP/IP 和具名管道通訊協定，然後重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
### <a name="to-enable-remote-administration-in-windows-firewall"></a>在 Windows 防火牆中啟用遠端管理  
  
1.  以本機管理員的身分登入您想要啟用遠端管理的電腦。  
  
2.  以系統管理權限開啟命令提示字元。  
  
3.  執行下列命令：  
  
    ```  
    netsh.exe firewall set service type=REMOTEADMIN mode=ENABLE scope=ALL  
    ```  
  
     您可以對 Scope 指定不同的選項。 如需詳細資訊，請參閱 Windows Firewall 產品文件集。  
  
4.  確認是否啟用遠端管理； 您可以執行下列命令來顯示狀態：  
  
    ```  
    netsh.exe firewall show state  
    ```  
  
5.  重新啟動電腦。  
  
### <a name="to-set-dcom-permissions-to-enable-remote-wmi-access-for-non-administrators"></a>設定 DCOM 權限來對非管理員啟用遠端 WMI 存取  
  
1.  在 [開始] 功能表上，指向 **[系統管理工具]**，然後按一下 **[元件服務]**。  
  
     如果是 Windows Vista，請在 [開始] 功能表上按一下 **[所有程式]**，再按一下 **[執行]**，然後輸入 **mmc comexp.msc**。  
  
2.  開啟 [元件服務] 資料夾。  
  
3.  開啟 [電腦] 資料夾。  
  
4.  選取 [我的電腦]。  
  
5.  選取 **[執行]** 功能表上的 **[內容]**。  
  
6.  按一下 **[COM 安全設定]**。  
  
7.  在 **[啟動和啟用權限]**中，按一下 **[編輯限制]**。  
  
8.  如果您沒有在 **[啟動權限]**中看到您的名稱，請按一下 **[新增]**。  
  
9. 輸入您的使用者帳戶名稱，然後按一下 **[確定]**。  
  
10. 中**權限\<使用者或群組 >**，請在**允許**欄中，選取**遠端啟動**和**遠端啟用**，然後按一下 **確定**。  
  
### <a name="to-set-permissions-on-the-report-server-wmi-namespace-for-non-administrators"></a>針對非管理員設定報表伺服器 WMI 命名空間的權限  
  
1.  在 [開始] 功能表上，指向 **[系統管理工具]**，然後按一下 **[電腦管理]**。  
  
2.  開啟 [服務及應用程式] 資料夾。  
  
3.  以滑鼠右鍵按一下 [WMI 控制]，然後選取 [內容]。  
  
4.  按一下 **[安全性]**。  
  
5.  開啟 [Root] 資料夾。  
  
6.  開啟 [Microsoft] 資料夾。  
  
7.  開啟 [SQLServer] 資料夾。  
  
8.  開啟 [ReportServer] 資料夾。  
  
9. 開啟執行個體資料夾。 如果您已安裝預設執行個體，此資料夾就是 MSSQLSERVER。  
  
10. 開啟 [v10] 資料夾。  
  
11. 選取 [Admin] 資料夾，然後按一下 **[安全性]**。  
  
12. 按一下 **[新增]**，然後輸入將用來管理伺服器的使用者帳戶。  
  
13. 在 **[允許]** 一欄中，選取 **[啟用帳戶]**、 **[遠端啟用]**及 **[讀取安全性]**，然後按一下 **[確定]**。  
  
## <a name="see-also"></a>請參閱＜  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
  

