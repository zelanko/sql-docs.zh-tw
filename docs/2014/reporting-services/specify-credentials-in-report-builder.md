---
title: 在 報表產生器中指定認證 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7412ce68-aece-41c0-8c37-76a0e54b6b53
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 432b41216418cd1ad1bae70557c95a589f5e78dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101135"
---
# <a name="specify-credentials-in-report-builder"></a>在報表產生器中指定認證
  認證會驗證嘗試從資料來源擷取資料的使用者。 資料來源的擁有者可決定必須使用的認證類型。 例如，資料庫管理員可能會指定使用者必須提供 Windows 使用者名稱和密碼。  
  
 在報表定義中，每個資料來源定義都會指定名稱、連接字串、是否要使用整合式安全性，以及需要認證但沒有指定時要顯示的提示。 認證不會儲存在報表定義中。 在報表伺服器上發行報表之後，資料來源就可以與報表定義分開管理。 資料來源擁有者可以針對報表伺服器上的內嵌和共用資料來源指定認證。  
  
> [!NOTE]  
>  報表伺服器管理員必須授與使用者適當的權限，使用者才能瀏覽報表伺服器以選取共用資料來源或模型，或是開啟或儲存報表。 如需詳細資訊，請參閱 <<c0> [ 安裝、 解除安裝，以及報表產生器支援](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-when-credentials-are-used"></a>了解使用認證的時機  
 在報表產生器中，認證經常在您連接至報表伺服器時使用，或是用於資料相關工作，例如建立內嵌的資料來源、執行資料集查詢，或是預覽報表。 認證不會儲存在報表中。 認證會在報表伺服器或本機用戶端上另行管理。 下列清單說明您可能需要提供的認證類型、認證儲存的位置，以及使用認證的方式：  
  
-   您在 [Reporting Services 登入對話方塊 &#40;報表產生器&#41;](report-builder/reporting-services-login-dialog-box-report-builder.md) 中輸入的報表伺服器認證。  
  
     當您初次儲存、發佈或瀏覽至報表伺服器或 SharePoint 網站時，可能需要輸入您的認證。 您輸入的認證會持續使用到報表產生器工作階段結束為止。 如果您選擇儲存認證，這些認證會在電腦上與使用者設定安全地儲存在一起。 在後續報表產生器工作階段中，儲存的認證會用來連接至相同的報表伺服器或 SharePoint 網站。 報表伺服器管理員或 SharePoint 管理員會指定要使用的認證類型。  
  
-   您在[資料來源屬性對話方塊、認證 &#40;報表產生器&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md) 頁面中針對內嵌資料來源輸入的資料來源認證。  
  
     報表伺服器會使用這些認證建立與外部資料來源的資料連接。 針對部分類型的資料來源，其認證可以安全地儲存在報表伺服器上。 這些認證可讓其他使用者執行報表，而不需提供基礎資料連接的認證。  
  
-   您執行資料集查詢、重新整理資料集欄位或預覽報表時，在[輸入資料來源認證對話方塊 &#40;報表產生器&#41;](report-data/enter-data-source-credentials-dialog-box-report-builder.md) 中輸入的資料來源認證。  
  
     這些認證會用來建立報表產生器與外部資料來源之間的資料連接，或是預覽設定為提示認證的報表。 您在此對話方塊中輸入的認證不會儲存在報表伺服器上，也無法供其他使用者使用。 報表產生器會在報表編輯工作階段中快取認證，因此您不必在每次執行查詢或預覽報表時輸入認證。  
  
     如果是共用資料來源，請使用 **[儲存我的密碼]** 選項將認證與使用者設定一起儲存在本機電腦上。 報表產生器會在每次連接對應的外部資料來源時，使用儲存的認證。  
  
 如需詳細資訊，請參閱[資料來源屬性對話方塊、一般 &#40;報表產生器&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md) 和[在報表產生器中預覽報表](report-builder/previewing-reports-in-report-builder.md)。  
  
## <a name="types-of-credentials"></a>認證的類型  
 資料來源支援的認證類型是由資料來源的擁有者所指定。 例如，若要存取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫，您可能必須提供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入使用者名稱和密碼。 若要存取不同的資料來源，您可能必須提供 Windows 使用者名稱和密碼。 某些資料來源可能不需要認證。  
  
### <a name="options-for-specifying-credentials"></a>指定認證的選項  
 下列選項可用來指定資料來源的認證：  
  
-   使用目前的 Windows 使用者 (也稱為整合式安全性)。  
  
-   使用預存的使用者名稱和密碼。  
  
-   提示使用者提供認證。  
  
-   不需要認證。  
  
### <a name="windows-integrated-security"></a>Windows 整合式安全性  
 當您選取 **[使用 Windows 驗證 (整合式安全性)]** 時，目前使用者的安全性 Token 就會傳遞至資料來源。 在此情況下，不會提示使用者輸入使用者名稱或密碼。 這個選項通常需要啟用委派功能。 如果這些功能未啟用，您只能使用這個選項來存取位於相同電腦上的資料來源。  
  
### <a name="user-name-and-password-login"></a>使用者名稱和密碼登入  
 當您選取 **[使用此使用者名稱和密碼]** 時，必須提供使用者名稱和密碼才能存取資料來源。 若為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫，這些認證可能會用於資料庫登入。 認證將會傳遞至資料來源以供驗證。  
  
### <a name="prompted-credentials"></a>提示認證  
 當您指定提示認證時，存取此報表的每位使用者都必須輸入使用者名稱和密碼，才能擷取資料。 這個選項建議用於包含機密資料的報表。 提示認證可以是 Windows 帳戶或資料庫登入。 如果資料庫伺服器無法辨識您所提供的認證，或者指定的使用者尚未取得擷取資料的權限，連接就會失敗。  
  
### <a name="no-credentials"></a>無認證  
 此資料來源不需要認證。 若要在報表伺服器上執行此報表，則必須設定自動執行帳戶。 如需詳細資訊，請參閱 <<c0> [ 設定自動執行帳戶&#40;SSRS 組態管理員&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)中[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][線上叢書 》](https://go.microsoft.com/fwlink/?linkid=121312)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [安裝、 解除安裝與報表產生器支援](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)   
 [內嵌和共用資料連接或資料來源 &#40;報表產生器及 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [報表產生器選項 對話方塊中，設定&#40;報表產生器&#41;](report-builder/set-default-options-for-report-builder.md)   
 [報表產生器中的資料連接、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [加入及驗證資料連接或資料來源&#40;報表產生器及 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
  
