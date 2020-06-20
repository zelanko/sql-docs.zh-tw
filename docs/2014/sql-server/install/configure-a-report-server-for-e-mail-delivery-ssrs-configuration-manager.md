---
title: 為電子郵件傳遞設定報表伺服器（SSRS Configuration Manager） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], distributing
- report servers [Reporting Services], e-mail delivery
- remote SMTP service [Reporting Services]
- distributing reports [Reporting Services], e-mail
- CDO
- Collaboration Data Objects
- SMTP settings [Reporting Services]
- e-mail [Reporting Services]
- sending reports
- mail [Reporting Services]
- local SMTP service [Reporting Services]
ms.assetid: b838f970-d11a-4239-b164-8d11f4581d83
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5f7d99c3459d7bf41a4b9b6552ad6dbb6fe2213c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036980"
---
# <a name="configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager"></a>為電子郵件傳遞設定報表伺服器 (SSRS 組態管理員)


  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含一個電子郵件傳遞延伸模組，讓您能夠透過電子郵件散發報表。 根據您定義電子郵件訂閱的方式而定，傳遞可能會由通知、連結、附加檔案或內嵌報表所組成。 電子郵件傳遞延伸模組可搭配現有的郵件伺服器技術一起使用。 郵件伺服器必須是 SMTP 伺服器或轉送器。 報表伺服器會透過作業系統提供的 Collaboration Data Objects (CDO) 程式庫 (cdosys.dll) 連接到 SMTP 伺服器。  
  
 根據預設，系統並不會設定報表伺服器電子郵件傳遞延伸模組。 您必須使用 Reporting Services 組態管理員，以最低限度的方式設定此延伸模組。 若要設定進階屬性，則必須編輯 `RSReportServer.config` 檔案。 如果您無法將報表伺服器設定為使用此延伸模組，則可以改成將報表傳遞到共用資料夾。 如需詳細資訊，請參閱＜ [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)＞。  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式|  
  
 
  
##  <a name="configuration-requirements"></a><a name="bkmk_configuration_requirements"></a>設定需求  
  
