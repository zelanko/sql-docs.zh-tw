---
title: 建立、修改及刪除共用資料來源 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 26bc12ce8c685c4aeb119f43ab594d920a6cef9f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59934744"
---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>建立、修改及刪除共用資料來源 (SSRS)
  共用資料來源是一組資料來源連接屬性，可供多個報表、模型以及在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器上執行的資料驅動訂閱參考。 共用資料來源提供一種簡單的方式，可用來管理通常會隨著時間而變更的資料來源屬性。 如果使用者帳戶或密碼變更，或者如果您將資料庫移到不同的伺服器，可以在一個地方更新連接資訊。  
  
 對於報表以及資料驅動訂閱而言，共用資料來源是選擇性的，但是對於報表模型而言，則是必要的。 如果您打算將報表模型用於隨選報表，您必須建立並維護一個共用資料來源項目，才能提供連接資訊給模型。  
  
 共用資料來源包含下列部分：  
  
|部分|描述|  
|----------|-----------------|  
|名稱|識別報表伺服器資料夾階層中之項目的名稱。|  
|描述|檢視資料夾的內容時，與「報表管理員」中的項目一起顯示的描述。|  
|連接類型|與資料來源搭配使用的資料處理延伸模組。 您僅能使用在報表伺服器上部署的資料處理延伸模組。 如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 隨附之資料處理延伸模組的詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../create-deploy-and-manage-mobile-and-paginated-reports.md)。|  
|連接字串|資料庫的連接字串。 如需詳細資訊，以及要檢視常用的資料來源的連接字串範例，請參閱[資料連接、 資料來源和 Reporting Services 中的連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。|  
|認證類型|指定如何取得用於連接的認證，以及建立連接後是否要使用這些認證。 如需詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](../../integration-services/connection-manager/data-sources.md)。|  
  
 共用資料來源不包含用來擷取資料的查詢資訊。 查詢永遠會保留在報表定義中。  
  
## <a name="creating-and-modifying-a-shared-data-source"></a>建立與刪除共用資料來源  
 若要建立共用資料來源或修改其屬性，您必須擁有報表伺服器的 [管理資料來源] 權限。 如果報表伺服器是在原生模式下執行，您可以使用「報表管理員」來建立與設定共用資料來源。 如果報表伺服器是在 SharePoint 整合模式下執行，您可以使用 SharePoint 網站上的應用程式頁面。 如果是任意模式下的任何報表伺服器，您可以在「報表設計師」中建立共用資料來源，然後將其發行到目標伺服器上。  
  
 如需有關建立共用資料來源的詳細資訊，請參閱：  
  
-   [建立內嵌或共用資料來源 &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)  
  
-   [建立和管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
 在報表伺服器上建立共用資料來源之後，您可以建立角色指派來控制其存取權、將其移動到不同的位置、重新命名它，或者在外部資料來源執行維護作業時離線以防進行報表處理。 如果您重新命名或移動共用資料來源項目至報表伺服器資料夾階層中的其他位置，所有參考共用資料來源的報表或訂閱，其相關路徑資訊會隨之更新。 如果您讓共用資料來源離線，所有報表、模型和訂閱都不會執行，直到您重新啟用資料來源為止。  
  
 如需在報表伺服器資料夾階層控制共用資料來源存取權的詳細資訊，請參閱 [保護共用資料來源項目的安全](../security/secure-shared-data-source-items.md)。  
  
## <a name="deleting-a-shared-data-source"></a>刪除共用資料來源  
 您可以利用從報表伺服器刪除任何項目的相同方式，刪除共用資料來源。 在報表管理員中，您在詳細資料檢視中開啟資料夾，選取項目，然後按一下**刪除**。 在 SharePoint 網站上的 [應用程式] 頁面中，您開啟 SharePoint 文件庫、 選取項目，然後按一下**刪除**。  
  
 刪除共用資料來源將會停用使用共用資料來源的所有報表、模型或資料驅動訂閱。 如果沒有資料來源連接資訊，這些項目就無法再執行 若要啟動這些項目，您必須開啟每個項目，並執行下列動作：  
  
-   若是參考共用資料來源的報表和資料驅動訂閱，您可以在報表屬性或訂閱中指定資料來源連接資訊，或者選取其中包含您要使用之值的新共用資料來源。  
  
-   若是模型或使用該模型的「報表產生器」報表，您必須指定一個新的共用資料來源。 這些模型僅能透過共用資料來源取得資料來源連接資訊。  
  
 若要檢視使用資料來源之報表和模型的清單，開啟共用資料來源的 [相依項目] 頁面。 當您在「報表管理員」或 SharePoint 應用程式頁面中開啟資料來源時，您可以存取此頁面。 請注意，[相依項目] 頁面中不會顯示資料驅動訂閱。 如果共用資料來源是由訂閱所使用，訂閱將不會出現在相依項目清單中。  
  
 刪除共用資料來源時，沒有「復原」作業。 不過，如果您不小心刪除了共用資料來源，可以使用相同的屬性值來建立一個新的共用資料來源。 您必須開啟每個報表、模型和資料驅動訂閱，才能在使用它的項目中重建共用資料來源，但是，只要資料來源屬性與之前的資料來源屬性相同，報表、模型和訂閱就會如先前般運作。  
  
## <a name="see-also"></a>另請參閱  
 [建立和管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [資料連接、 資料來源和 Reporting Services 中的連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [管理報表資料來源](manage-report-data-sources.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [內嵌和共用資料連接或資料來源 &#40;報表產生器及 SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [資料來源屬性頁面 &#40;報表管理員&#41;](../data-sources-properties-page-report-manager.md)   
 [建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [設定報表的資料來源屬性 &#40;報表管理員&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
