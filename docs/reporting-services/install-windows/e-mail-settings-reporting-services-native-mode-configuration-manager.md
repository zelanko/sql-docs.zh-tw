---
title: 電子郵件設定 - Reporting Services 原生模式 (設定管理員) | Microsoft Docs
ms.date: 06/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
f1_keywords:
- SQL13.rsconfigtool.emailsettings.F1
helpviewer_keywords:
- SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ab2d4208d26ca6da5188e635dda8183c545d6f3e
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50020392"
---
# <a name="e-mail-settings---reporting-services-native-mode-configuration-manager"></a>電子郵件設定 - Reporting Services 原生模式 (組態管理員)
Reporting Services 包含一個電子郵件傳遞延伸模組，讓您能夠透過電子郵件散發報表。 根據您定義電子郵件訂閱的方式而定，傳遞可能會由通知、連結、附加檔案或內嵌報表所組成。 電子郵件傳遞延伸模組可搭配現有的郵件伺服器技術一起使用。 郵件伺服器必須是 SMTP 伺服器或轉送器。 報表伺服器會透過作業系統提供的 Collaboration Data Objects (CDO) 程式庫 (cdosys.dll) 連接到 SMTP 伺服器。

根據預設，系統並不會設定報表伺服器電子郵件傳遞延伸模組。 您必須使用 Reporting Services 組態管理員，以最低限度的方式設定此延伸模組。 若要設定進階屬性，則必須編輯 RSReportServer.config 檔案。 如果您無法將報表伺服器設定為使用此延伸模組，則可以改成將報表傳遞到共用資料夾。 如需詳細資訊，請參閱＜File Share Delivery in Reporting Services＞(Reporting Services 中的檔案共用傳遞)。

## <a name="configuration-requirements"></a>組態需求

