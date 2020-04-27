---
title: 設定 PowerPivot 資料重新整理的預存認證（PowerPivot for SharePoint） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 987eff0f-bcfe-4bbd-81e0-9aca993a2a75
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23f35c8998b204182f25f85f8f7694fb60d042b4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087463"
---
# <a name="configure-stored-credentials-for-powerpivot-data-refresh-powerpivot-for-sharepoint"></a>設定 PowerPivot 資料重新整理的預存認證 (PowerPivot for SharePoint)
  只要您在 Secure Store Service 中建立目標應用程式來儲存想要使用的認證，PowerPivot 資料重新整理作業就可以在任何 Windows 使用者帳戶之下執行。 同樣地，若想要提供的資料庫登入不同於最初用於匯入 PowerPivot for Excel 資料的登入，可以將這些認證對應至 Secure Store Service 目標應用程式，然後在資料重新整理排程中指定該目標應用程式。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
 當您依照本主題的指示進行之後，即可使用 PowerPivot 資料重新整理排程頁面中的認證選項，如下所示：  
  
 ![SSAS_PowerPivotDataRefreshCreds_Stored](media/ssas-powerpivotdatarefreshcreds-stored.gif "SSAS_PowerPivotDataRefreshCreds_Stored")  
  
 本主題說明如何設定 SharePoint 2010 伺服器陣列中用於 PowerPivot 資料重新整理的使用者名稱和密碼。 您必須先啟用 Secure Store Service 並產生主要金鑰，然後才能使用這些步驟。 如需詳細資訊，請參閱[PowerPivot 資料重新整理與 SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
 本主題包含下列幾節：  
  
 [針對資料重新整理設定任何 Windows 帳戶](#configAny)  
  
 [針對存取外部或協力廠商資料來源設定預先定義的帳戶](#config3rd)  
  
 如果您在設定或使用資料重新整理時遇到問題，請參閱 TechNet wiki 上的[疑難排解 PowerPivot 資料](https://go.microsoft.com/fwlink/?LinkID=223279)重新整理頁面，以取得可能的解決方案。  
  
##  <a name="configure-any-windows-account-for-data-refresh"></a><a name="configAny"></a>設定任何 Windows 帳戶以進行資料重新整理  
 當 SharePoint 使用者定義資料重新整理排程時，該使用者必須指定用來執行資料重新整理的使用者識別。 您可以選擇選取 PowerPivot 無人看管的資料重新整理帳戶，也可輸入使用者的 Windows 網域使用者帳戶，或是輸入其他可以適用於資料重新整理的 Windows 使用者帳戶。 本節中的步驟適用於最後一個選項：指定某些其他 Windows 帳戶。  
  
 如果您想要使用 PowerPivot 無人看管的資料重新整理帳戶 (適用於 SharePoint 的所有 PowerPivot 使用者) 或活頁簿擁有者之認證的替代方案，可能會選擇這種方式。 例如，您可能會想要將一系列資料重新整理帳戶提供給不同的工作群組，以便協助您在組織層級中追蹤和管理資料重新整理活動。  
  
> [!IMPORTANT]  
>  使用此目標應用程式 (及所儲存之認證) 的人員和應用程式都必須列為應用程式的成員。 您必須加入將使用目標應用程式之每個 PowerPivot 服務應用程式的識別、您的 Windows 帳戶，以及將在其資料重新整理排程中指定此目標應用程式之人員的群組或使用者帳戶。 當您建立目標應用程式時，可以指定上述所有帳戶。 如果您不知道將需要存取此應用程式的所有使用者和群組帳戶，您可以在建立目標應用程式之後再加入它們。  
  
 設定資料重新整理的預存認證共有 4 個部分：  
  
-   建立用以儲存認證的目標應用程式。  
  
-   授與「參與」權限給帳戶。  
  
-   授與帳戶讀取權限，以便在資料重新整理期間存取外部資料來源。  
  
-   驗證當您在資料重新整理排程中指定此目標應用程式時，資料重新整理可否運作。  
  
### <a name="step-1-create-a-target-application"></a>步驟 1：建立目標應用程式  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 [**管理服務應用程式**]。  
  
2.  按一下 [ **Secure Store Service**]。  
  
3.  在 [管理目標應用程式] 中，按一下 [**新增**]。  
  
4.  在 [目標應用程式識別碼] 中，輸入文字字串。 此字串必須是唯一的，但也應該容易記憶。 每當使用者想要使用儲存在此應用程式中的認證時，將在資料重新整理排程頁面中輸入這個字串。  
  
5.  在 [顯示名稱] 中，輸入描述性名稱。 此名稱僅用於顯示用途， 而不是在資料重新整理排程中用來指定目標應用程式。  
  
6.  在 [連絡人電子郵件] 中，輸入您的電子郵件地址。  
  
7.  在 [目標應用程式類型] 中，選取 [**群組**]。  
  
    > [!IMPORTANT]  
    >  您必須選擇群組帳戶類型，如此才能夠指定存取認證所需的所有使用者與服務帳戶。 PowerPivot 系統服務會檢查各項要求的要求者是否為目標應用程式的成員。  
  
8.  略過目標應用程式的網頁 URL。 PowerPivot 資料重新整理不會使用它。  
  
9. 按 [下一步]  。  
  
10. 在 [**指定 Secure Store 目標應用程式的認證欄位**] 頁面中，接受預設值。 欄位名稱和類型應該是 Windows 使用者名稱和 Windows 密碼。  
  
11. 按 [下一步]。  
  
12. 在 [目標應用程式管理員] 中，指定 SharePoint 使用者的 Windows 網域使用者帳戶，而該使用者必須具備目標應用程式的系統管理存取權 (例如新增或移除 [成員] 清單中之帳戶的能力)。  
  
13. 在 [成員] 中，加入下列使用者和群組帳戶：  
  
    1.  將您的 Windows 使用者帳戶加入至 [成員] 清單中，做為建立應用程式的人員。  
  
    2.  加入 PowerPivot 服務應用程式的應用程式集區識別，讓它能夠在資料重新整理排程為執行時擷取認證。 若要查看應用程式集區身分識別，請移至 [**管理服務應用程式**]，按一下名稱旁邊的空白處（這會選取資料列）來選取 PowerPivot 服務應用程式，然後按一下 [**屬性**]。 出現在此頁面的安全性帳戶就是要當做目標應用程式成員加入的帳戶。  
  
    3.  加入將在資料重新整理排程中輸入此目標應用程式的 Windows 使用者和群組帳戶。  
  
14. 按一下 [確定]  。  
  
15. 選取您剛才建立的目標應用程式，按一下向下箭號，然後選取 [**設定認證]。**  
  
16. 請注意，[認證擁有者] 中的認證擁有者清單為唯讀。 凡具有認證擁有權的帳戶，皆是目標應用程式的成員。 若要新增或移除認證擁有者，必須先在目標應用程式的成員清單中新增或移除帳戶。  
  
     在 [Windows 使用者名稱] 及 [Windows 密碼] 中，輸入要用於執行資料重新整理之 Windows 使用者帳戶的認證。  
  
17. 按一下 [確定]  。  
  
###  <a name="step-2-grant-contribute-permissions-to-the-account"></a><a name="bkmk_grant"></a>步驟2：授與帳戶的「參與」許可權  
 帳戶必須先獲指派其所應用之任何 PowerPivot 活頁簿的「參與」權限，您才可使用預存認證。 您需要這個權限等級才能從文件庫開啟活頁簿，然後在重新整理資料之後，將其存回文件庫。  
  
 指派權限是由網站集合管理員所執行的步驟。 您可以在根網站集合或根網站集合底下的任何層級 (包括個別文件和項目) 指派 SharePoint 權限。 設定權限的方式將隨著細緻程度而有所不同。 下列步驟示範授與權限的其中一個方法。  
  
1.  在 SharePoint 網站的 [網站動作] 中，按一下 [**網站許可權**]。  
  
2.  按一下 [授與權限]****。  
  
3.  在 [選取使用者] 中，輸入您在目標應用程式中所指定之 Windows 網域使用者帳戶的名稱。  
  
4.  在 [授與許可權] 中，選取 **[直接授與使用者許可權**]。  
  
5.  選取 [**參與**]，然後按一下 **[確定]**。  
  
###  <a name="step-3-grant-read-permissions-to-access-external-data-sources-used-in-data-refresh"></a><a name="bkmk_dbread"></a>步驟3：授與讀取權限以存取資料重新整理時所使用的外部資料源  
 當資料匯入至 PowerPivot 活頁簿時，外部資料連接通常是以信任連接或是以使用目前使用者身分連接至資料來源的模擬連接為基礎。 這些類型的連接只能在目前使用者有讀取所匯入之資料的權限時使用。  
  
 在資料重新整理案例中，用來匯入資料的相同連接字串現在會重複使用來重新整理資料。 假使連接字串採行目前使用者 (例如字串中包含 Integrated_Security=SSPI) 的作法，PowerPivot 系統服務在傳遞目前使用者時，即會將目標應用程式中所指定的使用者識別視為目前使用者。 帳戶必須具備外部資料來源的讀取權限，此連接才會成功。  
  
 因此，您必須將資料重新整理期間所要使用之所有外部資料來源的唯讀權限授與帳戶。  
  
 如果您是組織中使用的資料來源的系統管理員，可以建立登入並指定所需的權限。 否則，您必須連絡資料擁有者並提供帳戶資訊。 請務必指定對應至目標應用程式的 Windows 網域使用者帳戶。 這是您在本主題的「步驟1：建立目標應用程式」中指定的帳號。  
  
###  <a name="step-4-verify-account-availability-in-data-refresh-configuration-pages"></a><a name="bkmk_verify"></a>步驟4：確認資料重新整理設定頁面中的帳戶可用性  
  
1.  為包含 PowerPivot 資料之已發行的活頁簿，開啟資料重新整理組態頁面。 如需如何開啟頁面的指示，請參閱[排程資料重新整理 &#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)。  
  
2.  在 [資料重新整理設定] 頁面中，確認已啟用 [**使用儲存在 Secure Store Service （SSS）中的認證來登入資料來源]** 選項，然後輸入目標應用程式的名稱。  
  
3.  選取 [**同時**儘快重新整理] 核取方塊，然後按一下 **[確定]**。  
  
4.  在包含活頁簿的文件庫中，選取活頁簿，按一下向右顯示的向下箭號，然後選取 [**管理 PowerPivot 資料**重新整理]。 若資料重新整理作業傳回的資料量十分龐大，可能需要等候數分鐘的時間。  
  
 如果發生錯誤，您可以按一下 [資料重新整理記錄] 頁面中的 [設定**排程**]，以嘗試不同的認證。 您也可能需要檢查原始活頁簿中的資料來源連接資訊，以查看資料重新整理期間所使用的連接字串。 連接字串所提供的伺服器位置與資料庫資訊，可讓您用於疑難排解問題。  
  
 如需有關疑難排解的詳細資訊，請參閱 TechNet Wiki 上的[疑難排解 PowerPivot 資料](https://go.microsoft.com/fwlink/p/?LinkID=223279)重新整理。  
  
##  <a name="configure-a-predefined-account-for-accessing-external-or-third-party-data-sources"></a><a name="config3rd"></a>設定預先定義的帳戶來存取外部或協力廠商資料來源  
 資料庫伺服器通常會有自己的驗證方法。 如果您的 PowerPivot 活頁簿需要資料庫認證，以便在資料重新整理期間存取外部資料來源，則可以建立認證的目標應用程式識別碼，然後在排程資料重新整理頁面的 [資料來源] 區段指定目標應用程式。  
  
 只有在您想要讓使用者選擇覆寫已經內嵌在 PowerPivot 活頁簿中的資料庫認證時，才需要這個步驟。  
  
 連接字串中必須包含使用者名稱及密碼，此步驟才能運作。 請注意，在連接字串中包含認證十分罕見，因此您在使用此選項時也會有所限制。 在大多數的情況下，您若是使用資料庫驗證來連接資料來源，則連接字串中將只會包含使用者識別碼及密碼。 如需如何檢查連接字串以查看其是否包含使用者識別碼和密碼的詳細資訊，請參閱[PowerPivot Data Refresh With SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)中的「授與建立排程和存取外部資料的許可權」一節。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 [**管理服務應用程式**]。  
  
2.  按一下 [ **Secure Store Service**]。  
  
3.  在 [管理目標應用程式] 中，按一下 [**新增**]。  
  
4.  在 [目標應用程式識別碼] 中，輸入文字字串。 此字串必須是唯一的，但也應該容易記憶。 每當使用者想要使用儲存在此應用程式中的認證時，將在資料重新整理排程頁面中輸入這個字串。  
  
5.  在 [顯示名稱] 中，輸入描述性名稱。 此名稱僅用於顯示用途， 而不是在資料重新整理排程中用來指定目標應用程式。  
  
6.  在 [連絡人電子郵件] 中，輸入您的電子郵件地址。  
  
7.  在 [目標應用程式類型] 中，選取 [**群組**]。  
  
8.  略過目標應用程式的網頁 URL。 PowerPivot 資料重新整理不會使用它。  
  
9. 按 [下一步]  。  
  
10. 在 [**指定 Secure Store 目標應用程式的認證欄位**] 頁面中，只有在資料來源使用 Windows 驗證時才接受預設值。 否則，請選擇適用於資料來源的欄位類型，然後編輯欄位名稱以符合此類型。  
  
     例如，您可能在欄位名稱中指定 SQL Server 使用者名稱及 SQL Server 使用者密碼，然後選擇使用者名稱及密碼做為欄位類型。  
  
11. 按 [下一步]。  
  
12. 在 [目標應用程式管理員] 中，針對應該擁有應用程式設定管理存取權的 SharePoint 使用者指定 Windows 網域使用者帳戶。  
  
13. 在 [成員] 中，加入下列使用者和群組帳戶：  
  
    1.  將您的 Windows 使用者帳戶加入至 [成員] 清單中，做為建立應用程式的人員。  
  
    2.  加入將使用目標應用程式存取其預存認證之每個 PowerPivot 服務應用程式的應用程式集區識別。 若要查看身分識別，請移至 [**管理服務應用程式**]，按一下名稱旁邊的空白處（這會選取資料列）來選取 PowerPivot 服務應用程式，然後按一下 [**屬性**]。 出現在此頁面的安全性帳戶就是您要當做目標應用程式成員加入的帳戶。  
  
    3.  加入將在資料重新整理排程頁面之資料來源區段中輸入此目標應用程式的 Windows 使用者和群組帳戶。  
  
14. 按一下 [確定]  。  
  
15. 選取您剛才建立的目標應用程式，按一下向下箭號，然後選取 [**設定認證]。**  
  
16. 輸入要用於連接資料來源的認證 (例如 SQL Server 登入的使用者名稱及密碼)。  
  
17. 按一下 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
 [排程資料重新整理 &#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [SharePoint 2010 中的 PowerPivot 資料重新整理](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
  
