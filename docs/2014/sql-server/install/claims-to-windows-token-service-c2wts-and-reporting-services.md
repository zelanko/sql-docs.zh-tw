---
title: 對 Windows Token 服務的宣告（C2WTS）和 Reporting Services |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0ec82b7cca2062e1ed918e300eeb76dad16cbb20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245616"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>對 Windows Token 服務 (C2WTS) 和 Reporting Services 的宣告
  如果您想要針對 SharePoint 伺服器陣列以外的資料來源使用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] windows 驗證，sharepoint 模式需要 Sharepoint 對 Windows Token 服務的宣告（c2WTS）。 使用者若是利用 Windows 驗證存取資料來源也是如此，因為 Web 前端 (WFE) 與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務之間的通訊皆會使用宣告驗證。  
  
 即使資料來源位於共用服務所在的同一部電腦上，也必須使用 c2WTS。 但此情況無須使用限制委派。  
  
 c2WTS 所建立的 Token 只可與限制委派 (僅限特定服務使用) 及組態選項 [使用任何驗證通訊協定] 並用。 如前文所述，資料來源與共用服務若是位在同一部電腦上，即無須使用限制委派。  
  
 如果您的環境會使用 Kerberos 限制委派，則 SharePoint Server 服務及外部資料來源必須位於相同的 Windows 網域。 相依於 Windows Token 服務之宣告 (c2WTS) 的任何服務，都必須使用 Kerberos **限制** 委派，才能讓 c2WTS 使用 Kerberos 通訊協定轉換將宣告轉譯成 Windows 認證。 這些需求對於所有 SharePoint Shared 服務都是如此。 如需詳細資訊，請參閱[Microsoft SharePoint 2010 產品的 Kerberos 驗證總覽https://technet.microsoft.com/library/gg502594.aspx)（](https://technet.microsoft.com/library/gg502594.aspx)。  
  
 本主題中會概述此程序。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
## <a name="prerequisites"></a>Prerequisites  
  
> [!NOTE]  
>  注意：在某些伺服器陣列拓撲中，部分組態步驟可能會有所變更或無法使用。 例如單一伺服器安裝並不支援 Windows Identity Foundation c2WTS 服務，因此即無法在此伺服器陣列組態使用對 Windows Token 委派的宣告。  
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>設定 c2WTS 所需的基本步驟  
  
1.  設定 c2WTS 服務帳戶。 在每部執行 c2WTS 的應用程式伺服器的本機 Administrators 群組中加入服務帳戶。 此外，確認帳戶具有下列本機安全性原則權限︰  
  
    -   作為作業系統的一部分  
  
    -   在驗證後模擬用戶端  
  
    -   登入為服務  
  
     您用於 c2WTS 的帳戶也必須設定為具有通訊協定轉換的限制委派，而且需要委派給所需的服務（例如 SQL Server 引擎、SQL Server Analysis Services）。若要設定委派，您可以使用 [Active Directory 使用者和電腦] 嵌入式管理單元。  
  
    1.  以滑鼠右鍵按一下各服務帳戶，以開啟屬性對話方塊。 按一下對話方塊中的 [委派]**** 索引標籤。  
  
        > [!NOTE]  
        >  注意：物件必須指派有 SPN，才會顯示委派索引標籤。 c2WTS 不需要 c2WTS 帳戶的 SPN，但若沒有 SPN，將不會顯示 [**委派**] 索引標籤。 另一種設定限制委派的方法是使用 **ADSIEdit**這類的公用程式。  
  
    2.  以下是 [委派] 索引標籤上的主要組態選項：  
  
        -   選取 [信任這個使用者，但只委派指定的服務]  
  
        -   選取 [使用任何驗證通訊協定]  
  
         如需詳細資訊，請參閱下列白皮書中的「設定電腦和服務帳戶的 Kerberos 限制委派」一節，為[SharePoint 2010 和 SQL Server 2008 R2 產品設定 kerberos 驗證](https://blogs.technet.com/b/tothesharepoint/archive/2010/07/22/whitepaper-configuring-kerberos-authentication-for-sharepoint-2010-and-sql-server-2008-r2-products.aspx)  
  
2.  設定 c2WTS ' AllowedCallers '  
  
     c2WTS 需要在設定檔**c2wtshost.exe.config**中明確列出「呼叫者」身分識別。c2WTS 不接受系統中所有經過驗證之使用者的要求，除非已設定為執行此動作。 本例中的 'caller' 是 WSS_WPG Windows 群組。 c2wtshost.exe.confi 檔案會儲存在下列位置：  
  
     **\Program Files\Windows Identity Foundation\v3.5\c2wtshost.exe.config**  
  
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
  
    2.  將 [啟動類型] 變更為 [**自動**]，然後啟動服務。  
  
4.  啟動 SharePoint 的「對 Windows Token 服務的宣告」：在 [**管理伺服器上的服務**] 頁面上，透過 SharePoint 管理中心啟動對 Windows token 服務的宣告。 您應在要執行動作的伺服器上啟動該服務。 例如您有一部 WFE 伺服器及另一部執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務的應用程式伺服器，就只需在應用程式伺服器上啟動 c2WTS。 WFE 並不需要 c2WTS。  
  
## <a name="see-also"></a>另請參閱  
 [對 Windows Token 服務的宣告（c2WTS）總覽（https://msdn.microsoft.com/library/ee517278.aspx)](https://msdn.microsoft.com/library/ee517278.aspx)   
 [Microsoft SharePoint 2010 產品的 Kerberos 驗證總覽（https://technet.microsoft.com/library/gg502594.aspx)](https://technet.microsoft.com/library/gg502594.aspx)  
  
