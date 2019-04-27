---
title: 模擬 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cb44454c12dec173e586fd2a94d0147dfde01eef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757247"
---
# <a name="impersonation-ssas-tabular"></a>模擬 (SSAS 表格式)
  本主題讓表格式模型作者了解連接到資料來源匯入與處理 (重新整理) 資料時，Analysis Services 如何使用登入認證。  
  
 本文包含下列各節：  
  
-   [優點](#bkmk_how_imper)  
  
-   [選項。](#bkmk_imp_info_options)  
  
-   [Security](#bkmk_impers_sec)  
  
-   [匯入模型模擬](#bkmk_imp_newmodel)  
  
-   [設定模擬](#bkmk_conf_imp_info)  
  
##  <a name="bkmk_how_imper"></a> 優點  
 *「模擬」* (Impersonation) 是伺服器應用程式 (例如 Analysis Services) 假設用戶端應用程式身分識別的功能。 Analysis Services 會使用服務帳戶執行，不過，當伺服器建立與資料來源的連接時，它會使用模擬，以便執行用於資料匯入和處理的存取檢查。  
  
 用於模擬的認證與目前登入之使用者的認證不同。 製作模型時，已登入的使用者認證可用於特定的用戶端作業。  
  
 請務必了解如何模擬認證會指定並保護，以及目前登入使用者的認證以及使用其他認證時的內容之間的差異。  
  
 **了解伺服器端認證**  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，您可以使用 [資料表匯入精靈] 中的 [模擬資訊] 頁面，或在 [現有連接] 對話方塊中編輯現有的資料來源連接，藉以指定每個資料來源的認證。  
  
 匯入或處理資料時，在 [模擬資訊] 頁面中指定的認證會用來連接資料來源以及提取資料。 這是在用戶端應用程式的內容中執行的 *「伺服器端」*(server side) 作業，因為主控工作空間資料庫的 Analysis Services 伺服器會連接到資料來源並提取資料。  
  
 當您將模型部署到 Analysis Services 伺服器時，如果工作空間資料庫在部署模型時位於記憶體中，就會將認證傳遞到部署模型所在的 Analysis Services 伺服器。 使用者認證絕不會存放在磁碟上。  
  
 當部署的模型處理資料來源的資料時，保存在記憶體中資料庫的模擬認證會用來連接資料來源並提取資料。 此程序是由管理模型資料庫的 Analysis Services 伺服器所處理，因此這也是伺服器端作業。  
  
 **了解用戶端認證**  
  
 製作新模型或將資料來源加入至現有的模型時，您可以使用 [資料表匯入精靈] 連接到資料來源，然後選取要匯入到模型中的資料表和檢視表。 在 [資料表匯入精靈] 的 [選取資料表和檢視表] 頁面上，您可以使用 [預覽和篩選] 功能來檢視您要匯入之資料的範例 (限制為 50 個資料列)。 您也可以指定篩選，來排除不需要包含在模型中的資料。  
  
 同樣地，針對已經建立的現有模型，您可以使用 [編輯資料表屬性] 對話方塊來預覽並篩選匯入到資料表中的資料。 此處的預覽和篩選功能使用與 [資料表匯入精靈] 之 [選取資料表和檢視表] 頁面上的 [預覽和篩選] 功能相同的功能。  
  
 [預覽和篩選] 功能、[資料表屬性] 和 [資料分割管理員] 對話方塊是同處理序的 *「用戶端」*(Client Side) 作業，也就是說，在此作業期間完成的作業與連接資料來源和從資料來源提取資料的方式不同，後者是伺服器端作業。 用於預覽和篩選資料的認證就是目前登入之使用者的認證。 用戶端作業一律會使用目前使用者的 Windows 認證來連接到資料來源。  
  
 在伺服器端和用戶端作業期間使用不同的認證可能會導致使用者使用 [預覽和篩選] 功能或 [資料表屬性] 對話方塊所看到的內容 (用戶端作業)，與匯入或處理期間所提取的資料 (伺服器端作業) 不符。 如果目前登入之使用者的認證和指定的模擬認證不同，在 [預覽和篩選] 功能或 [資料表屬性] 對話方塊中所看到的資料以及在匯入或處理期間提取的資料，可能會根據資料來源所需要的認證而有所不同。  
  
> [!IMPORTANT]  
>  製作模型時，請確認目前登入之使用者的認證和針對模擬所指定的認證都有從資料來源提取資料的足夠權限。  
  
##  <a name="bkmk_imp_info_options"></a> 選項。  
 設定模擬時，或在 Analysis Services 中編輯現有資料來源連接的屬性時，您可以指定下列其中一個選項：  
  
|選項|ImpersonationMode<sup>1</sup>|描述|  
|------------|-----------------------------------|-----------------|  
|**特定的 Windows 使用者名稱和密碼** <sup>2</sup>|ImpersonateWindowsUserAccount|此選項會指定模型使用 Windows 使用者帳戶匯入或處理資料來源中的資料。 網域和使用者帳戶的名稱使用下列格式：**\<網域名稱 >\\< 使用者帳戶名稱\>**。 使用 [資料表匯入精靈] 建立新模型這是預設選項。|  
|**服務帳戶**|ImpersonateServiceAccount|此選項會指定模型使用與管理該模型之 Analysis Services 服務執行個體相關聯的安全性認證。|  
  
 <sup>1</sup>impersonationmode 會針對指定的值[DataSourceImpersonationInfo 元素&#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)資料來源上的屬性。  
  
 <sup>2</sup>時使用此選項時，如果工作空間資料庫已移除從記憶體中，由於重新開機或有**工作區保留**屬性設定為**從記憶體中的卸載**或**從工作區刪除**，而該模型專案是關閉，後續的工作階段中，如果您嘗試處理資料表的資料，將會提示您輸入每個資料來源的認證。 同樣地，如果部署的模型資料庫已從記憶體中移除，系統將提示您輸入每個資料來源的認證。  
  
##  <a name="bkmk_impers_sec"></a> Security  
 搭配模擬使用的認證是透過與管理工作空間資料庫或已部署模型之 Analysis Services 伺服器相關聯的 xVelocity 記憶體中分析引擎 (VertiPaq)™ 引擎，保存在記憶體中。  認證絕不會寫入到磁碟中。 如果工作空間資料庫在部署模型時不在記憶體中，系統將會提示使用者輸入用來連接資料來源並提取資料的認證。  
  
> [!NOTE]  
>  建議您針對模擬認證指定 Windows 使用者帳戶和密碼。 Windows 使用者帳戶可以設定為使用在資料來源中連接與讀取資料所需的最低權限。  
  
##  <a name="bkmk_imp_newmodel"></a> 匯入模型模擬  
 PowerPivot 不像可以使用數個不同模擬模式支援跨處理序資料收集的表格式模型，前者僅使用一個模式，也就是 ImpersonateCurrentUser。 由於 PowerPivot 一律執行同處理序，因此它會使用目前登入之使用者的認證，連接到資料來源。 使用表格式模型時，目前登入之使用者的認證僅能搭配 [資料表匯入精靈] 中的 [預覽和篩選] 功能，並在檢視 [資料表屬性] 時使用。 將資料匯入或處理到工作空間資料庫時，或將資料匯入或處理到已部署的模型時，會使用模擬認證。  
  
 匯入現有的 PowerPivot 活頁簿來建立新模型時，模型設計師預設會設定模擬使用服務帳戶 (ImpersonateServiceAccount)。 建議您變更模型上從 PowerPivot 匯入到 Windows 使用者帳戶的模擬認證。 已匯入 PowerPivot 活頁簿，並在模型設計師中建立新的模型之後，您可以使用來變更認證**現有的連線**對話方塊。  
  
 從 Analysis Services 伺服器上的現有模型匯入來建立新模型時，會將模擬認證從現有的模型資料庫傳遞到新的模型工作空間資料庫。 必要時，您可以在新模型上使用 [現有連接] 對話方塊來變更認證。  
  
##  <a name="bkmk_conf_imp_info"></a> 設定模擬  
 模型存在的位置及其內容，將會決定設定模擬資訊的方式。 針對在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中製作的模型，您可以在 [資料表匯入精靈] 的 [模擬資訊] 頁面上設定模擬資訊，或者透過編輯 [現有連接] 對話方塊上的資料來源連接來設定。 若要檢視現有連接，請在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的 [模型] 功能表上，按一下 [現有連接]。  
  
 針對部署到 Analysis Services 伺服器的模型，可以設定模擬資訊的省略符號 （...），即可**資料來源模擬資訊**屬性中的**資料庫屬性**對話方塊中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [DirectQuery 模式 &#40;SSAS 表格式&#41;](directquery-mode-ssas-tabular.md)   
 [資料來源 &#40;SSAS 表格式&#41;](../data-sources-ssas-tabular.md)   
 [表格式模型方案部署 &#40;SSAS 表格式&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
