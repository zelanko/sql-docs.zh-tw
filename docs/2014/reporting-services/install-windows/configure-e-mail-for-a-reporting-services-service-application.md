---
title: Reporting Services 服務應用程式 （SharePoint 2010 和 SharePoint 2013），設定電子郵件 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 0e12d4d1c630dcc1e46492cf93582ab5b882e3af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031181"
---
# <a name="configure-e-mail-for-a-reporting-services-service-application-sharepoint-2010-and-sharepoint-2013"></a>設定 Reporting Services 服務應用程式的電子郵件 (SharePoint 2010 和 SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料警示以電子郵件訊息傳送警示。 若要傳送電子郵件，您可能需要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式，以及修改服務應用程式的電子郵件傳遞延伸模組。 如果您計劃針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱功能使用電子郵件傳遞延伸模組，也需要電子郵件設定。  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式&#124;SharePoint 2010 和 SharePoint 2013。|  
  
### <a name="to-configure-e-mail-for-the-shared-service"></a>設定共用服務的電子郵件  
  
1.  在 SharePoint 管理中心中，按一下 **[應用程式管理]**。  
  
2.  在 **[服務應用程式]** 群組中，按一下 **[管理服務應用程式]**。  
  
3.  在 **[名稱]** 清單中，按一下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的名稱。  
  
4.  在 [管理 Reporting Services 應用程式] 頁面上，按一下 [電子郵件設定]。  
  
5.  選取 **[使用 SMTP 伺服器]**。  
  
6.  在 **[外送 SMTP 伺服器]** 方塊中，輸入 SMTP 伺服器的名稱。  
  
7.  在 [來源位址] 方塊中，鍵入電子郵件地址。  
  
     此地址是所有警示電子郵件訊息的寄件者地址。  
  
     在 **[來源位址]** 中指定的使用者帳戶，必須是您在設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的應用程式集區時，所指定的受管理帳戶。 如果您具有權限，您可以在 SharePoint 管理中心的 [服務帳戶] 頁面上，檢視現有受管理帳戶的清單。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="ntlm-authentication"></a>NTLM 驗證  
  
1.  如果您的電子郵件環境需要 NTLM 驗證，且不允許匿名存取，您需要修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的電子郵件傳遞延伸模組組態。 將 **SMTPAuthenticate** 變更為使用值 "2"。 您無法從使用者介面變更此值。 下列 PowerShell 指令碼範例會更新服務應用程式 "SSRS_TESTAPPLICATION" 之報表伺服器電子郵件傳遞延伸模組的完整組態。 請注意，指令碼中列出的部分節點也可以透過使用者介面設定，例如 [寄件者] 地址。  
  
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
  
  