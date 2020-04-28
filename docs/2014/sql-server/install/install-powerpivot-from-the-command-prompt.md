---
title: 從命令提示字元安裝 PowerPivot |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 7f1f2b28-c9f5-49ad-934b-02f2fa6b9328
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8959b1ca4ea719ce571cb8609b817bba965185bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798325"
---
# <a name="install-powerpivot-from-the-command-prompt"></a>從命令提示字元安裝 PowerPivot
  您可以從命令列執行安裝程式來安裝 SQL Server PowerPivot for SharePoint。 您可以在命令中包含 `/ROLE` 參數並排除 `/FEATURES` 參數。  
  
## <a name="prerequisites"></a>Prerequisites  
 您必須安裝 SharePoint Server 2010 Enterprise Edition Service Pack 1 (SP1)。  
  
 您必須使用網域帳戶佈建 Analysis Services。  
  
 電腦必須聯結至與 SharePoint 伺服器陣列相同的網域。  
  
##  <a name="role-based-installation-options"></a><a name="Commands"></a>以/ROLE 為基礎的安裝選項  
 在 PowerPivot for SharePoint 部署中，會使用 `/ROLE` 參數取代 `/FEATURES` 參數。 有效值包括：  
  
-   `SPI_AS_ExistingFarm`  
  
-   `SPI_AS_NewFarm`  
  
 兩個角色都會安裝應用程式、組態和部署檔案，好讓 PowerPivot for SharePoint 在 SharePoint 伺服器陣列中執行。 指定任一個角色將會使得安裝程式檢查 SharePoint 整合所需的硬體和軟體需求。  
  
 現有的伺服器陣列選項假設已具有 SharePoint 伺服器陣列。 [新增伺服器陣列] 選項會假設您將建立新的伺服器陣列;它支援在命令列語法中加入資料庫引擎實例，讓您可以使用資料庫引擎實例作為伺服器陣列的資料庫伺服器。  
  
 相對於舊版，所有伺服器組態工作會以後續安裝工作來執行。 如果您想自動化安裝和組態步驟，您可以使用 PowerShell 設定伺服器。 如需詳細資訊，請參閱[使用 Windows PowerShell 的 PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)設定。  
  
## <a name="example-commands"></a>範例命令  
 下列範例說明每個選項的用法。 範例1顯示`SPI_AS_ExistingFarm`。  
  
```cmd
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 範例 2 顯示 `SPI_AS_NewFarm`。 請注意，此範例包含佈建 Database Engine 的參數。  
  
```cmd
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_NewFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/SQLSVCACCOUNT=<DomainName\UserName> /SQLSVCPASSWORD=<StrongPassword> /SQLSYSADMINACCOUNTS=<DomainName\UserName> /AGTSVCACCOUNT=<DomainName\UserName> /AGTSVCPASSWORD=<StrongPassword> /ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
##  <a name="modifying-the-command-syntax"></a><a name="Join"></a>修改命令語法  
 使用下列步驟可修改範例命令語法。  
  
1.  將下列命令複製到 [記事本] 中：  
  
    ```cmd
    Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
    ```  
  
     `/q` 參數會以無訊息模式執行安裝程式，這樣會隱藏使用者介面。  
  
     當針對自動安裝指定了 `/IAcceptSQLServerLicenseTerms` 或 `/q` 參數時，將需要 `/qs`。  
  
     `/action` 參數會指示安裝程式執行安裝。  
  
     `/role` 參數會指示安裝程式安裝 PowerPivot for SharePoint 所需的 Analysis Services 程式和組態檔。 這個角色也會偵測及使用現有的伺服器陣列連接資訊，以存取 SharePoint 組態資料庫。 此為必要參數。 若要指定要安裝的元件，請使用這個參數，而非 `/features` 參數。  
  
     `/instancename` 參數會將 'PowerPivot' 指定為具名執行個體。 這個值為硬式編碼，無法變更。 在命令中指定這個值是為了教育使用者，好讓使用者知道如何安裝此服務。  
  
     `/indicateprogress` 參數可讓您在命令提示字元視窗中監視進度。  
  
2.  此命令會略過 `PID` 參數，這樣會造成 Evaluation Edition 的安裝。 如果您想要安裝 Enterprise Edition，請將 PID 加入至安裝程式命令，並提供有效的產品金鑰。  
  
    ```  
    /PID=<product key for an Enterprise installation>  
    ```  
  
3.  使用有效的使用者\<帳戶和密碼\<來取代網域 \ 使用者名稱> 和設為 strongpassword>的預留位置。  
  
     `/assvaccount`和 **/assvcpassword**參數是用來設定應用程式[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]伺服器上的實例。 請以有效的帳戶資訊取代這些預留位置。  
  
     **/Assysadminaccounts**參數必須設定為正在執行 SQL Server 安裝程式之使用者的身分識別。 您至少必須指定一個系統管理員。 請注意，SQL Server 安裝程式不再授與自動系統管理員 (sysadmin) 權限給內建系統管理員群組的成員。  
  
4.  移除分行符號。  
  
5.  選取整個命令，然後按一下 [編輯] 功能表上的 [**複製**]。  
  
6.  開啟系統管理員命令提示字元。 若要這樣做，請按一下 [**開始**]，以滑鼠右鍵按一下命令提示字元，然後選取 [以**系統管理員身分執行**]。  
  
7.  導覽至包含 SQL Server 安裝媒體的磁碟機或共用資料夾。  
  
8.  將修改過的命令貼到命令列。 若要這麼做，請按一下 [命令提示字元] 視窗左上角的圖示，指向 [**編輯**]，然後按一下 [**貼**上]。  
  
9. 按**enter**鍵以執行命令。 等候安裝程式完成。 您可以在命令提示字元視窗中監視安裝程式的進度。  
  
10. 若要驗證安裝，請檢查位於 \Program Files\SQL Server\120\Setup Bootstrap\Log 的 summary.txt 檔。 如果伺服器安裝成功而沒有任何錯誤，最終的結果應該是 "Passed"。  
  
11. 設定伺服器。 您至少必須要部署方案、建立服務應用程式，並針對每一個網站集合啟用此功能。 如需詳細資訊，請參閱[設定或修復 PowerPivot for SharePoint 2010 &#40;PowerPivot 設定工具&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)或 [[管理中心] 中的 powerpivot 伺服器管理和](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)設定。  
  
## <a name="see-also"></a>另請參閱  
 [設定 PowerPivot 服務帳戶](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)   
 [PowerPivot for SharePoint 2010 安裝](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
