---
title: "設定 Reporting Services 服務應用程式的電子郵件 (SharePoint 2013 和 SharePoint 2016) | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# 設定 Reporting Services 服務應用程式的電子郵件 (SharePoint 2013 和 SharePoint 2016)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料警示以電子郵件訊息傳送警示。 若要傳送電子郵件，您可能需要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式，以及修改服務應用程式的電子郵件傳遞延伸模組。 如果您計劃針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱功能使用電子郵件傳遞延伸模組，也需要電子郵件設定。  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式 &#124; SharePoint 2013 和 SharePoint 2016。|  
  
### 設定共用服務的電子郵件  
  
1.  在 SharePoint 管理中心中，按一下 **[應用程式管理]**。  
  
2.  在 **[服務應用程式]** 群組中，按一下 **[管理服務應用程式]**。  
  
3.  在 **[名稱]** 清單中，按一下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的名稱。  
  
4.  在 [管理 Reporting Services 應用程式] 頁面上，按一下 [電子郵件設定]。  
  
5.  選取 **[使用 SMTP 伺服器]**。  
  
6.  在 **[外送 SMTP 伺服器]** 方塊中，輸入 SMTP 伺服器的名稱。  
  
7.  在 [來源位址] 方塊中，輸入電子郵件地址。  
  
     此地址是所有警示電子郵件訊息的寄件者地址。  
  
     在 **[來源位址]** 中指定的使用者帳戶，必須是您在設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的應用程式集區時，所指定的受管理帳戶。 如果您具有權限，您可以在 SharePoint 管理中心的 [服務帳戶] 頁面上，檢視現有受管理帳戶的清單。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### NTLM 驗證  
  
1.  如果您的電子郵件環境需要 NTLM 驗證，且不允許匿名存取，您需要修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的電子郵件傳遞延伸模組組態。 例如，如果您在 [管理訂閱]  頁面的 [上次結果]  中看到下列訊息：訂閱。  
  
    -   傳送郵件失敗: SMTP 伺服器需要安全連接，或用戶端未經驗證。 伺服器回應為: 5.7.1 用戶端未經驗證。將不會重新傳送郵件。  
  
     將 **SMTPAuthenticate** 變更為使用值 "2"。 您無法從使用者介面變更此值。 下列 PowerShell 指令碼範例會更新服務應用程式 "SSRS_TESTAPPLICATION" 之報表伺服器電子郵件傳遞延伸模組的完整組態。 請注意，指令碼中列出的部分節點也可以透過使用者介面設定，例如 [寄件者] 地址。  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
    $emailXml = [xml]$emailCfg   
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = “your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = “your FROM email address”  
    Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  如果您需要確認服務應用程式的名稱，請執行 **Get-SPRSServiceApplication Cmdlet**。  
  
    ```  
    get-sprsserviceapplication  
    ```  
  
3.  下列範例會傳回服務應用程式 "SSRS_TESTAPPLICATION" 之電子郵件延伸模組的目前值。  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
    ```  
  
4.  下列範例會使用服務應用程式 "SSRS_TESTAPPLICATION" 之電子郵件延伸模組的目前值，建立名為 "emailconfig.txt" 的新檔案。  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml | out-file c:\emailconfig.txt  
    ```  
  
  