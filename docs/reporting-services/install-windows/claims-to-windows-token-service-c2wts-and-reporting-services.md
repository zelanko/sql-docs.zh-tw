---
title: 對 Windows Token 服務 (c2WTS) 和 Reporting Services 的宣告 | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.date: 09/15/2017
ms.openlocfilehash: 8d53445544c360250ed35c322e2fc4078559bbbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66454568"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>對 Windows Token 服務 (C2WTS) 和 Reporting Services 的宣告

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

如果您想要在 [SQL Server Reporting Services 報表檢視器 Web 組件](../report-server-sharepoint/deploy-report-viewer-web-part.md)中檢視原生模式報表，SharePoint 需要對 Windows Token 服務 (C2WTS) 宣告。

如果要針對 SharePoint 伺服器陣列以外的資料來源使用 Windows 驗證，C2WTS 也需要 SQL Server Reporting Services SharePoint 模式。 即使資料來源位於共用服務所在的同一部電腦上，也必須使用 C2WTS。 但此情況無須使用限制委派。

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。

## <a name="report-viewer-native-mode-web-part-configuration"></a>報表檢視器 (原生模式) Web 組件設定

報表檢視器 Web 組件可用於在 SharePoint 網站中，內嵌 SQL Server Reporting Services 原生模式報表。 SharePoint 2013 和 SharePoint 2016 提供此 Web 組件。 SharePoint 2013 和 SharePoint 2016 都使用宣告驗證。 因此，除了必須正確地設定 C2WTS，還必須為 Kerberos 驗證設定 Reporting Services，才能正確地轉譯報表。

