---
title: PowerPivot 資料重新整理與 SharePoint 2010 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 01b54e6f-66e5-485c-acaa-3f9aa53119c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9f042a937b1ce2a51bc6d8dbb50b8fc39c4fb78
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175627"
---
# <a name="powerpivot-data-refresh-with-sharepoint-2010"></a>SharePoint 2010 中的 PowerPivot 資料重新整理
  
  [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 資料重新整理是一項查詢外部資料來源的排程伺服器端作業，可更新儲存在內容庫中 Excel 2010 活頁簿的內嵌 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 資料。

 資料重新整理是 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 的內建功能，但您需要在 SharePoint 2010 伺服器陣列中執行特定服務和計時器工作才能使用它。 此外，通常也需要額外的管理步驟 (例如安裝資料提供者及檢查資料庫權限)，資料重新整理才會成功。

 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010

> [!NOTE]
>  
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 和 SharePoint Server 2013 Excel Services 會使用不同的架構來進行 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 資料模型的資料重新整理。 新的架構會運用 Excel Services 做為主要元件來載入 PowerPivot 資料模型。 先前的資料重新整理架構會使用並仰賴在 SharePoint 模式下執行 PowerPivot 系統服務和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的伺服器來載入資料模型。 如需詳細資訊，請參閱[PowerPivot Data Refresh With SharePoint 2013](power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md)。

 **本主題內容：**

 [步驟1：啟用 Secure Store Service 並產生主要金鑰](#bkmk_services)

 [步驟 2：關閉您不想要支援的認證選項](#bkmk_creds)

 [步驟 3：建立目標應用程式來儲存資料重新整理時所使用的認證](#bkmk_stored)

 [步驟 4：針對可擴充的資料重新整理設定伺服器](#bkmk_scale)

 [步驟 5：安裝用於匯入 PowerPivot 資料的資料提供者](#bkmk_installdp)

 [步驟 6：授與建立排程及存取外部資料來源的權限](#bkmk_accounts)

 [步驟 7：針對資料重新整理啟用活頁簿升級](#bkmk_upgradewrkbk)

 [步驟 8：驗認資料重新整理組態](#bkmk_verify)

 [針對資料重新整理修改組態設定](#bkmk_config)

 [重新排程 PowerPivot 資料重新整理計時器工作](#configTimerJob)

 [停用資料重新整理計時器工作](#bkmk_disableDR)

 在確定伺服器環境和權限已設定之後，資料重新整理已備妥可供使用。 若要使用資料重新整理，SharePoint 使用者必須建立 PowerPivot 活頁簿的排程，指定進行資料重新整理的頻率。 排程建立通常是由發行檔案至 SharePoint 的活頁簿擁有者或作者所完成。 這位人員會建立並管理他所擁有之活頁簿的資料重新整理排程。 如需詳細資訊，請參閱[排程資料重新整理 &#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)。

##  <a name="bkmk_services"></a>步驟1：啟用 Secure Store Service 並產生主要金鑰
 PowerPivot 資料重新整理功能仰賴 Secure Store Service 提供認證以供執行資料重新整理作業，以及連接至使用預存認證的外部資料來源之用。

 您若是使用 [新伺服器] 選項安裝 PowerPivot for SharePoint，即會為您設定 Secure Store Service。 除此之外的其他安裝狀況皆須建立及設定服務應用程式，並產生 Secure Store Service 的主要加密金鑰。

> [!NOTE]
>  您必須是伺服器陣列管理員才能設定 Secure Store Service，或是將 Secure Store Service 管理委派給其他使用者。 您必須是服務應用程式管理員，才能在啟用後設定或修改設定值。

1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。

2.  在 [服務應用程式] 功能區的 [建立] 中，按一下 [**新增**]。

3.  選取 [ **Secure Store Service**]。

4.  在 [**建立 Secure Store 應用程式**] 頁面中，輸入應用程式的名稱。

5.  在 [**資料庫**] 中，指定將裝載此服務應用程式之資料庫的 SQL Server 實例。 預設值是主控伺服陣列組態資料庫的 SQL Server Database Engine 執行個體。

6.  在 [**資料庫名稱**] 中，輸入服務應用程式資料庫的名稱。 預設值為 Secure_Store_Service_DB_\<guid>。 預設名稱會對應至服務應用程式的預設名稱。 如果您輸入唯一的服務應用程式名稱，請依照類似的命名慣例來命名資料庫名稱，以利同時管理它們。

7.  在 **[資料庫驗證]** 中，預設值是 Windows 驗證。 如果您選擇 [SQL 驗證]，請參考 SharePoint 管理員指南，以取得如何在伺服陣列中使用這個驗證類型的指引。

8.  在應用程式集區中，選取 [**建立新應用程式集**區]。 指定描述性名稱，將可協助其他伺服器系統管理員識別如何使用應用程式集區。

9. 選取應用程式集區的安全性帳戶。 指定受管理的帳戶，以使用網域使用者帳戶。

10. 接受其餘的預設值，然後按一下 **[確定]。** 服務應用程式將會和伺服陣列的服務應用程式清單中其他受管理的服務一起並排顯示。

11. 從清單按一下 Secure Store Service 應用程式。

12. 在 [服務應用程式] 功能區中，按一下 [**管理**]。

13. 在 [金鑰管理] 中，按一下 [**產生新金鑰**]。

14. 輸入複雜密碼，然後進行確認。 此複雜密碼將用來加入其他安全存放共用服務應用程式。

15. 按一下 [確定]  。

 可供疑難排解之用的 Store Service 作業稽核記錄必須在作業開始之前啟用。 如需如何啟用記錄的詳細資訊，請參閱[設定 Secure Store Service （SharePoint 2010）](https://go.microsoft.com/fwlink/p/?LinkID=223294)。

##  <a name="bkmk_creds"></a>步驟2：關閉您不想要支援的認證選項
 PowerPivot 資料重新整理在資料重新整理排程方面提供三種認證。 當活頁簿擁有者排程資料重新整理時，必須從中選擇一個選項，以決定執行資料重新整理作業時所要使用的帳戶。 您身為管理員，可以決定排程擁有者所能使用的認證選項。

 您至少必須提供一個選項，資料重新整理功能才能運作。

 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")

 選項1：**使用系統管理員所設定的資料**重新整理帳戶，一律會出現在排程定義頁面上，但只有在您設定自動資料重新整理帳戶時才有效。 如需如何建立帳戶的詳細資訊，請參閱[設定 PowerPivot 無人看管的資料重新整理帳戶 &#40;PowerPivot for SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)。

 選項2：**使用下列 windows 認證進行連接**：一律會顯示在頁面上，但只有當您啟用 [服務應用程式設定] 頁面中的 [**允許使用者輸入自訂的 windows 認證**] 選項時才有效。 預設會啟用此選項，但如果啟用此選項對您而言壞處多於好處，也可予以停用 (請參閱下文)。

 選項3：**使用儲存在 Secure Store Service 中的認證進行連接**，一律會顯示在頁面上，但只有在排程擁有者提供有效的目標應用程式時才適用。 管理員必須事先建立這些目標應用程式，然後將應用程式名稱提供給建立資料重新整理排程的使用者。 如需如何建立資料重新整理作業之目標應用程式的詳細資訊，請參閱[設定 PowerPivot 資料重新整理的預存認證 &#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。

 **設定認證選項2：「使用下列 Windows 使用者認證連接」**

 PowerPivot 服務應用程式所包含的認證選項可允許排程擁有者輸入任意的 Windows 使用者名稱及密碼，以執行資料重新整理作業。 此選項是排程定義頁面的第二個認證選項：

 ![SSAS_PPS_ScheduleDataRefreshCreds](media/ssas-pps-scheduledatarefreshcreds.gif "SSAS_PPS_ScheduleDataRefreshCreds")

 預設會啟用這個認證選項。 啟用此認證選項之後，PowerPivot 系統服務會在 Secure Store Service 中產生目標應用程式，以儲存排程擁有者所輸入的使用者名稱及密碼。 產生的目標應用程式會使用下列命名慣例來建立\<： PowerPivotDataRefresh_ guid>。 每一組 Windows 認證各會建立一個目標應用程式。 假使 PowerPivot 系統服務已有目標應用程式可以用於儲存排程定義者所輸入的使用者名稱及密碼，PowerPivot 系統服務將會使用該目標應用程式，而不會建立新的目標應用程式。

 此認證選項的主要優點在於簡單易用。 因為它會為您建立目標應用程式，所以不太需要額外的工夫。 除此之外，使用排程擁有者 (極有可能是活頁簿的建立者) 的認證執行資料重新整理也可簡化下游的權限需求。 此使用者極有可能已經具備目標資料庫的權限。 當資料重新整理以此人的 Windows 使用者身分識別執行時，任何指定「目前使用者」的資料連線都會自動運作。

 其缺點是管理能力有限。 雖然會自動建立目標應用程式，但卻不會隨著帳戶資訊變更而自動刪除或更新。 密碼到期原則可能會造成目標應用程式過期。 使用過期認證的資料重新整理作業將無法啟動。 當發生此狀況時，排程擁有者必須在資料重新整理排程中提供目前的使用者名稱及密碼值，以更新其認證。 如此之後，即會建立新的目標應用程式。 使用者會在其資料重新整理排程中加入及修訂認證資訊，因此，在經過一段時間之後，您的系統上可能會出現大量自動產生的目標應用程式。

 目前尚無法區分使用中及非使用中的目標應用程式，也無法循著特定的目標應用程式追溯回使用該目標應用程式的資料重新整理排程。 一般而言，您應保留這些目標應用程式，因為刪除這些應用程式可能會破壞現有的資料重新整理排程。 刪除仍在使用中的目標應用程式會導致資料重新整理失敗，並顯示「找不到目標應用程式」訊息，出現在活頁簿的資料重新整理記錄頁面中。

 您若是選擇停用此認證選項，可以放心刪除針對 PowerPivot 資料重新整理所產生的所有目標應用程式。

 **不允許在資料重新整理排程中使用任意的 Windows 認證**

1.  在 [管理中心] 的 [應用程式管理] 中，按一下 [**管理服務應用程式**]。

2.  按一下 PowerPivot 服務應用程式名稱。 隨即出現 PowerPivot 管理儀表板。

3.  在 [動作] 中，按一下 [**設定服務應用程式設定**] 以開啟 [PowerPivot 服務應用程式設定] 頁面

4.  在 [資料重新整理] 區段中，清除 [**允許使用者輸入自訂的 Windows 認證**] 核取方塊。

     ![SSAS_PowerPivotDatarefreshOptions_AllowUser](media/ssas-powerpivotdatarefreshoptions-allowuser.gif "SSAS_PowerPivotDatarefreshOptions_AllowUser")

##  <a name="bkmk_stored"></a>步驟3：建立目標應用程式來儲存資料重新整理時所使用的認證
 當您設定 Secure Store Service 之後，SharePoint 管理員即可建立目標應用程式，將預存認證提供給資料重新整理作業使用，包括 PowerPivot 自動資料重新整理帳戶，或是其他用於執行此作業或連接至外部資料來源的帳戶。

 一如前文所述，您必須建立目標應用程式，才可使用某些認證選項。 特別是您必須為 PowerPivot 自動資料重新整理帳戶建立目標應用程式，以及其他您要在資料重新整理作業中使用的預存認證。

 如需如何建立包含預存認證之目標應用程式的詳細資訊，請參閱[設定 Powerpivot 無人看管的資料重新整理帳戶 &#40;PowerPivot for SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)並[設定 powerpivot 資料重新整理的預存認證 &#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。

##  <a name="bkmk_scale"></a>步驟4：設定伺服器以進行可調整的資料重新整理
 每個 PowerPivot for SharePoint 安裝預設都會支援視需要的查詢及排程資料重新整理功能。

 您可為每個安裝指定 Analysis Services 伺服器執行個體要同時支援查詢與排程資料重新整理功能，或只要執行某種特定類型的作業。 您的伺服器陣列中如有多個 PowerPivot for SharePoint 安裝，而且作業出現延遲或失敗的狀況，也可考慮使用專用的伺服器執行資料重新整理作業。

 除此之外，在基礎硬體支援的情況下，也可增加並行執行的資料重新整理作業數目。 可並行執行的作業數目預設會依據系統記憶體進行計算，但您如有加裝額外的 CPU 可以負荷此工作量，也可提高該數目。

 如需詳細資訊，請參閱[設定專用資料重新整理或僅查詢處理 &#40;PowerPivot for SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)。

##  <a name="bkmk_installdp"></a>步驟5：安裝用來匯入 PowerPivot 資料的資料提供者
 資料重新整理作業基本上就是重複擷取原始資料的匯入作業。 這表示，用於在 PowerPivot 用戶端應用程式中匯入資料的相同資料提供者也必須安裝在 PowerPivot 伺服器上。

 您必須是本機系統管理員，才能在 Windows 伺服器上安裝資料提供者。 您若是安裝其他驅動程式，請務必在安裝有 PowerPivot for SharePoint 之 SharePoint 伺服器陣列的每部電腦上安裝這些驅動程式。 如果伺服器陣列中有多部 PowerPivot 伺服器，您就必須在每部伺服器上安裝提供者。

 請記住，SharePoint 伺服器是 64 位元應用程式。 請務必安裝您所使用的 64 位元版資料提供者來支援資料重新整理作業。

##  <a name="bkmk_accounts"></a>步驟6：授與建立排程及存取外部資料源的許可權
 活頁簿擁有者或作者必須具備 **[參與]** 權限，才能排程活頁簿的資料重新整理。 基於此許可權等級，他或她可以開啟和編輯活頁簿的 [資料重新整理] 設定頁面，以指定用來重新整理資料的認證和排程資訊。

 除了 SharePoint 權限之外，也必須檢閱外部資料來源的資料庫權限，確保重新整理資料期間所使用的帳戶，也具備足夠的權限可以存取資料。 決定權限需求時應謹慎評估，因為您所要授與的權限會隨活頁簿中的連接字串，以及執行資料重新整理作業時所用的使用者識別而不同。

 **PowerPivot 活頁簿中現有的連接字串與 PowerPivot 資料重新整理作業之間的關係**

 當資料重新整理執行時，伺服器會傳送連接要求給使用一開始匯入資料時所建立之連接字串的外部資料來源。 資料重新整理期間將會重複使用該連接字串中所指定的伺服器位置、資料庫名稱及驗證參數，以存取相同的資料來源。 您無法針對不同的資料重新整理用途，修改連接字串及其整體建構， 只可以現況重複用於資料重新整理。 在某些情況下，您若是使用 Windows 以外的驗證方式連接資料來源，可以覆寫連接字串中的使用者名稱及密碼。 本主題將會就此提供進一步的詳細資料。

 對於大多數的活頁簿而言，連接時的預設驗證選項是使用信任的連接或 Windows 整合式安全性，因此連接字串中會包含 `SSPI=IntegratedSecurity` 或 `SSPI=TrustedConnection`。 在資料重新整理期間使用此連接字串時，用來執行資料重新整理工作的帳戶會變成「目前使用者」。 因此，該帳戶必須有權讀取所有透過信任連接進行存取的外部資料來源。

 **啟用了 PowerPivot 自動資料重新整理帳戶嗎？**

 如有啟用，即應授與帳戶對於資料重新整理期間所要存取之資料來源的讀取權限。 此帳戶需要讀取權限的原因是因為在使用預設驗證選項的活頁簿中，自動帳戶在資料重新整理期間將會是「目前使用者」。 除非排程擁有者覆寫了連接字串中的認證，否則此帳戶必須有權讀取貴組織中目前正在使用之任何數量的資料來源。

 **您要使用認證選項 2：允許排程擁有者輸入 Windows 使用者名稱及密碼嗎？**

 通常建立 PowerPivot 活頁簿的使用者因為一開始就執行了資料匯入作業，所以應已具備足夠的權限。 這些使用者之後若是將資料重新整理設定成使用其 Windows 使用者識別執行，則在資料重新整理期間，將會使用其具備資料庫各項權限的 Windows 使用者帳戶擷取資料。 現有的權限應已足夠。

 **您要使用認證選項 3：使用 Secure Store Service 目標應用程式提供執行資料重新整理作業所要使用的使用者識別嗎？**

 與前文所述 PowerPivot 自動資料重新整理帳戶一樣，任何用於執行資料重新整理作業的帳戶都必須具備讀取權限。

 **如何檢查連接字串，以判斷您是否可以覆寫資料重新整理期間所使用的認證**

 如前文所述，倘若連接使用 Windows 以外的驗證方式 (如 SQL Server 驗證)，您可在資料重新整理作業層級替換另一個使用者名稱及密碼。 非 Windows 認證會透過利用使用者識別碼及密碼參數的連接字串進行傳遞。 活頁簿中的連接字串如有包含這些參數，可以選擇是否要指定其他的使用者名稱及密碼，以重新整理該資料來源中的資料。

 下列步驟說明如何判斷您的連接字串是否可以讓您覆寫使用者名稱及密碼。

1.  使用 Excel 開啟該活頁簿。

2.  開啟 PowerPivot 視窗 (在 Excel 的 PowerPivot 功能區上按一下 [PowerPivot 視窗])。

3.  按一下 [**設計**]。

4.  按一下 [**現有連接**]。

     活頁簿中使用的所有連接都會列在 [ **PowerPivot 資料連接**] 之下。

5.  選取連接，然後按一下 [**編輯**]，再按一下 [ **Advanced**]。 該連接字串會顯示在頁面底部。

 如果您在連接字串中看到 [**整合式安全性 = SSPI** ]，則無法覆寫連接字串中的認證。 連接一律會使用目前使用者， 並忽略您所提供的任何認證。

 如果您看到 [**保存安全性資訊 = False，Password\*\*\*\*\*\*\*\*\*\*\*=，UserID\<= userlogin>**]，則表示您有可接受認證覆寫的連接字串。 連接字串中所出現的認證 (如使用者識別碼及密碼) 並非 Windows 認證，而是資料庫登入或其他對目標資料來源有效的登入帳戶。

 **如何覆寫連接字串中的認證**

 您可以藉由在資料重新整理排程中指定資料來源認證的方式覆寫認證。 您身為管理員，可以在 Secure Store Service 中提供對應至存取外部資料時所用之認證的目標應用程式。 如此一來，排程擁有者即可在其定義的資料重新整理排程中，輸入目標應用程式識別碼。 如需建立此目標應用程式的詳細資訊，請參閱[設定 PowerPivot 資料重新整理的預存認證 &#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。

 除此之外，排程擁有者也可輸入資料重新整理期間，用於連接資料來源的認證集。 下圖說明排程定義頁面中的這個資料來源選項。

 ![SSAS_PowerPivotKJ_DataRefreshDSOptions](media/ssas-powerpivotkj-datarefreshdsoptions.gif "SSAS_PowerPivotKJ_DataRefreshDSOptions")

 **確認資料存取需求**

 如前文所述，用於執行資料重新整理及連接外部資料來源的帳戶，通常會是同一個。 因此，用於存取外部資料來源的帳戶，將會由資料重新整理排程頁面中這部分的選項設定決定。 此帳戶可能是 PowerPivot 自動資料重新整理帳戶、個人使用者的 Windows 帳戶，或是儲存在預先定義之目標應用程式中的帳戶。

 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")

 若用來執行資料重新整理的帳戶不同於匯入資料的帳戶 (例如認證選項 1 的 PowerPivot 自動資料重新整理帳戶，或是認證選項 3 的其他預存認證集)，即必須針對該帳戶建立新的資料庫登入，並授與其對外部資料來源的讀取權限。

 當您確認需要存取資料的帳戶之後，即可開始檢查 PowerPivot 活頁簿中最常使用之資料來源的權限。 您可以先從目前正在使用的任何資料倉儲或報告資料庫著手，並向目前正在使用 PowerPivot 的使用者收集意見，了解其所使用的資料來源。 當您列出資料來源之後，即可逐項檢查其權限設定是否正確。

##  <a name="bkmk_upgradewrkbk"></a>步驟7：啟用資料重新整理的活頁簿升級
 根據預設，使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 版本的 PowerPivot for Excel 所建立的活頁簿不得在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 版本的 PowerPivot for SharePoint 上設定排程資料重新整理。 如果您在 SharePoint 環境中裝載較新和較舊版本的 PowerPivot 活頁簿，您必須先升級任何 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 活頁簿，然後才可在伺服器上排程自動資料重新整理。

##  <a name="bkmk_verify"></a>步驟8：確認資料重新整理設定
 若要確認資料重新整理，您必須擁有發行到 SharePoint 網站的 PowerPivot 活頁簿。 您必須具備活頁簿的「參與」權限，以及存取資料重新整理排程中所含之任何資料來源所需的各項權限。

 當您建立排程時，請選取 [**也**儘快重新整理] 核取方塊，以立即執行資料重新整理。 接著您可以查看該活頁簿的資料重新整理記錄頁面，確認其執行是否成功。 請注意，PowerPivot 資料重新整理計時器工作會每隔一分鐘執行一次， 因此，您至少必須等候一分鐘，才能確認資料重新整理是否成功。

 請務必試用您打算支援的所有認證選項。 例如，您若是設定 PowerPivot 自動資料重新整理帳戶，請使用該選項驗證資料重新整理是否成功。 如需有關排程和查看狀態資訊的詳細資訊，請參閱排程資料重新整理[&#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)和[觀看資料重新整理記錄 &#40;PowerPivot for SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)。

 如果資料重新整理失敗，請參閱 TechNet wiki 上的[疑難排解 PowerPivot 資料](https://go.microsoft.com/fwlink/?LinkID=223279)重新整理頁面，以取得可能的解決方案。

##  <a name="bkmk_config"></a>修改資料重新整理的設定
 每個 PowerPivot 服務應用程式各有其影響資料重新整理作業的組態設定。 本節說明如何修改這些設定。

###  <a name="procIntervals"></a>設定「上班時間」以判斷下班時間處理
 排程資料重新整理作業的 SharePoint 使用者可以指定「下班後」的最早開始時間。 如果使用者想要擷取工作日期間累積的商務交易資料，這項功能會很有用。 身為伺服陣列管理員，您可以依最適合組織所定義工作日的時間範圍指定。 如果您定義工作日是從 04:00 到 20:00，則根據「下班後」進行的資料更新處理開始時間就會是 20：01。

 在下班期間執行的資料重新整理要求會依收到要求的順序加入佇列。 個別的要求會在伺服器資源可使用的情況下進行處理。

1.  在 [管理中心] 的 [應用程式管理] 中，按一下 [**管理服務應用程式**]。

2.  按一下 PowerPivot 服務應用程式名稱。 隨即出現 PowerPivot 管理儀表板。

3.  在 [動作] 中，按一下 [**設定服務應用程式設定**] 以開啟 [PowerPivot 服務應用程式設定] 頁面

4.  在 [資料重新整理] 區段的 [上班時間] 中，輸入定義下班後處理期間的開始及結束時間。

     如果不要定義下班處理期間，可以為 [開始時間] 和 [結束時間] 輸入相同的值 (例如，兩個時間都設定為 12: 00)。 不過請注意，SharePoint 網站上的排程定義頁面仍然會提供「下班後」做為選項。 如果使用者在未定義下班處理範圍的伺服器陣列上選取了該選項，最後會因為處理工作無法啟動而接到資料重新整理錯誤訊息。

5.  按一下 [確定]  。

###  <a name="usagehist"></a>限制資料重新整理記錄的保留時間長度
 資料重新整理記錄是資料重新整理作業隨著時間經過所產生的成功與失敗訊息詳細記錄。 記錄資訊是透過伺服器陣列中的使用量資料收集系統進行收集與管理。 因此，您在使用量資料記錄上設定的限制也會套用至資料重新整理記錄。 由於使用活動報告會彙集整個 PowerPivot 系統的資料，所以只使用單一記錄設定來控制資料重新整理記錄與收集及儲存之所有其他使用量資料的資料保留。

1.  在 [管理中心] 的 [應用程式管理] 中，按一下 [**管理服務應用程式**]。

2.  按一下 PowerPivot 服務應用程式名稱。 隨即出現 PowerPivot 管理儀表板。

3.  在 [動作] 中，按一下 [**設定服務應用程式設定**] 以開啟 [PowerPivot 服務應用程式設定] 頁面

4.  在 [使用量資料收集] 區段的 [使用量資料記錄] 中，輸入要為每個活頁簿記錄資料重新整理活動的天數。

     預設值為 365 天。 最小值是 1 天，最大值是 5000 天。 0 指定無限制的保留期間，也就是永遠不會刪除資料。 請注意，您無法透過任何設定關閉記錄。

5.  按一下 [確定]  。

 SharePoint 使用者在具有資料重新整理記錄的活頁簿上選擇 [管理資料重新整理] 選項時，就可以使用記錄資訊。 這項資訊也用在伺服器陣列管理員用來管理 PowerPivot 服務作業的 PowerPivot 管理儀表板。 如需詳細資訊，請參閱[View Data Refresh History &#40;PowerPivot for SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)。

 記錄資料的長期實體儲存體位於 PowerPivot 服務應用程式的 PowerPivot 服務應用程式資料庫中。 如需如何收集和儲存使用量資料的詳細資訊，請參閱[PowerPivot 使用量資料收集](power-pivot-sharepoint/power-pivot-usage-data-collection.md)。

##  <a name="configTimerJob"></a>重新排程 PowerPivot 資料重新整理計時器工作
 已排程的資料重新整理是由 PowerPivot 資料重新整理計時器工作所觸發，此工作每隔一分鐘，就會掃描 PowerPivot 服務應用程式資料庫中的排程資訊。 當資料重新整理要依排程開始進行時，計時器工作會將要求加入可用 PowerPivot 伺服器的處理佇列中。

 您可以增加掃描間隔的時間，當做效能微調技巧使用。 您也可以停用計時器工作，在對問題進行疑難排解時，暫時停止資料重新整理作業。

 預設值是一分鐘，這是您可以指定的最低值。 因為此值可為一天內任意時間執行的排程提供最可預期的結果，所以建議使用此值。 例如，如果使用者排定在下午 4:15 執行資料重新整理，而且計時器工作每分鐘都會掃描排程資訊，則系統就會在 4:15 偵測到已排程的資料重新整理要求，4:15 之後數分鐘內就會執行處理。

 如果您提高掃描間隔，以極低的頻率執行 (例如，每天午夜執行一次)，原先排定在該間隔期間執行的所有資料重新整理作業就會全部一次加入處理佇列中，這可能會讓伺服器負載過重並佔用其他應用程式的系統資源。 視已排程的重新整理數目而定，資料重新整理作業的處理佇列可能會不斷累積到無法完成所有工作。 如果作業持續到下一個處理間隔，佇列結尾的資料重新整理要求可能會被卸除。

 如果硬體支援的話，您可以藉由指定額外處理器平行執行其他資料重新整理作業，以減輕這個問題。 如需詳細資訊，請參閱[設定專用資料重新整理或僅查詢處理 &#40;PowerPivot for SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)。 如需如何探索資料重新整理要求、將其新增至佇列，以及進行處理的詳細資訊，請參閱[PowerPivot 資料](power-pivot-sharepoint/power-pivot-data-refresh.md)重新整理。

1.  在管理中心，按一下 **[監視]**。

2.  按一下 [**審查工作定義**]。

3.  選取 [ **PowerPivot 資料重新整理計時器工作**]。

4.  修改排程頻率，以變更計時器工作掃描資料重新整理排程資訊的頻率。

##  <a name="bkmk_disableDR"></a>停用資料重新整理計時器工作
 PowerPivot 資料重新整理計時器工作是伺服器陣列層級的工作，它會針對伺服器陣列中的所有 PowerPivot 伺服器執行個體一起啟用或停用。 這項工作不會繫結至特定 Web 應用程式或 PowerPivot 服務應用程式。 您無法在某些伺服器上停用，以強制在伺服器陣列中的其他伺服器上執行資料重新整理處理。

 如果停用 PowerPivot 資料重新整理計時器工作，已排入佇列的要求將進行處理，但您必須重新啟用工作，才能再加入新的要求。 已排定在過去執行的要求不會進行處理。

 停用計時器工作對應用程式頁面中功能的可用性不會有任何影響。 在 Web 應用程式中，沒有任何方法可以移除或隱藏資料重新整理功能。 即使永久停用計時器工作，擁有「參與」或以上權限的使用者仍然可以建立新的資料重新整理作業排程。

## <a name="see-also"></a>另請參閱
 [排程資料重新整理 &#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md) [設定專用的資料重新整理或僅限查詢的處理 &#40;PowerPivot for SharePoint](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)&#41;[設定 Powerpivot 無人看管的資料重新整理帳戶 &#40;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md) PowerPivot for SharePoint&#41;[設定 Powerpivot 資料重新整理的預存認證 &#40;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md) PowerPivot for SharePoint&#41;


