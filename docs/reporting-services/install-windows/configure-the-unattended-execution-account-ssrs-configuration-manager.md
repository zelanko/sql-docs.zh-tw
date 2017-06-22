---
title: "設定自動的執行帳戶 （SSRS 組態管理員） |Microsoft 文件"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- no credentials option [Reporting Services]
- security [Reporting Services], unattended report processing
- unattended report processing [Reporting Services]
- credentials [Reporting Services]
- external data sources [Reporting Services]
- accounts [Reporting Services]
- reports [Reporting Services], processing
ms.assetid: 4e50733e-bd8c-4bf6-8379-98b1531bb9ca
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4c18054b5c11569239af51e7c3808bdb9ce05109
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="configure-the-unattended-execution-account-ssrs-configuration-manager"></a>設定自動執行帳戶 (SSRS 組態管理員)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了一個特殊帳戶，它是用於自動報表處理和透過網路傳送連接要求。 以下是使用此帳戶的方式：  
  
-   透過網路針對使用資料庫驗證的報表傳送連接要求，或是連接到不需要或不使用驗證的外部報表資料來源。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [指定報表資料來源的認證和連接資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) 。  
  
-   擷取報表中使用的外部影像檔。 如果想要使用影像檔而該檔案無法透過匿名存取來存取，則您可以設定自動報表處理帳戶，並授與該帳戶存取檔案的權限。  
  
 自動報表處理是指由事件觸發 (不論是排程驅動事件或資料重新整理事件)，而非由使用者要求觸發的任何報表執行處理。 報表伺服器使用自動報表處理帳戶，來登入主控外部資料來源的電腦。 因為報表伺服器服務帳戶的認證絕不會用來連接到其他電腦，所以需要此帳戶。  
  
> [!IMPORTANT]  
>  設定此帳戶是選擇性的。 不過，如果沒有加以設定，您就可能無法連接到某些資料來源，而且可能無法從遠端電腦擷取影像檔。 如果您真的設定帳戶，就必須讓它保持最新狀態。 特別是如果您讓密碼過期或者 Active Directory 中的帳戶資訊變更，則下次在處理報表時，您將遇到下列的錯誤訊息：「登入失敗 (rsLogonFailed) 登入失敗：未知的使用者名稱或密碼錯誤。」 正確維護自動報表處理帳戶是很重要的，即使您從未擷取外部影像或傳送對外部電腦的連接要求也是如此。 如果在設定帳戶之後發現並未使用該帳戶，可以將其刪除，這樣就不需經常進行帳戶維護工作。  
  
## <a name="how-to-configure-the-account"></a>如何設定帳戶  
 您必須使用網域使用者帳戶。 為了提供原先預期的用途，此帳戶應該與用來執行報表伺服器服務的帳戶不同。 請務必使用符合下列條件的帳戶：擁有最小權限 (具有網路連接的唯讀存取權限就足夠)，而且僅擁有提供資料來源和資源給報表伺服器之電腦的有限存取權。  
  
 若要指定此帳戶，您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具或 **rsconfig** 公用程式。 設定自動執行帳戶的最簡單方法，是執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並在 [執行帳戶] 頁面中指定認證。  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到您要設定的報表伺服器執行個體。 如需指示，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)。  
  
2.  在 [執行帳戶] 頁面上，選取 [指定執行帳戶]。  
  
3.  輸入帳戶和密碼，重新輸入密碼，然後按一下 [套用]。  
  
### <a name="using-rsconfig-utility"></a>使用 RSCONFIG 公用程式  
 設定此帳戶的另一個方法是使用 **rsconfig** 公用程式。 若要指定帳戶，請使用 **rsconfig** 的 **-e**引數。 指定 **rsconfig** 的 **-e** 引數，會引導公用程式將帳戶資訊寫入組態檔。 您不需要指定 RSreportserver.config 的路徑。 請遵循以下步驟來設定帳戶。  
  
