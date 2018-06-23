---
title: Reporting Services 報表伺服器 (原生模式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- administering Reporting Services
- administering [Reporting Services]
- Reporting Services, administration
ms.assetid: fa0d84e2-4c21-432c-aa7c-23517da75253
caps.latest.revision: 23
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 9673fbd613b927a16b4d5a66ee49ac74c158ca87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034519"
---
# <a name="reporting-services-report-server-native-mode"></a>Reporting Services Report Server (Native Mode)
  針對原生模式設定的報表伺服器會當做應用程式伺服器執行，並透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]元件專門提供所有處理和管理能力。  
  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或報表管理員來管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表。 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員可在原生模式中管理報表伺服器。  
  
 如果報表伺服器是針對 SharePoint 模式所設定，您就必須使用 SharePoint 網站上的內容管理頁面來管理報表、共用資料來源和其他報表伺服器項目。  
  
 本主題包含下列資訊：  
  
-   [原生模式摘要](#bkmk_sum)  
  
-   [管理內容](#bkmk_managecontent)  
  
-   [保護和管理資源](#bkmk_manageresources)  
  
-   [從報表參考影像資源](#bkmk_referenceimage)  
  
##  <a name="bkmk_sum"></a> 原生模式摘要  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式安裝包含多項需要管理及維護的伺服器端功能。 此伺服器功能包含以下項目：  
  
-   報表伺服器 Web 服務 (在報表伺服器服務內部執行)。  
  
-   背景處理應用程式 (處理排程作業和報表傳遞)。  
  
-   報表伺服器資料庫。  
  
 若要完整地管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝，您必須具備下列權限：  
  
-   報表伺服器電腦上本機管理員群組中的成員資格。 如果您的安裝包含在遠端電腦上執行的伺服器功能，則當您想要透過遠端連接來管理這些伺服器時，必須具備這些電腦上的管理員權限。  
  
-   主控資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料庫管理員權限。  
  
-   如果您將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝在網域控制站上，您必須是網域管理員。  
  
##  <a name="bkmk_managecontent"></a> 管理內容  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，內容管理是指報表、模型、資料夾、資源和共用資料來源的管理。 所有的這些項目都可以透過屬性和安全性設定單獨進行管理， 而任何一個項目都可以移至報表伺服器資料夾命名空間內的不同位置。 若要有效管理項目，您必須了解內容管理員所執行的工作。  
  
> [!NOTE]  
>  內容管理與報表伺服器管理不同。 如需如何管理報表伺服器的執行的環境的詳細資訊，請參閱[(Reporting Services)](reporting-services-report-server-native-mode.md)。  
  
 內容管理包括下列工作：  
  
-   藉由套用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]所提供以角色為基礎的安全性，保護報表伺服器站台及項目的安全。  
  
-   藉由加入、修改和刪除資料夾，將報表伺服器資料夾階層結構化。  
  
-   設定適用於報表伺服器所管理之項目的預設值及屬性。 例如，您可以設定最大基準值，來決定報表記錄的儲存原則。  
  
-   建立可以用來取代報表特定資料來源連接的共用資料來源項目。 發行者或內容管理員可以選取和報表原始定義不同的資料來源；例如，以實際執行的資料庫的參考取代測試資料庫的參考。  
  
-   建立可用來取代報表特有和訂閱特有排程的共用排程，讓您更方便地隨著時間維護排程資訊。  
  
-   藉由從資料存放區擷取資料，建立可產生收件者清單的資料驅動訂閱。  
  
-   藉由建立報表處理排程，並指定何者可依需求執行以及何者要從快取載入，即可平衡伺服器的報表處理負荷。  
  
 執行管理工作的權限是透過兩個預先定義角色提供的： **系統管理員** 和 **內容管理員**。 您必須被指派至這兩種角色，才能有效管理報表伺服器內容。 如需這些預先定義角色的詳細資訊，請參閱[角色與權限 &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md)。  
  
 用於管理報表伺服器內容的工具包括 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或報表管理員。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 可讓您設定預設值和啟用功能。 報表管理員是用來將報表伺服器項目與作業的存取權授與使用者、檢視和使用報表與其他內容類型，以及檢視和使用所有共用項目與報表散發功能。  
  
##  <a name="bkmk_manageresources"></a> 保護和管理資源  
 資源是指儲存在報表伺服器上，但並非由報表伺服器所處理的 Managed 項目。 一般而言，資源會提供外部內容給報表使用者。 範例包括 .jpg 檔或 HTML 檔中描述報表所使用之商務規則的影像。 雖然此 JPG 或 HTML 檔會儲存在報表伺服器上，但是報表伺服器會直接將此檔案傳遞至瀏覽器而非先處理它。  
  
 若要將資源加入至報表伺服器，您可以上傳或發行檔案：  
  
|作業|檔案類型|  
|---------------|---------------|  
|上傳|除了報表定義 (.rdl) 和報表模型 (.smdl) 檔以外，所有檔案都會當做資源上傳。<br /><br /> 若要上傳資源，您必須使用報表管理員 (如果報表伺服器以原生模式執行的話) 或 SharePoint 網站上的應用程式頁面 (如果伺服器以 SharePoint 整合模式執行的話)。 如需詳細資訊，請參閱[上傳檔案或報表 &#40;報表管理員&#41;](../reports/upload-a-file-or-report-report-manager.md) 或[將文件上傳到 SharePoint 文件庫 &#40;SharePoint 模式的 Reporting Services&#41;](../upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)。|  
|發行|除了 .rdl、.smdl 和 .rds 資料來源檔案以外，專案中的所有檔案都會當做資源上傳。 若要發行資源，請在報表設計師中，將現有的項目加入至專案，然後將此專案發行至報表伺服器。|  
  
 所有資源都會先在檔案系統上以檔案的形式產生，然後再上傳至報表伺服器。 除了 ASP.NET 所加諸的 4 MB 預設檔案大小限制以外，您可以上傳的檔案類型沒有任何限制。 不過，以資源發行至報表伺服器時，具有對等 MIME 類型之檔案類型的效能會優於其他類型。 例如，當使用者按一下資源時，以 HTML 和 JPG 檔為基礎的資源將在瀏覽器視窗中開啟，HTML 將轉譯成網頁，JPG 將轉譯成影像，供使用者檢視。 反之，沒有對等 MIME 類型的資源 (例如桌上型電腦應用程式檔案) 可能就無法在瀏覽器視窗中轉譯。  
  
 資源是否可供報表使用者檢視，要看瀏覽器的檢視功能而定。 由於報表伺服器不會處理資源，因此瀏覽器可能會提供檢視功能來轉譯特定 MIME 類型。 如果瀏覽器無法轉譯內容，檢視資源的使用者就只能看到資源的一般屬性。  
  
 資源會連同報表、共用資料來源、共用排程和資料夾一起當做具名項目存在報表伺服器資料夾階層中。 您可以搜尋、檢視、保護和設定資源的屬性，就像處理報表伺服器上所儲存的任何項目一樣。 若要檢視或管理資源，您的角色指派中必須具有檢視資源或管理員資源的工作。  
  
##  <a name="bkmk_referenceimage"></a> 從報表參考影像資源  
 資源可以包含您在報表中參考的影像。 如果報表需求包括使用外部影像，請考慮下列將影像儲存成資源的優點：  
  
-   報表伺服器資料庫中的集中式儲存。 如果您將報表伺服器資料庫及其內容移至另一部電腦，外部影像會與報表一起移動。 您不需要追蹤儲存在不同電腦之磁碟上的影像檔。  
  
-   透過角色指派而非檔案系統安全性進行保護。 用來檢視報表的相同權限可以套用至資源。 反之，如果您將影像儲存在磁碟上，就必須確保匿名使用者帳戶或自動執行帳戶擁有存取此檔案的權限。  
  
 若要在報表中使用影像資源，請將影像檔加入至專案，然後將它與報表一起發行。 發行影像之後，您可以更新報表中的影像參考，讓它指向報表伺服器上的資源，然後單獨重新發行該報表，以便儲存您的變更。 之後，您就可以透過重新發行資源，更新影像 (與報表分開處理)。 報表會使用報表伺服器上可用的最新影像版本。  
  
## <a name="see-also"></a>另請參閱  
 [設定和管理報表伺服器 &#40;SSRS 原生模式&#41;](configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [針對 Reporting Services 安裝進行疑難排解](../install-windows/troubleshoot-a-reporting-services-installation.md)  
  
  