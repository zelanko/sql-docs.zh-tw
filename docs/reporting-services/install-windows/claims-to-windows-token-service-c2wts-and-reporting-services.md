---
title: "對 Windows Token Service (c2WTS) 和 Reporting Services 的宣告 |Microsoft 文件"
ms.custom: The Claims to Windows Token Service (C2WTS) is used by SharePoint and needs to be configured for Kerberos constrained delegation to work with SQL Server Reporting Services properly.
ms.date: 09/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: 8a478bba3cde66967594d5ef02f867de5b33edd7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/15/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>對 Windows Token 服務 (C2WTS) 和 Reporting Services 的宣告

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

如果您想要檢視中的原生模式報表，則需要 SharePoint 對 Windows Token Service 宣告 (C2WTS) [SQL Server Reporting Services 報表檢視器 web 組件](../report-server-sharepoint/deploy-report-viewer-web-part.md)。

如果您想要針對 SharePoint 伺服器陣列以外的資料來源使用 Windows 驗證，也是 SQL Server Reporting Services SharePoint 模式需要 C2WTS。 即使資料來源位於共用服務所在的同一部電腦上，也必須使用 C2WTS。 但此情況無須使用限制委派。

> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

## <a name="report-viewer-web-part-configuration"></a>報表檢視器 web 組件組態

報表檢視器 web 組件可用於將 SharePoint 網站中的 SQL Server Reporting Services 原生模式報表內嵌到。 此 web 組件適用於 SharePoint 2013 和 SharePoint 2016。 SharePoint 2013 和 SharePoint 2016 使用的宣告驗證。 SQL Server Reporting Services （原生模式） 預設會使用 Windows 驗證。 如此一來，C2WTS 必須正確設定。 若要正確轉譯的報表。

## <a name="sharepoint-mode-integaration"></a>SharePoint 模式 integaration

**本節只適用於 SQL Server 2016 Reporting Services 及更早版本。**

如果您想要針對 SharePoint 伺服器陣列以外的資料來源使用 Windows 驗證與 SQL Server Reporting Services SharePoint 模式需要 SharePoint 對 Windows Token Service 宣告 (C2WTS)。 這是 true，即使使用者存取資料來源使用 Windows 驗證，因為之間的通訊 web 前端 (WFE) 和 Reporting Services 共用的服務一律為宣告驗證。

## <a name="steps-needed-to-configure-c2wts"></a>設定 c2WTS 所需的步驟

C2WTS 所建立的 Token 只可與限制委派 (僅限特定服務使用) 及組態選項 [使用任何驗證通訊協定] 並用。 如前文所述，資料來源與共用服務若是位在同一部電腦上，即無須使用限制委派。

如果您的環境會使用 Kerberos 限制委派，則 SharePoint Server 服務及外部資料來源必須位於相同的 Windows 網域。 相依於 Windows Token 服務之宣告 (c2WTS) 的任何服務，都必須使用 Kerberos **限制** 委派，才能讓 c2WTS 使用 Kerberos 通訊協定轉換將宣告轉譯成 Windows 認證。 這些需求對於所有 SharePoint Shared 服務都是如此。 如需詳細資訊，請參閱 [規劃 SharePoint 2013 的 Kerberos 驗證](http://technet.microsoft.com/library/ee806870.aspx)。  

1. 設定 C2WTS 服務帳戶。 將服務帳戶加入至本機 Administrators 群組，將用於 C2WTS 的每部伺服器上。

    如**報表檢視器 web 組件**，這是 Web 前端 (WFE) 伺服器。 如**SharePoint 整合的模式**，這會是 Reporting Services 服務執行所在的應用程式伺服器。

2. 設定 C2WTS 服務帳戶的委派。

    帳戶必須具有通訊協定轉換和權限委派給所 (也就是 SQL Server Database Engine，SQL Server Analysis Services) 與通訊之服務的限制委派。 若要設定委派，您可以使用 [Active Directory 使用者和電腦] 嵌入式管理單元並將需要以網域系統管理員。

    > [!IMPORTANT]
    > 設定 C2WTS 服務帳戶上設定 [委派] 索引標籤中，必須符合所使用的主要的服務帳戶。 如**報表檢視器 web 組件**，這會是 SharePoint web 應用程式的服務帳戶。 如**SharePoint 整合的模式**，這將是 Reporting Services 服務帳戶。
    >
    > 例如，如果您允許將 C2WTS 服務帳戶委派給 SQL 服務，您需要執行 SharePoint 整合模式的 Reporting Services 服務帳戶相同的動作。

    * 以滑鼠右鍵按一下各服務帳戶，以開啟屬性對話方塊。 在對話方塊中按一下**委派** 索引標籤。

        [委派] 索引標籤才看得見，如果物件具有服務主體名稱 (SPN) 指派給它。 C2WTS 不需要 C2WTS 帳戶的 SPN，但無 SPN，**委派** 索引標籤就不會顯示。 另一種設定限制委派的方法是使用 **ADSIEdit**這類的公用程式。

    * 以下是 [委派] 索引標籤上的主要組態選項：

        * 選取**信任這個使用者委派指定的服務**
        * 選取**使用任何驗證通訊協定**

    * 選取 [加入]，加入要委派的目標服務。

    * 選取**使用者或電腦...*** 並輸入裝載服務的帳戶。 例如，如果名為的帳戶下執行 SQL Server *sqlservice*，輸入`sqlservice`。 

    * 選取服務清單。 這會顯示適用於該帳戶的 SPN。 如果您看不到針對該帳戶所列出的服務，則它可能遺失或放置在不同的帳戶上。 您可以使用 SetSPN 公用程式來調整 SPN。

    * 選取 [確定] 以離開對話方塊。

3. 設定 C2WTS *AllowedCallers*。

    C2WTS 的 'callers' 識別必須明確列在組態檔中， **C2WTShost.exe.config**。除非兩者設定一致，否則 C2WTS 將不接受系統中所有經過驗證之使用者的要求。 在此情況下，'caller' 將是 WSS_WPG Windows 群組。 C2WTShost.exe.confi 檔案會儲存在下列位置：

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

4. 啟動對 Windows Token Service，透過 SharePoint 管理中心內的宣告上**管理伺服器上的服務**頁面。 您應在要執行動作的伺服器上啟動該服務。 例如，如果您有的伺服器，也就是一部 WFE 另一部伺服器及應用程式伺服器具有 SQL Server Reporting Services 共用的服務執行，您只需要啟動 C2WTS 的應用程式伺服器上。 如果您正在執行的報表檢視器 web 組件，C2WTS 時才會需要在 WFE 伺服器上。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