1.  建立或選取網域帳戶，該帳戶擁有提供資料或服務給報表伺服器之電腦和伺服器的存取權。 您應使用擁有較小權限的帳戶 (例如唯讀權限)。  
  
2.  開啟命令提示字元：在 [開始] 功能表上，按一下 [執行]，輸入 **cmd**，然後按一下 [確定]。  
  
3.  輸入下列命令，即可在本機報表伺服器執行個體上設定帳戶：  
  
     **rsconfig-e-u\<網域/使用者名稱 >-p\<密碼 >**  
  
 **rsconfig -e** 可支援其他引數。 如需語法的詳細資訊以及若要檢視命令範例，請參閱《SQL Server 線上叢書》中的[rsconfig 公用程式&#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)。  
  
### <a name="how-account-information-is-stored"></a>如何儲存帳戶資訊  
 當您設定此帳戶時，下列設定會當做加密的值指定於本機或遠端報表伺服器執行個體上的 RSreportserver.config 檔案中：  
  
```  
<UnattendedExecutionAccount>  
     <UserName></UserName>  
     <Password></Password>  
     <Domain></Domain>  
</UnattendedExecutionAccount>  
```  
  
 您設定了值之後，就不能將值解密，以純文字檢視這些值。 如果您輸入錯誤的值，或者忘記自己指定的值，就必須使用 Reporting Services 組態工具，或執行 **rsconfig -e** 以重新開始。  
  
## <a name="how-to-use-the-unattended-report-processing-account"></a>如何使用自動報表處理帳戶  
 為了擷取影像檔，報表伺服器會自動使用此帳戶，而且您不需要採取特定的動作。 若要使用此帳戶連接到提供資料給報表的外部資料來源，您必須在報表資料來源或共用資料來源的資料來源屬性頁面上指定 [認證類型] 選項：  
  
-   在 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]或 SharePoint 網站上，選取 [不需要認證] 選項。  
  
 自動報表處理帳戶主要是用來連接外部伺服器，而不是登入資料庫伺服器。 如果您想要使用此帳戶認證來登入資料庫，就必須在連接字串中指定認證。 如果資料庫伺服器支援 Windows 整合式安全性，而且自動報表處理所使用的帳戶擁有讀取資料庫的權限，您就可以指定 **Integrated Security=SSPI** 。 否則，您必須在連接字串中輸入使用者名稱和密碼，而此連接字串會以純文字格式顯示給有權編輯資料來源連接屬性的任何使用者查看。  
  
 雖然系統不會禁止您在建立連接之後使用自動報表處理帳戶來擷取資料，但是我們不建議您這樣做。 您應該針對非常特定的功能使用此帳戶。 如果您用它來擷取資料，就會破壞它原本設計的用途。  
  
## <a name="how-to-maintain-the-unattended-report-processing-account"></a>如何維護自動報表處理帳戶  
 一旦定義此帳戶後，就必須確保帳戶和密碼都保持最新狀態。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來更新儲存此帳戶之相關資訊的組態設定。  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到您要設定的報表伺服器執行個體。  
  
2.  在 [執行帳戶] 頁面上，確認已經選取 [指定執行帳戶]。  
  
3.  輸入新帳戶和密碼，重新輸入密碼，然後按一下 [套用]。  
  
## <a name="how-to-delete-the-unattended-report-processing-account"></a>如何刪除自動報表處理帳戶  
 如果沒有使用此帳戶，可以將其刪除，這樣就不需經常進行帳戶維護工作。  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到您要設定的報表伺服器執行個體。  
  
2.  在 [執行帳戶] 頁面上，清除 [指定執行帳戶]。  
  
3.  按一下 **[套用]**。  
  
 帳戶資訊會隨即從 RSReportServer.config 檔案中移除。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 (SSRS 原生模式)](http://msdn.microsoft.com/en-us/379eab68-7f13-4997-8d64-38810240756e)  
  
  

