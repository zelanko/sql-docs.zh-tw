---
title: "安全性 (報表產生器) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ed38291a-6afe-449f-9f32-3ae04502bd6f
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7e6f09ff050246777e307f73280c764dd6da3ad7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="security-report-builder"></a>安全性 (報表產生器)
  報表產生器是一種報表撰寫用戶端應用程式，專為搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器使用而設計。 該報表伺服器可以設定為以獨立伺服器的原生模式運作，或者以 SharePoint 整合模式運作以支援 SharePoint 網站上的報表。  
  
 在報表產生器中，您可以撰寫報表、共用的資料集以及可重複使用的報表組件。 從報表伺服器或 SharePoint 網站上，您可以編輯報表並且加入共用的資料來源、共用的資料集以及共用的報表組件。  
  
 在撰寫、發行並且使用報表與報表相關的項目之前，您必須先了解與下列層面相關的安全性功能：  
  
-   **您在其中發行報表的報表伺服器或 SharePoint 網站** ：這些功能是由報表伺服器管理員或 SharePoint 網站管理員所管理。  
  
-   **已發行的報表與報表相關的項目** ：報表相關的項目包括內嵌與共用的資料來源，以及它們的認證、共用的資料集、參數、報表組件與報表模型。 套用到這些項目的安全性功能是由報表作者所管理。 報表伺服器管理員或 SharePoint 網站管理員必須授與報表作者適當的權限，報表作者才能夠發行並共用項目。  
  
-   **報表所使用的外部資料來源** ：這些功能是由外部資料來源的擁有者所管理。  
  
-   **以外部資料來源為基礎的報表模型** ：這些功能由模型設計人員所管理。  
  
-   **互動式報表功能，例如參數** ：這些功能是由報表作者所管理。  
  
 請檢閱本主題中的資訊，協助您更深入了解如何使用安全性功能，進一步協助管理及維護報表與報表相關項目的安全性。  
  
##  <a name="ReportServers"></a> 了解報表伺服器的安全性  
 發行報表與檢視報表是需要有適當權限才能進行的作業。 報表伺服器管理員會授與使用權限，確保只有獲得授權的使用者才可以在下列其中一種報表伺服器上發行並檢視報表：  
  
-   以原生模式設定的報表伺服器  
  
     若要連接或瀏覽至報表伺服器，您必須具有有效的 URL 與存取伺服器的適當權限。  
  
     若要在報表伺服器上檢視或發行項目，套用到報表相關項目與作業的多組使用權限會根據角色分組。 報表伺服器管理員會將您指派為一個或多個角色。 例外，預先定義的角色 [瀏覽者] 可以讓您檢視報表、資料夾、模型與資源。  
  
     如果您無法連接或瀏覽至報表伺服器，請連絡報表伺服器管理員。 如需詳細資訊，請參閱《 [](../../reporting-services/security/reporting-services-security-and-protection.md) 線上叢書》 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312).  
  
-   以 SharePoint 整合模式設定的報表伺服器  
  
     若要連接至與報表伺服器整合的 SharePoint 網站，您必須具有有效之 SharePoint 網站或子網站的 URL 以及存取該報表伺服器的適當權限。  
  
     用於存取報表相關項目和作業的權限是透過 SharePoint 安全性原則所授與，這些原則會將使用者或群組帳戶對應至權限等級 (相對於項目)。  
  
     如果您無法連接或瀏覽到 SharePoint 網站或子站台，請連絡 SharePoint 網站管理員。  
  
  