1. 您可以指定 SSRS 服務帳戶、設定 SPN，以及更新 rsreportserver.config 檔案，以使用 RSWindowsNegotiate 驗證類型，為 Kerberos 驗證設定您的 Reporting Services (原生模式) 執行個體。 [為報表伺服器註冊服務主體名稱 (SPN)](https://docs.microsoft.com/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server)

2. 遵循[設定 c2WTS 的必要步驟](https://docs.microsoft.com/sql/reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services?view=sql-server-2017#steps-needed-to-configure-c2wts)中的步驟
 

## <a name="sharepoint-mode-integration"></a>SharePoint 模式整合

**本節只適用於 SQL Server 2016 Reporting Services 及更早版本。**

如果要針對 SharePoint 伺服器陣列以外的資料來源使用 Windows 驗證，SQL Server Reporting Services SharePoint 模式需要 SharePoint 對 Windows Token 服務宣告 (c2WTS)。 使用者若是使用 Windows 驗證來存取資料來源也是如此，因為 Web 前端 (WFE) 與 Reporting Services 共用服務之間的通訊皆會使用宣告驗證。

## <a name="steps-needed-to-configure-c2wts"></a>設定 c2WTS 的必要步驟

C2WTS 建立的權杖只能與限制委派 (僅限於特定服務) 及設定選項 [使用任何驗證通訊協定] (通訊協定轉換) 搭配使用。

如果您的環境會使用 Kerberos 限制委派，則 SharePoint Server 服務及外部資料來源必須位於相同的 Windows 網域。 相依於 Windows Token 服務之宣告 (c2WTS) 的任何服務，都必須使用 Kerberos **限制** 委派，才能讓 c2WTS 使用 Kerberos 通訊協定轉換將宣告轉譯成 Windows 認證。 這些需求對於所有 SharePoint Shared 服務都是如此。 如需詳細資訊，請參閱 [規劃 SharePoint 2013 的 Kerberos 驗證](https://technet.microsoft.com/library/ee806870.aspx)。  

1. 設定 C2WTS 服務網域帳戶。 

    **最佳做法：C2WTS 應以自己的網域識別身分執行。**

    * 建立 Active Directory 帳戶，並在 SharePoint 伺服器中，將此帳戶註冊為受控帳戶。 若要深入了解受控帳戶，請參閱 [Managed Accounts in Sharepoint](https://blog.wbaer.net/2010/04/11/managed-accounts-in-sharepoint-2010/) (Sharepoint 中的受控帳戶)
   
    * 將 C2WTS 服務設定為必須透過 SharePoint 管理中心 > 安全性 > 設定服務帳戶 > Windows 服務 - 對 Windows Token 服務宣告，才能使用受控帳戶

    將 C2WTS 服務帳戶新增到要使用 C2WTS 之每部伺服器上的本機系統管理員群組。 在**報表檢視器 Web 組件**，這會是 Web 前端 (WFE) 伺服器。 在 **SharePoint 整合模式**，這會是 Reporting Services 服務執行所在的應用程式伺服器。
    * 在本機原則 > 使用者權限指派下的本機安全性原則中，授與 C2WTS 帳戶下列權限：
        * 作為作業系統的一部分
        * 在驗證後模擬用戶端
        * 登入為服務

    
2. 設定 C2WTS 服務帳戶的委派。

    帳戶需要具有通訊協定轉換的限制委派，以及要委派給所需通訊服務 (如 SQL Server 資料庫引擎、SQL Server Analysis Services) 的權限。 若要設定委派，您可以使用 [Active Directory 使用者和電腦] 嵌入式管理單元，且需要成為網域的系統管理員。

    > [!IMPORTANT]
    > 在 [委派] 索引標籤上，您為 C2WTS 服務帳戶所設定的設定都需要符合 未來使用的主要服務帳戶。 在**報表檢視器 Web 組件**，這會是 SharePoint Web 應用程式的服務帳戶。 在 **SharePoint 整合模式**，這會是 Reporting Services 的服務帳戶。
    >
    > 例如，如果您允許將 C2WTS 服務帳戶委派給 SQL Service，則需要對 SharePoint 整合模式的 Reporting Services 服務帳戶執行相同的動作。

    * 以滑鼠右鍵按一下各服務帳戶，以開啟屬性對話方塊。 按一下對話方塊中的 [委派]  索引標籤。

        僅當物件指派有服務主體名稱 (SPN) 時，才會顯示 [委派] 索引標籤。 C2WTS 不需要 C2WTS 帳戶的 SPN，但若無 SPN，即不會顯示 [委派]  索引標籤。 另一種設定限制委派的方法是使用 **ADSIEdit**這類的公用程式。

    * 以下是 [委派] 索引標籤上的主要組態選項：

        * 選取 [信任這個使用者，但只委派指定的服務] 
        * 選取 [使用任何驗證通訊協定] 

    * 選取 [加入]  ，加入要委派的目標服務。

    * 選取 [使用者或電腦...&#42;]  ，然後輸入裝載服務的帳戶。 例如，如果使用名為 *sqlservice* 的帳戶來執行 SQL Server，請輸入 `sqlservice`。 
      對於**報表檢視器 Web 組件**，這會是 Reporting Services (原生模式) 執行個體的服務帳戶。

    * 選取服務清單。 這會顯示適用於該帳戶的 SPN。 如果您看不到針對該帳戶所列出的服務，則它可能遺失或放置在不同的帳戶上。 您可以使用 SetSPN 公用程式來調整 SPN。 在**報表檢視器 Web 組件**的[報表檢視器 Web 組件設定](https://docs.microsoft.com/sql/reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services?view=sql-server-2017#report-viewer-native-mode-web-part-configuration)中，會顯示 HTTP SPN 設定。

    * 選取 [確定] 以離開對話方塊。

3. 設定 C2WTS *AllowedCallers*。

    **C2WTShost.exe.config** 設定檔必須明確列出 C2WTS 的 'callers' 識別。除非兩者設定一致，否則 C2WTS 將不接受系統中所有經過驗證之使用者的要求。 本例中的 'caller' 是 WSS_WPG Windows 群組。 C2WTShost.exe.confi 檔案儲存在下列位置：

    在 SharePoint 管理中心內變更 C2WTS 服務的服務帳戶，就會將該帳戶加入 WSS_WPG 群組中。

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

4. 從 SharePoint 管理中心的 Manage Services on Server  (伺服器上的受控服務 頁面，啟動對 Windows Token 服務的宣告 (若已啟動，請先停止再啟動)。 您應在要執行動作的伺服器上啟動該服務。 例如您有一部 WFE 伺服器及另一部執行 SQL Server Reporting Services 共用服務的應用程式伺服器，就只需在應用程式伺服器上啟動 C2WTS。 如果在執行的是報表檢視器 Web 組件，WFE 伺服器上只需要 C2WTS。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
