---
title: 對 Windows Token Service (C2WTS) 和 Reporting Services 的宣告 |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0f6443f8015d3b2a4c94c9470a35a5b1433691d8
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354348"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>對 Windows Token 服務 (C2WTS) 和 Reporting Services 的宣告
  SharePoint 對 Windows Token Service 宣告 (c2WTS) 是必要項目[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式，如果您想要針對 SharePoint 伺服器陣列以外的資料來源使用 windows 驗證。 使用者若是利用 Windows 驗證存取資料來源也是如此，因為 Web 前端 (WFE) 與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務之間的通訊皆會使用宣告驗證。  
  
 即使資料來源位於共用服務所在的同一部電腦上，也必須使用 c2WTS。 但此情況無須使用限制委派。  
  
 c2WTS 所建立的 Token 只可與限制委派 (僅限特定服務使用) 及組態選項 [使用任何驗證通訊協定] 並用。 如前文所述，資料來源與共用服務若是位在同一部電腦上，即無須使用限制委派。  
  
 如果您的環境會使用 Kerberos 限制委派，則 SharePoint Server 服務及外部資料來源必須位於相同的 Windows 網域。 相依於 Windows Token 服務之宣告 (c2WTS) 的任何服務，都必須使用 Kerberos **限制** 委派，才能讓 c2WTS 使用 Kerberos 通訊協定轉換將宣告轉譯成 Windows 認證。 這些需求對於所有 SharePoint Shared 服務都是如此。 如需詳細資訊，請參閱 <<c0> [ 適用於 Microsoft SharePoint 2010 產品的概觀的 Kerberos 驗證 (https://technet.microsoft.com/library/gg502594.aspx)](https://technet.microsoft.com/library/gg502594.aspx)。  
  
 本主題中會概述此程序。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
## <a name="prerequisites"></a>先決條件  
  
> [!NOTE]  
>  注意：在某些伺服器陣列拓撲中，部分組態步驟可能會有所變更或無法使用。 例如單一伺服器安裝並不支援 Windows Identity Foundation c2WTS 服務，因此即無法在此伺服器陣列組態使用對 Windows Token 委派的宣告。  
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>設定 c2WTS 所需的基本步驟  
  
1.  設定 c2WTS 服務帳戶。 在每部執行 c2WTS 的應用程式伺服器的本機 Administrators 群組中加入服務帳戶。 此外，確認帳戶具有下列本機安全性原則權限︰  
  
    -   作為作業系統的一部分  
  
    -   在驗證後模擬用戶端  
  
    -   登入為服務  
  
     您用於 c2WTS 的帳戶也必須設有通訊協定轉換之限制委派設定，且需要委派給它，才能與 （也就是 SQL Server 引擎、 SQL Server Analysis Services） 進行通訊之服務的權限。若要設定委派，您可以使用 Active Directory 使用者和電腦嵌入式管理單元。  
  
    1.  以滑鼠右鍵按一下各服務帳戶，以開啟屬性對話方塊。 按一下對話方塊中的 [委派] 索引標籤。  
  
        > [!NOTE]  
        >  注意：物件必須指派有 SPN，才會顯示委派索引標籤。 c2WTS 不需要 c2WTS 帳戶的 SPN，但無 SPN，**委派** 索引標籤就不會顯示。 另一種設定限制委派的方法是使用 **ADSIEdit**這類的公用程式。  
  
    2.  以下是 [委派] 索引標籤上的主要組態選項：  
  
        -   選取 信任這個使用者委派指定的服務 」  
  
        -   選取 [使用任何驗證通訊協定]  
  
         如需詳細資訊，請參閱 「 設定電腦的 Kerberos 限制委派和服務帳戶 > 一節的下列技術白皮書：[適用於 SharePoint 2010 和 SQL Server 2008 R2 產品設定 Kerberos 驗證](http://blogs.technet.com/b/tothesharepoint/archive/2010/07/22/whitepaper-configuring-kerberos-authentication-for-sharepoint-2010-and-sql-server-2008-r2-products.aspx)  
  
2.  設定 c2WTS 'AllowedCallers'  
  
     c2WTS 必須明確的 'callers' 識別組態檔中，列出**c2wtshost.exe.config**。 c2WTS 不接受來自所有已驗證的使用者要求系統中除非它被設定為執行這項操作。 本例中的 'caller' 是 WSS_WPG Windows 群組。 c2wtshost.exe.confi 檔案會儲存在下列位置：  
  
     **Files\windows 識別 Foundation\v3.5\c2wtshost.exe.config**  
  
     以下是組態檔的範例：  
  
    ```  
    <configuration>  
      <windowsTokenService>  
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->  
        <allowedCallers>  
          <clear/>  
          <add value="WSS_WPG" />  
        </allowedCallers>  
      </windowsTokenService>  
    </configuration>  
    ```  
  
3.  啟動作業系統的 c2WTS 服務：  
  
    1.  將該服務設定成使用您在前述步驟中設定的服務帳戶。  
  
    2.  將啟動類型變更為 「**自動**」 並啟動服務。  
  
4.  啟動 SharePoint 對 Windows Token Service 的宣告':從 [管理伺服器上的服務] 上的 SharePoint 管理中心啟動對 Windows Token 服務的宣告。 您應在要執行動作的伺服器上啟動該服務。 例如您有一部 WFE 伺服器及另一部執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務的應用程式伺服器，就只需在應用程式伺服器上啟動 c2WTS。 WFE 並不需要 c2WTS。  
  
## <a name="see-also"></a>另請參閱  
 [宣告對 Windows Token Service (c2WTS) 概觀 （ https://msdn.microsoft.com/library/ee517278.aspx)](https://msdn.microsoft.com/library/ee517278.aspx)   
 [（Microsoft SharePoint 2010 產品的 Kerberos 驗證概觀 https://technet.microsoft.com/library/gg502594.aspx)](https://technet.microsoft.com/library/gg502594.aspx)  
  
  