##  <a name="Reports"></a> 了解已發行報表與報表相關項目的安全性  
 報表與報表相關項目的安全性是由報表伺服器管理員所管理。 報表相關的項目包括內嵌與共用的資料來源，包括了認證、共用的資料集、參數、報表組件與模型。  
  
 在報表伺服器或 SharePoint 網站上，報表與報表相關項目及作業的安全性為獨立的。 用於存取項目和作業的權限是透過安全性原則所授與，這些原則會將使用者或群組帳戶對應至權限等級 (相對於項目)。 為了簡化維護大量原則的複雜性與成本，容器 (例如資料夾) 上的使用權限會由容器中的項目繼承。 例如，如果使用者對某一資料夾具有特定的 [檢視報表] 權限，那麼該使用者對於資料夾中的項目也具有 [檢視報表] 權限。  
  
 可以透過使用項目層級安全式的方式，覆寫項目或資料夾上的權限。 套用項目層級安全性後，來自父容器的權限繼承將不再適用於該項目。 如果對資料夾套用項目層級安全性，則巢狀資料夾會繼承相同的權限。  
  
 如果您無法瀏覽到或找到其他使用者已為您發行的項目，可能表示您對該項目或資料夾尚未具有適當的權限。  
  
 若要讓其他使用者瀏覽到並且找到您已發行要共用的項目，您必須請報表伺服器管理員設定資料夾組織，以便為您的使用者提供存取權限。 撰寫報表並且執行已發行的報表時，必須能夠使用 Access。  
  
 如需詳細資訊，請參閱《 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [角色與權限 &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  
-   [管理共用資料集](../../reporting-services/report-data/manage-shared-datasets.md)  
  
### <a name="update-notifications-for-report-parts"></a>報表組件更新通知  
 報表組件會發行到報表伺服器，讓其他使用者可以共用這些組件。 根據預設，您可以指定要發行報表組件的目標位置。  
  
 在報表中加入報表組件的使用者可以啟用更新功能。 啟用這項功能時，使用者會在報表伺服器上的報表組件發生變更時，收到通知。  
  
 如果報表組件已經從原來的位置移動，那麼更新通知會包含報表組件目前的位置以及先前的位置。 只接受來自受信任位置的更新。  
  
 如需詳細資訊，請參閱 [報表組件 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)。  
  
  
##  <a name="Data"></a> 了解報表資料與外部資料來源的安全性  
 若要存取報表中每一個外部資料來源的資料，您可以建立內嵌資料來源或是將加入報表中共用資料來源或共用資料集的參考。  
  
 針對每一個外部資料來源，您必須提供存取該來源及其底層資料的適當認證。 資料來源擁有者會指定提供存取的認證類型。  
  
 認證不會儲存在報表定義中。 這些認證會另外進行管理，有別與報表伺服器或 SharePoint 以及報表撰寫用戶端上的報表。  
  
 在報表設計階段，認證會用於執行資料集查詢和預覽報表。 在執行階段，認證會用於執行報表與快取查詢結果。 您也可以獨立地快取共用資料集查詢結果。 設計階段與執行階段使用的認證可能會不同。 如需詳細資訊，請參閱 [在報表產生器中指定認證](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
 如需維護資料安全的詳細資訊，請參閱《 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 如需資料來源的詳細資訊，請參閱 [報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
  
##  <a name="Models"></a> 了解模型與安全性篩選  
 當資料擷取自以外部資料為基礎的報表模型時，您可以在模型中套用安全性篩選。這是維護資料安全的好方法，因為如此一來，每一位執行報表的使用者都只能看到他們有權限讀取的內容。  
  
 報表參數不能用於資料列層級安全性，也無法防止使用者或使用者群組查看特定的資料列。 若要為報表內所顯示的資料套用安全性，您需要使用安全性篩選或模型項目安全性。  
  
  
##  <a name="Interactive"></a> 了解撰寫具有互動式功能之報表的安全性  
 報表經常會使用參數，讓使用者可以互動式地自訂他們的報表檢視。 請採用下列秘訣協助設計出遵循優良作法的報表：  
  
-   除非您會提供有效的值，否則請不要使用依據查詢參數以及屬於 **[文字]** 類型的參數。 可用的值清單有助於使用者只選擇有效的值。 如果沒有有效的值清單，則您將無法限制使用者可以輸入的值。  
  
-   請不要使用全域 [&UserID] 來維護私用資料的安全性。 這個值做為報表參數時，可以利用 URL 存取語法在報表 URL 中指定它。 在共用資料集的運算式中使用這個值，會讓資料集無法被快取。 如需詳細資訊，請參閱《 [](../../reporting-services/url-access-parameter-reference.md) 線上叢書》 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312).  
  
 項目發行到報表伺服器後，報表伺服器管理員可以指定以角色為基礎的安全性或資料夾與項目層級安全性，藉此維護這些項目的安全。 如需詳細資訊，請參閱《 [](../../reporting-services/security/secure-reports-and-resources.md) 線上叢書》 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312).  
  
  
## <a name="see-also"></a>另請參閱  
 [安裝和解除安裝報表產生器](http://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416)   
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