- 報表伺服器電子郵件傳遞是在 Collaboration Data Objects (CDO) 上實作，並需要本機或遠端 Simple Mail Transfer Protocol (SMTP) 伺服器或 SMTP 轉送器。 並非所有的 Windows 作業系統都支援 SMTP。 如果您是使用 Itanium 型版本的 Windows Server 2008，SMTP 將不受支援。 如需有關透過 CDO 提供之組態選項的詳細資訊，請參閱 MSDN 上的 [組態 CoClass](https://go.microsoft.com/fwlink/?LinkId=98237) 。

已設定驗證的帳戶在 SMTP 伺服器上必須擁有傳送郵件的權限。

- 電子郵件傳遞延伸模組會在電子郵件附加檔案中使用 UTF-8 編碼。 您不能修改編碼；HTML 轉譯延伸模組只支援 UTF-8。

> [!NOTE] 
> 預設電子郵件傳遞延伸模組不提供以數位方式，將外寄郵件訊息簽章或加密的支援。

## <a name="setting-configuration-options-for-e-mail-delivery"></a>設定電子郵件傳遞的組態選項
您必須先設定提供要使用哪個 SMTP 伺服器之相關資訊的組態值，才能使用報表伺服器電子郵件傳遞。

若要為電子郵件傳遞設定報表伺服器，請執行下列步驟：

- 如果您只是要指定 SMTP 伺服器和一個擁有傳送電子郵件之權限的使用者帳戶，請使用 Reporting Services 組態管理員。 這些是設定報表伺服器電子郵件傳遞延伸模組時所需的最小設定。

- (選擇性) 請使用文字編輯器在 RSreportserver.config 檔案中指定其他設定。 這個檔案包含報表伺服器電子郵件傳遞的所有組態設定。 如果您要使用本機 SMTP 伺服器，或要設定只能對特定主機進行電子郵件傳遞的限制，則必須在這些檔案中指定其他設定。 如需尋找和修改組態檔的詳細資訊，請參閱《SQL Server 線上叢書》中的 [Modify a Reporting Services Configuration File (rsreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) (修改 Reporting Services 組態檔 (RSreportserver.config))。

> [!NOTE] 
> 報表伺服器電子郵件設定是以 CDO 為基礎。 如果您想要取得有關特定設定的詳細資料，可以參考 CDO 產品文件集。

## <a name="a-namersconfigmanconfigure-report-server-e-mail-using-the-reporting-services-configuration-manager"></a><a name="rsconfigman"/>使用 Reporting Services 管理員設定報表伺服器電子郵件

1. 啟動 Reporting Services 組態管理員，並連接到報表伺服器執行個體。

2. 在 [寄件者地址] 中輸入要產生的電子郵件 [寄件者:] 欄位中使用的電子郵件地址。 

     您必須指定有權從 SMTP 伺服器傳送郵件的使用者帳戶。 您在 [寄件者地址] 鍵入的值會儲存在 rsreportserver.config 檔案的 [`<From>`] 欄位中。  

3.  在 [SMTP 伺服器] 中，指定要使用的 SMTP 伺服器或閘道。 

     此值可以是 IP 位址、您公司內部網路之電腦的 NetBIOS 名稱，或是完整的網域名稱。 您在 [SMTP 伺服器] 鍵入的值會儲存在 rsreportserver.config 檔案的 [`<SMTPServer>`] 欄位中。

4. 使用 [驗證] 下拉式清單來指定如何驗證 SMTP 伺服器。 此 

     - [不需要驗證] 表示您會以匿名方式連接到指定的郵件伺服器。
     
          選取此選項會在 rsreportserver.config 中將 `<SendUsing>` 設為 **2** 值，將 `<SMTPAuthenticate>` 設為 **0** 值。
     
     - [使用者名稱與密碼 (基本)] 可讓您指定連接到郵件伺服器的使用者名稱和密碼。 您也可以選取 [使用安全連線] 使用您郵件伺服器的加密連線。
     
          選取此選項會在 rsreportserver.config 中將 `<SendUsing>` 設為 **2** 值，將 `<SMTPAuthenticate>` 設為 **1** 值。選取 [使用安全連線] 會將 `SMTPUseSSL` 設為 **True**。 **中的** 使用者名稱 `<SendUserName>` 會設為加密值。 **中的** 密碼 `<SendPassword>` 會設為加密值。
     
     - [報表伺服器服務帳戶 (NTLM)] 會使用您為報表伺服器指定的服務帳戶。 如果使用報表伺服器服務帳戶進行驗證，請確認服務帳戶具有 SMTP 伺服器的 **傳送為** 權限。
     
          選取此選項會在 rsreportserver.config 中將 `<SendUsing>` 設為 **2** 值，將 `<SMTPAuthenticate>` 設為 **2** 值。

5. 選取 [套用]。

6. 您也可以在 rsreportserver.config 中調整電子郵件組態的其他欄位。

## <a name="example-report-server-e-mail-configuration"></a>範例報表伺服器電子郵件組態
下列範例說明遠端 SMTP 伺服器之 RSreportserver.config 檔案中的設定。 如需設定描述和有效值的相關資訊，請參閱《SQL Server 線上叢書》中的 [Rsreportserver.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 。

```
<RSEmailDPConfiguration>
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>
     <SMTPServerPort></SMTPServerPort>
     <SMTPAccountName></SMTPAccountName>
     <SMTPConnectionTimeout></SMTPConnectionTimeout>
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>
     <SMTPUseSSL>False</SMTPUseSSL>
     <SendUsing>2</SendUsing>
     <SMTPAuthenticate>2</SMTPAuthenticate>
     <From>my-rs-email-account@Adventure-Works.com</From>
     <EmbeddedRenderFormats>
          <RenderingExtension>MHTML</RenderingExtension>
     </EmbeddedRenderFormats>
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>
     <ExcludedRenderFormats>
          <RenderingExtension>HTMLOWC</RenderingExtension>
          <RenderingExtension>NULL</RenderingExtension>
          <RenderingExtension>RGDI</RenderingExtension>
     </ExcludedRenderFormats>
     <SendEmailToUserAlias>True</SendEmailToUserAlias>
     <DefaultHostName></DefaultHostName>
     <PermittedHosts>
          <HostName>Adventure-Works.com</HostName>
          <HostName>hotmail.com</HostName>
     </PermittedHosts>
     <SendUserName></SendUserName>
     <SendPassword></SendPassword>
</RSEmailDPConfiguration>
```
## <a name="configuration-options-for-setting-the-to-field-in-a-message"></a>設定郵件收件者欄位的組態選項
如果依據 [管理個別訂閱] 工作所授與的權限建立使用者自訂訂閱，這些訂閱中便會包含以網域使用者帳戶為基礎的預設使用者名稱。 當使用者建立訂閱時，系統就會利用建立訂閱之使用者的網域使用者帳戶，自行處理 **[收件者:]** 欄位中的收件者名稱。

如果使用 SMTP 伺服器或轉送器，而伺服器或轉送器所使用的電子郵件帳戶與網域使用者帳戶不同時，則 SMTP 伺服器嘗試將報表傳遞給該使用者時便會失敗。

若要解決這個問題，您可以修改組態，允許使用者在 **[收件者:]** 欄位中輸入名稱：

1. 以文字編輯器開啟 RSReportServer.config。

2. 將 `<SendEmailToUserAlias>` 設為 **False**。

3. 將 `<DefaultHostName>` 設定為 SMTP 伺服器或轉送器的網域名稱系統 (DNS) 名稱或 IP 位址。

4. 儲存檔案。

## <a name="configuration-options-for-remote-smtp-service"></a>遠端 SMTP 服務的組態選項
報表伺服器和 SMTP 伺服器或轉寄站之間的連接，是由下列組態設定決定：

- `<SendUsing>` 指定傳送訊息的方法。 您可以選擇網路 SMTP 服務或本機 SMTP 服務收取目錄。 若要使用遠端 SMTP 服務，必須在 RSReportServer.config 檔案中將此值設定為 **2** 。
- `<SMTPServer>` 指定遠端 SMTP 伺服器或轉送子。 如果您使用的是遠端 SMTP 伺服器或轉送子，此值為必要的。
- [`<From>`] 設定的值，會在電子郵件訊息 [寄件者:] 行內顯示。 如果您使用的是遠端 SMTP 伺服器或轉送子，此值為必要的。

用於遠端 SMTP 服務的其他值包括下列項目 (請注意，除非您要覆寫預設值，否則不需要指定這些值)。

- `<SMTPServerPort>` 預設設定為連接埠 25。
- `<SMTPAuthenticate>` 指定報表伺服器如何連接到遠端 SMTP 伺服器。 預設值是 **0** (或無驗證)。 在此情況下，連接是透過匿名存取。 依照您的網域組態，報表伺服器和 SMTP 伺服器可能必須是同一網域的成員。
- 若要傳送電子郵件至限制的通訊群組清單 (例如，只接受來自已驗證帳戶之內送訊息的通訊群組清單)，請將 `<SMTPAuthenticate>` 設為 **1** 或 **2**。 如果設為 **1**，就也要設定 `<SendUserName>` 和 `<SendPassword>`。 建議透過 Reporting Services 組態管理員執行此作業，因為它會加密 `<SendUserName>` 和 `<SendPassword>`的值。

### <a name="to-configure-a-remote-smtp-service-for-the-report-server"></a>若要為報表伺服器設定遠端 SMTP 服務

> [!NOTE] 
> 建議您透過 Reporting Services 組態管理員設定郵件伺服器。

1. 確認報表伺服器 Windows 服務擁有 SMTP 伺服器的 **Send As** 權限。

2. 在文字編輯器中開啟 RSReportServer.config 檔。

3. 確認 `<UrlRoot>` 設定為報表伺服器的 URL 位址。 此值是在您設定報表伺服器時設定的，所以它應該已被填入。 如果未設定此值，請輸入報表伺服器的 URL 位址。

4. 在 [傳遞] 區段中，尋找 `<RSEmailDPConfiguration>`。
     
5. 在 `<SMTPServer>`中，輸入 SMTP 伺服器的名稱。 此值可以是 IP 位址、您公司內部網路之電腦的 UNC 名稱，或是完整的網域名稱。

6. 將 `<SendUsing>` 設為 **2** 值以使用報表伺服器的服務帳戶。 將 `<SendUsing>` 設為 **1** 值以進行基本驗證。 如果設為 **1**，即必須另外提供 `<SendUserName>` 和 `<SendPassword>`的值。 如果想要加密這些值，請在 Reporting Services 組態管理員內設定驗證。

7. 如果 `<SMTPAuthenticate>` 設為 1 或 2，請將 **設為** 1 `<SendUsing>` 值。

7. 設定 `<From>`。 您必須指定有權從 SMTP 伺服器傳送郵件的使用者帳戶。

8. 儲存檔案。

     報表伺服器會自動使用新的設定；您不需要重新啟動服務。 您可以指定其他 SMTP 設定，來進一步設定如何將 SMTP 伺服器用於報表伺服器電子郵件傳遞。

## <a name="configuration-options-for-local-smtp-service"></a>本機 SMTP 服務的組態選項
如果您是測試報表伺服器電子郵件傳遞或進行疑難排解，則設定本機 SMTP 服務很有用。 根據預設，不會啟用本機 SMTP 服務。

報表伺服器和本機 SMTP 伺服器或轉寄站之間的連接，是由下列組態設定決定：

- **[SendUsing]** 設定為 **[1]**。
- **[SMTPServerPickupDirectory]** 設定為本機磁碟機上的資料夾。

  > [!NOTE] 
  > 如果是使用本機 SMTP 伺服器，請確定並未設定 SMTPServer。

- **[寄件者]** 設定的值，會在電子郵件訊息 **[寄件者:]** 行內顯示。 這是必要的值。

### <a name="to-configure-a-local-smtp-service-for-the-report-server"></a>若要為報表伺服器設定本機 SMTP 服務

1. 在 [控制台] 中選取 [開啟或關閉 Windows 功能] 來啟動 [新增角色及功能精靈]。

2. 選取 [角色型或功能型安裝]，然後選取 [下一步]。

3. 選取要安裝 Internet Information Server (IIS) 的伺服器，然後選取 [下一步]。

4. 選取 [伺服器角色]* 頁面的 [下一步]。
     
5. 選取 [功能] 頁面上的 [SMTP 伺服器]，然後選取 [下一步]。

     如果系統提示您新增 SMTP 伺服器所需的功能，請選取 [新增功能]。

6. 選取 [網頁伺服器角色 (IIS)] 頁面的 [下一步]。

7. 選取 [角色服務] 頁面的 [下一步]。

8. 選取 [確認] 頁面上的 [安裝]。

9. 確認 [服務] 主控台正在執行 **簡易郵件傳送通訊協定 (SMTP)** Windows 服務。

     若要設定本機 SMTP 伺服器，您必須使用系統管理工具下的 IIS 6.0 管理員。

10. 在文字編輯器中開啟 RSReportServer.config 檔。

11. 確認 `<UrlRoot>` 設定為報表伺服器的 URL 位址。 此值是在您設定報表伺服器時設定的，所以它應該已被填入。 如未設定，請輸入報表伺服器的 Web 服務 URL 位址。

12. 在 [傳遞] 區段中，尋找 `<RSEmailDPConfiguration>`。
     
13. 請確定有空白的 `<SMTPServer>` 。
     
14. 請將 `<SendUsing>` 設定為 1。
     
14. 請將 `<SMTPAuthenticate>` 設為 0。
     
15. 請將 `<SMTPServerPickupDirectory>` 設為 SMTP 服務收取資料夾。
     
     預設位置是 *C:\inetpub\mailroot\Pickup*。
     
16. 設定 `<From>`。 這會設定電子郵件訊息 [寄件者:] 行內顯示的值。
     
17. 儲存檔案。
  
## <a name="see-also"></a>另請參閱  
[Reporting Services 組態管理員 (原生模式)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
[Modify a Reporting Services Configuration File (rsreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
[Rsreportserver.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)
  
  
