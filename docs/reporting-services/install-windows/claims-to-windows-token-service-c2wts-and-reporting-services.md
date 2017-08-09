---
title: "對 Windows Token Service (c2WTS) 和 Reporting Services 的宣告 |Microsoft 文件"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2ab5f4b5d2774d9dc944ad17bb55063388b70a6d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>對 Windows Token 服務 (c2WTS) 和 Reporting Services 的宣告

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../../includes/ssrs-appliesto-sql2016-xpreview.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  如果要針對 SharePoint 伺服器陣列以外的資料來源使用 Windows 驗證， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式需要 SharePoint 對 Windows Token 服務的宣告 (c2WTS)。 使用者若是使用 Windows 驗證來存取資料來源也是如此，因為 Web 前端 (WFE) 與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務之間的通訊皆會使用宣告驗證。  
  
 即使資料來源位於共用服務所在的同一部電腦上，也必須使用 c2WTS。 但此情況無須使用限制委派。  
  
 c2WTS 所建立的 Token 只可與限制委派 (僅限特定服務使用) 及組態選項 [使用任何驗證通訊協定] 並用。 如前文所述，資料來源與共用服務若是位在同一部電腦上，即無須使用限制委派。  
  
 如果您的環境會使用 Kerberos 限制委派，則 SharePoint Server 服務及外部資料來源必須位於相同的 Windows 網域。 相依於 Windows Token 服務之宣告 (c2WTS) 的任何服務，都必須使用 Kerberos **限制** 委派，才能讓 c2WTS 使用 Kerberos 通訊協定轉換將宣告轉譯成 Windows 認證。 這些需求對於所有 SharePoint Shared 服務都是如此。 如需詳細資訊，請參閱 [規劃 SharePoint 2013 的 Kerberos 驗證](http://technet.microsoft.com/library/ee806870.aspx)。  
  
 本主題中會概述此程序。

## <a name="prerequisites"></a>必要條件

> [!NOTE]
>  注意：在某些伺服器陣列拓撲中，部分組態步驟可能會有所變更或無法使用。 例如單一伺服器安裝並不支援 Windows Identity Foundation c2WTS 服務，因此即無法在此伺服器陣列組態使用對 Windows Token 委派的宣告。

> [!IMPORTANT]
> 如果您使用 Power View 對 Power Pivot 活頁簿進行作業，則需要進行 [Office Online Server 概觀](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx)的其他組態。 如需詳細資訊，請參閱下列白皮書。 
>
> - [在 SharePoint 2016 中部署 SQL Server 2016 PowerPivot 和 Power View](../../analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016.md)
> 
> - [在多層 SharePoint 2016 伺服器陣列中部署 SQL Server 2016 PowerPivot 和 Power View](../../analysis-services/instances/install-windows/deploy-powerpivot-and-power-view-multi-tier-sharepoint-2016-farm.md)
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>設定 c2WTS 所需的基本步驟  
  
1.  設定 c2WTS 服務帳戶。 在每部執行 c2WTS 的應用程式伺服器的本機 Administrators 群組中加入服務帳戶。 此外，確認帳戶具有下列本機安全性原則權限︰  
  
    -   作為作業系統的一部分  
  
    -   在驗證後模擬用戶端  
  
    -   登入為服務  
  
2.  設定 c2WTS 服務帳戶的委派。 帳戶需要具有通訊協定轉換的限制委派，以及要委派給所需通訊服務 (如 SQL Server 引擎、SQL Server Analysis Services) 的權限。 若要設定委派，您可以使用 [Active Directory 使用者和電腦] 嵌入式管理單元。  

    > [!IMPORTANT]
    > 在 [委派] 索引標籤上，您為 C2WTS 服務帳戶所設定的設定都需要符合 Reporting Services 服務帳戶。 例如，如果您允許將 C2WTS 服務帳戶委派給 SQL Service，則需要對 Reporting Services 服務帳戶執行相同的動作。
  
    1.  以滑鼠右鍵按一下各服務帳戶，以開啟屬性對話方塊。 按一下對話方塊中的 [委派] 索引標籤。  
  
        > [!NOTE]  
        >  注意：物件必須獲指派服務主體名稱 (SPN)，才會顯示 [委派] 索引標籤。 c2WTS 不需要 c2WTS 帳戶的 SPN，但若無 SPN，則不會顯示 [委派] 索引標籤。 另一種設定限制委派的方法是使用 **ADSIEdit** 這類的公用程式。  
  
    2.  以下是 [委派] 索引標籤上的主要組態選項：  
  
        -   選取 [信任這個使用者，但只委派指定的服務]。  
  
        -   選取 [使用任何驗證通訊協定]。  

    3. 選取 [加入]，加入要委派的目標服務。
    
    4. 選取**使用者或電腦...*** 並輸入裝載服務的帳戶。 例如，如果名為的帳戶下執行 SQL Server *sqlservice*，輸入`sqlservice`。
    
    5. 選取服務清單。 這會顯示適用於該帳戶的 SPN。 如果您看不到針對該帳戶所列出的服務，則它可能遺失或放置在不同的帳戶上。 您可以使用 SetSPN 公用程式來調整 SPN。
    
    6. 選取 [確定] 以離開對話方塊。
  
3.  設定 c2WTS ‘AllowedCallers’  
  
     c2WTS 的 'callers' 識別必須明確列出於 **c2WTShost.exe.config**組態中。 除非兩者設定一致，否則 c2WTS 將不接受系統中所有經過驗證之使用者的要求。 在此情況下，'caller' 將會是 WSS_WPG Windows 群組。 c2WTShost.exe.confi 檔案會儲存在下列位置：  
     
     > [!NOTE]
     > 在 SharePoint 管理中心內變更 C2WTS 服務的服務帳戶，就會將該帳戶加入 WSS_WPG 群組中。
  
     **\Program Files\Windows Identity Foundation\v3.5\c2WTShost.exe.config**  
  
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
4.  啟動「SharePoint 對 Windows Token 服務的宣告」：從 [管理伺服器上的服務] 頁面上的 SharePoint 管理中心，啟動對 Windows Token 服務的宣告。 您應在要執行動作的伺服器上啟動該服務。 例如您有一部 WFE 伺服器及另一部執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務的應用程式伺服器，就只需在應用程式伺服器上啟動 c2WTS。 WFE 並不需要 c2WTS。

## <a name="next-steps"></a>後續的步驟

[對 Windows Token 服務的宣告 (c2WTS) 概觀](http://msdn.microsoft.com/library/ee517278.aspx)   
[規劃 SharePoint 2013 的 Kerberos 驗證](http://technet.microsoft.com/library/ee806870.aspx)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
