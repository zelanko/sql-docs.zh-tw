---
title: 對 Windows Token 服務 (c2WTS) 和 Reporting Services 的宣告 | Microsoft Docs
ms.custom: ''
ms.date: 09/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9997cf254a6d7e2f01f846e76ae82d20db748e84
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38030976"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>對 Windows Token 服務 (C2WTS) 和 Reporting Services 的宣告

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

如果您想要在 [SQL Server Reporting Services 報表檢視器 Web 組件](../report-server-sharepoint/deploy-report-viewer-web-part.md)中檢視原生模式報表，SharePoint 需要對 Windows Token 服務 (C2WTS) 宣告。

如果要針對 SharePoint 伺服器陣列以外的資料來源使用 Windows 驗證，C2WTS 也需要 SQL Server Reporting Services SharePoint 模式。 即使資料來源位於共用服務所在的同一部電腦上，也必須使用 C2WTS。 但此情況無須使用限制委派。

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。

## <a name="report-viewer-web-part-configuration"></a>報表檢視器 Web 組件設定

報表檢視器 Web 組件可用於在 SharePoint 網站中，內嵌 SQL Server Reporting Services 原生模式報表。 SharePoint 2013 和 SharePoint 2016 提供此 Web 組件。 SharePoint 2013 和 SharePoint 2016 都使用宣告驗證。 SQL Server Reporting Services (原生模式) 預設使用 Windows 驗證。 結果是，您需要正確設定 C2WTS，才能正確轉譯報表。

## <a name="sharepoint-mode-integaration"></a>SharePoint 模式整合

**本節只適用於 SQL Server 2016 Reporting Services 及更早版本。**

如果要針對 SharePoint 伺服器陣列以外的資料來源使用 Windows 驗證，SQL Server Reporting Services SharePoint 模式需要 SharePoint 對 Windows Token 服務宣告 (c2WTS)。 使用者若是使用 Windows 驗證來存取資料來源也是如此，因為 Web 前端 (WFE) 與 Reporting Services 共用服務之間的通訊皆會使用宣告驗證。

## <a name="steps-needed-to-configure-c2wts"></a>設定 c2WTS 的必要步驟

C2WTS 所建立的 Token 只可與限制委派 (僅限特定服務使用) 及組態選項 [使用任何驗證通訊協定] 並用。 如前文所述，資料來源與共用服務若是位在同一部電腦上，即無須使用限制委派。

如果您的環境會使用 Kerberos 限制委派，則 SharePoint Server 服務及外部資料來源必須位於相同的 Windows 網域。 相依於 Windows Token 服務之宣告 (c2WTS) 的任何服務，都必須使用 Kerberos **限制** 委派，才能讓 c2WTS 使用 Kerberos 通訊協定轉換將宣告轉譯成 Windows 認證。 這些需求對於所有 SharePoint Shared 服務都是如此。 如需詳細資訊，請參閱 [規劃 SharePoint 2013 的 Kerberos 驗證](http://technet.microsoft.com/library/ee806870.aspx)。  

1. 設定 C2WTS 服務帳戶。 在每部使用 C2WTS 之伺服器的本機 Administrators 群組中新增服務帳戶。

    在**報表檢視器 Web 組件**，這會是 Web 前端 (WFE) 伺服器。 在 **SharePoint 整合模式**，這會是 Reporting Services 服務執行所在的應用程式伺服器。

2. 設定 C2WTS 服務帳戶的委派。

    帳戶需要具有通訊協定轉換的限制委派，以及要委派給所需通訊服務 (如 SQL Server 資料庫引擎、SQL Server Analysis Services) 的權限。 若要設定委派，您可以使用 [Active Directory 使用者和電腦] 嵌入式管理單元，且需要成為網域的系統管理員。

    > [!IMPORTANT]
    > 在 [委派] 索引標籤上，您為 C2WTS 服務帳戶所設定的設定都需要符合 未來使用的主要服務帳戶。 在**報表檢視器 Web 組件**，這會是 SharePoint Web 應用程式的服務帳戶。 在 **SharePoint 整合模式**，這會是 Reporting Services 的服務帳戶。
    >
    > 例如，如果您允許將 C2WTS 服務帳戶委派給 SQL Service，則需要對 SharePoint 整合模式的 Reporting Services 服務帳戶執行相同的動作。

    * 以滑鼠右鍵按一下各服務帳戶，以開啟屬性對話方塊。 按一下對話方塊中的 [委派] 索引標籤。

        物件必須獲指派服務主體名稱 (SPN)，才會顯示 [委派] 索引標籤。 C2WTS 不需要 C2WTS 帳戶的 SPN，但若無 SPN，即不會顯示 [委派] 索引標籤。 另一種設定限制委派的方法是使用 **ADSIEdit**這類的公用程式。

    * 以下是 [委派] 索引標籤上的主要組態選項：

        * 選取 [信任這個使用者，但只委派指定的服務]
        * 選取 [使用任何驗證通訊協定]

    * 選取 [加入]，加入要委派的目標服務。

    * 選取 [使用者或電腦...]*，然後輸入裝載服務的帳戶。 例如，如果使用名為 *sqlservice* 的帳戶來執行 SQL Server，請輸入 `sqlservice`。 

    * 選取服務清單。 這會顯示適用於該帳戶的 SPN。 如果您看不到針對該帳戶所列出的服務，則它可能遺失或放置在不同的帳戶上。 您可以使用 SetSPN 公用程式來調整 SPN。

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

4. 從 [管理伺服器上的服務] 上的 SharePoint 管理中心啟動對 Windows Token 服務的宣告。 您應在要執行動作的伺服器上啟動該服務。 例如您有一部 WFE 伺服器及另一部執行 SQL Server Reporting Services 共用服務的應用程式伺服器，就只需在應用程式伺服器上啟動 C2WTS。 如果在執行的是報表檢視器 Web 組件，WFE 伺服器上只需要 C2WTS。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