-   報表伺服器電子郵件傳遞是在 Collaboration Data Objects (CDO) 上實作，並需要本機或遠端 Simple Mail Transfer Protocol (SMTP) 伺服器或 SMTP 轉送器。 並非所有的 Windows 作業系統都支援 SMTP。 如果您是使用 Itanium 型版本的 Windows Server 2008，SMTP 將不受支援。 如需有關透過 CDO 提供之組態選項的詳細資訊，請參閱 MSDN 上的 [組態 CoClass](https://go.microsoft.com/fwlink/?LinkId=98237) 。  
  
-   報表伺服器服務帳戶在 SMTP 伺服器上必須擁有傳送郵件的權限。  
  
-   電子郵件傳遞延伸模組會在電子郵件附加檔案中使用 UTF-8 編碼。 您不能修改編碼；HTML 轉譯延伸模組只支援 UTF-8。  
  
> [!NOTE]  
>  預設電子郵件傳遞延伸模組不提供以數位方式，將外寄郵件訊息簽章或加密的支援。  
  
 
  
##  <a name="configuring-a-report-server-for-local-or-remote-smtp-service"></a><a name="bkmk_configure_for_local_or_remote_SMTP"></a>設定本機或遠端 SMTP 服務的報表伺服器  
 您可以使用本機 SMTP 服務，或遠端 SMTP 伺服器或轉送子以支援電子郵件傳遞。 如果您擁有現有之遠端 SMTP 伺服器的存取權，應該考慮使用該存取權。 如果沒有可用的 SMTP 伺服器，或者您隨後遇到因為電腦連接失敗造成的報表傳遞錯誤，則應該切換到使用本機 SMTP 服務。 此主題會進一步提供有關如何設定報表伺服器，以供本機或遠端服務的詳細資料。  
  
  
  
##  <a name="setting-configuration-options-for-e-mail-delivery"></a><a name="bkmk_setting_email_delivery"></a>設定電子郵件傳遞的設定選項  
 您必須先設定提供要使用哪個 SMTP 伺服器之相關資訊的組態值，才能使用報表伺服器電子郵件傳遞。  
  
 若要為電子郵件傳遞設定報表伺服器，請執行下列步驟：  
  
-   如果您只是要指定 SMTP 伺服器和一個擁有傳送電子郵件之權限的使用者帳戶，請使用 Reporting Services 組態管理員。 這些是設定報表伺服器電子郵件傳遞延伸模組時所需的最小設定。 如需詳細資訊，請參閱[電子郵件設定-Configuration Manager &#40;SSRS 原生模式&#41;](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)和[Reporting Services 中的電子郵件傳遞](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)。  
  
-   (選擇性) 請使用文字編輯器在 RSreportserver.config 檔案中指定其他設定。 這個檔案包含報表伺服器電子郵件傳遞的所有組態設定。 如果您要使用本機 SMTP 伺服器，或要設定只能對特定主機進行電子郵件傳遞的限制，則必須在這些檔案中指定其他設定。 如需尋找和修改設定檔的詳細資訊，請參閱 SQL Server 線上叢書中的[修改 Reporting Services 設定檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) 。  
  
> [!NOTE]  
>  報表伺服器電子郵件設定是以 CDO 為基礎。 如果您想要取得有關特定設定的詳細資料，可以參考 CDO 產品文件集。  
  

  
##  <a name="example-report-server-e-mail-configuration"></a><a name="bkmk_example_config_file"></a>報表伺服器電子郵件設定範例  
 下列範例說明遠端 SMTP 伺服器之 RSreportserver.config 檔案中的設定。 若要查看有關設定描述和有效值的資訊，請參閱《 [ssNoVersion](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 線上叢書》中的＜ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl線上叢書》中的＜e or the CDO product documentation.  
  
```  
<RSEmailDPConfiguration>  
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>  
     <SMTPServerPort></SMTPServerPort>  
     <SMTPAccountName></SMTPAccountName>  
     <SMTPConnectionTimeout></SMTPConnectionTimeout>  
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>  
     <SMTPUseSSL></SMTPUseSSL>  
     <SendUsing>2</SendUsing>  
     <SMTPAuthenticate></SMTPAuthenticate>  
     <From>my-rs-email-account@Adventure-Works.com</From>  
     <EmbeddedRenderFormats>  
          <RenderingExtension>MHTML</RenderingExtension>  
     </EmbeddedRenderFormats>  
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>  
     <ExcludedRenderFormats>  
          <RenderingExtension>HTMLOWC</RenderingExtension>  
          <RenderingExtension>NULL</RenderingExtension>  
     </ExcludedRenderFormats>  
     <SendEmailToUserAlias>True</SendEmailToUserAlias>  
     <DefaultHostName></DefaultHostName>  
     <PermittedHosts>  
          <HostName>Adventure-Works.com</HostName>  
          <HostName>hotmail.com</HostName>  
     </PermittedHosts>  
</RSEmailDPConfiguration>  
```  
  

  
##  <a name="configuration-options-for-setting-the-to-field-in-a-message"></a><a name="bkmk_setting_TO_field"></a>在訊息中設定 [To：] 欄位的設定選項  
 依據 [**管理個別訂閱**] 工作所授與的許可權所建立的使用者自訂訂閱，會包含以網域使用者帳戶為基礎的預先設定使用者名稱。 當使用者建立訂閱時，系統就會利用建立訂閱之使用者的網域使用者帳戶，自行處理 **[收件者:]** 欄位中的收件者名稱。  
  
 如果使用 SMTP 伺服器或轉送器，而伺服器或轉送器所使用的電子郵件帳戶與網域使用者帳戶不同時，則 SMTP 伺服器嘗試將報表傳遞給該使用者時便會失敗。  
  
 若要解決這個問題，您可以修改組態，允許使用者在 **[收件者:]** 欄位中輸入名稱：  
  
1.  以文字編輯器開啟 RSReportServer.config。  
  
2.  將 `SendEmailToUserAlias` 設定為 `False`。  
  
3.  將 `DefaultHostName` 設定為 SMTP 伺服器或轉送器的網域名稱系統 (DNS) 名稱或 IP 位址。  
  
4.  儲存檔案。  
  
  
  
##  <a name="configuration-options-for-remote-smtp-service"></a><a name="bkmk_options_remote_SMTP"></a>遠端 SMTP 服務的設定選項  
 報表伺服器和 SMTP 伺服器或轉寄站之間的連接，是由下列組態設定決定：  
  
-   `SendUsing` 指定傳送訊息的方法。 您可以選擇網路 SMTP 服務或本機 SMTP 服務收取目錄。 若要使用遠端 SMTP 服務，必須在 RSReportServer.config 檔案中將此值設定為 **2** 。  
  
-   `SMTPServer` 指定遠端 SMTP 伺服器或轉送子。 如果您使用的是遠端 SMTP 伺服器或轉送子，此值為必要的。  
  
-   `From`設定出現在電子郵件訊息的 [**寄件者：** ] 行中的值。 如果您使用的是遠端 SMTP 伺服器或轉送子，此值為必要的。  
  
 用於遠端 SMTP 服務的其他值包括下列項目 (請注意，除非您要覆寫預設值，否則不需要指定這些值)。  
  
-   **[SMTPServerPort]** 會設定為通訊埠 25。  
  
-   **SMTPAuthenticate** 會指定報表伺服器如何連接到遠端 SMTP 伺服器。 預設值是 0 (或無驗證)。 在此情況下，連接是透過匿名存取。 依照您的網域組態，報表伺服器和 SMTP 伺服器可能必須是同一網域的成員。  
  
     若要傳送電子郵件至限制的通訊群組清單 (例如，只接受來自已驗證帳戶之內送訊息的通訊群組清單)，請將 **[SMTPAuthenticate]** 設定為 **[2]**。  
  

  
##  <a name="configuration-options-for-local-smtp-service"></a><a name="bkmk_options_local_SMTP"></a>本機 SMTP 服務的設定選項  
 如果您是測試報表伺服器電子郵件傳遞或進行疑難排解，則設定本機 SMTP 服務很有用。 根據預設，不會啟用本機 SMTP 服務。 如需如何啟用它的指示，請參閱[為電子郵件傳遞設定報表伺服器（SSRS Configuration Manager）](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)和[電子郵件設定-Configuration Manager &#40;SSRS 原生模式&#41;](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)。  
  
 報表伺服器和本機 SMTP 伺服器或轉寄站之間的連接，是由下列組態設定決定：  
  
-   `SendUsing` 設定為 **1**。  
  
-   **[SMTPServerPickupDirectory]** 設定為本機磁碟機上的資料夾。  
  
    > [!NOTE]  
    >  `SMTPServer`如果您使用的是本機 SMTP 伺服器，請確定未設定。  
  
-   `From`設定出現在電子郵件訊息的 [**寄件者：** ] 行中的值。 這是必要的值。  
  
 
  
##  <a name="to-configure-report-server-e-mail-using-the-reporting-services-configuration-manager"></a><a name="bkmk_use_configuration_manager"></a>若要使用 Reporting Services 組態管理員設定報表伺服器電子郵件  
  
1.  確認報表伺服器 Windows 服務擁有 SMTP 伺服器的 `Send As` 權限。  
  
2.  啟動 Reporting Services 組態管理員，並連接到報表伺服器執行個體。  
  
3.  在 [電子郵件設定] 頁面上，輸入 SMTP 伺服器的名稱。 此值可以是 IP 位址、您公司內部網路之電腦的 UNC 名稱，或是完整的網域名稱。  
  
4.  在 **[寄件者地址]** 中，輸入擁有從 SMTP 伺服器傳送電子郵件之權限的帳戶名稱。  
  
5.  按一下 [套用]。  
  

  
##  <a name="to-configure-a-remote-smtp-service-for-the-report-server"></a><a name="bkmk_confiugre_remote_SMTP"></a>若要設定報表伺服器的遠端 SMTP 服務  
  
1.  確認報表伺服器 Windows 服務擁有 SMTP 伺服器的 `Send As` 權限。  
  
2.  在文字編輯器中開啟 RSReportServer.config 檔。  
  
3.  確認 <`UrlRoot`> 設定為 [報表伺服器 URL] 位址。 此值是在您設定報表伺服器時設定的，所以它應該已被填入。 如果未設定此值，請輸入報表伺服器的 URL 位址。  
  
4.  在 [傳遞] 區段中，尋找 <`ReportServerEmail`>。  
  
5.  在 [<`SMTPServer`> 中，輸入 SMTP 伺服器的名稱。 此值可以是 IP 位址、您公司內部網路之電腦的 UNC 名稱，或是完整的網域名稱。  
  
6.  確認 <`SendUsing`> 設定為2。 如果將它設定為其他值，報表伺服器就不會設定為使用遠端 SMTP 服務。  
  
7.  在 `From` [<> 中，輸入具有從 SMTP 伺服器傳送電子郵件之許可權的帳戶名稱。  
  
8.  儲存檔案。  
  
     報表伺服器會自動使用新的設定；您不需要重新啟動服務。 您可以指定其他 SMTP 設定，來進一步設定如何將 SMTP 伺服器用於報表伺服器電子郵件傳遞。 如需詳細資訊，請參閱 [ssNoVersion](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) 以及 [ssNoVersion](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 線上叢書》中的＜ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl線上叢書》中的＜e.  
  

  
##  <a name="to-configure-a-local-smtp-service-for-the-report-server"></a><a name="bkmk_confiugre_local_SMTP"></a>若要設定報表伺服器的本機 SMTP 服務  
  
1.  在 [控制台] 中，按一下 **[新增或移除程式]**。  
  
2.  按一下 **[新增/移除 Windows 元件]** 以啟動 [Windows 元件精靈]。  
  
3.  選取 **[應用程式伺服器]** 並按一下 **[詳細資料]**。  
  
4.  選取 **[Internet Information Services (IIS)]** ，再按一下 **[詳細資料]**。  
  
5.  選取 **[SMTP 服務]** 核取方塊，再按一下 **[確定]**。  
  
6.  在 [Windows 元件精靈] 中按 **[下一步]**。 按一下 [完成] 。  
  
7.  確認 **[服務]** 主控台中有執行該服務。  
  
8.  在文字編輯器中開啟**RSReportServer.config**檔案。  
  
9. 確認 `<UrlRoot>` 設定為報表伺服器的 URL 位址。 此值是在您設定報表伺服器時設定的，所以它應該已被填入。 如果未設定此值，請輸入報表伺服器的 URL 位址。  
  
10. 在 [傳遞] 區段中，尋找 `<ReportServerEmail>.`。  
  
11. 在 `<SMTPServer>`中，清除此設定的所有值，但不要刪除標記。  
  
12. 請將 `<SendUsing>` 設定為 1。 如果將它設定為其他值，報表伺服器就不會設定為使用本機 SMTP 服務。  
  
13. 將 `<SMTPServerPickupDirectory>` 設定為本機磁碟機上的資料夾。  
  
14. 將 `<From>` 設定為擁有從 SMTP 伺服器傳送電子郵件之權限的帳戶名稱。  
  
15. 儲存檔案。  
  
 
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
