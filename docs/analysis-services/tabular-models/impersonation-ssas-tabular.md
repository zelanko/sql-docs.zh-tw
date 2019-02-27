---
title: Analysis Services 表格式模型中的模擬 |Microsoft Docs
ms.date: 01/21/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 981b98523a53e0c828de5e9cdf8a6c35c6843805
ms.sourcegitcommit: c3b190f8f87a4c80bc9126bb244896197a6dc453
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852903"
---
# <a name="impersonation"></a>模擬 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  這篇文章會提供表格式模型作者了解如何登入認證使用 Analysis Services 連接到資料來源時匯入和處理 （重新整理） 資料。  

##  <a name="bkmk_conf_imp_info"></a> 設定模擬  
 內容在何處，以及有同名的模型，以決定如何設定模擬資訊。 建立新的模型專案時，模擬被設定在 SQL Server Data Tools (SSDT)，當您連接到資料來源匯入資料。 一旦部署模型時，可以設定模擬模型資料庫連接字串屬性中使用 SQL Server Management Studio (SSMS)。 Azure Analysis Services 中的表格式模型，您可以使用 SSMS 或**檢視：指令碼**瀏覽器為基礎的設計工具在編輯 JSON 的 Model.bim 檔案中的模式。
  
##  <a name="bkmk_how_imper"></a> 模擬的使用方式  
 *「模擬」* (Impersonation) 是伺服器應用程式 (例如 Analysis Services) 假設用戶端應用程式身分識別的功能。 可以執行 analysis Services 會使用執行的服務帳戶，不過，伺服器建立的資料來源，連接時，它會使用模擬，以便進行資料匯入和處理的存取檢查。  
  
 用於模擬的認證會與您目前登入使用的認證不同。 製作模型時，登入使用者認證會用於特定的用戶端作業。  
  
 請務必了解如何模擬認證會指定並保護，以及內容中的兩個您帶正負號之間的差異在使用使用者認證，並使用其他的模擬認證時。  
  
 **了解伺服器端認證**  
 
當資料匯入或處理時，會使用模擬認證來連接到資料來源並提取資料。 此連線*伺服器端*因為主控工作空間資料庫的 Analysis Services 伺服器連接到資料來源並提取資料，用戶端應用程式的內容中執行的作業。  
  
 當您將模型部署到 Analysis Services 伺服器時，如果工作空間資料庫在部署模型時位於記憶體中，就會將認證傳遞到部署模型所在的 Analysis Services 伺服器。 使用者認證不會儲存在磁碟上。  
  
 當已部署的模型處理從資料來源的資料時，，保存在記憶體中資料庫中，會使用模擬認證來連接到資料來源並提取資料。 此程序由管理模型資料庫的 Analysis Services 伺服器，因為此連線是一次在伺服器端作業。  
  
 **了解用戶端認證**  
  
 當製作新模型，或將資料來源新增至現有的模型，您連接到資料來源並選取要匯入至模型資料表和檢視。 在 資料表匯入精靈 或 取得 Data\Query 設計工具預覽和篩選功能，您會看到您匯入之資料的範例。 您也可以指定篩選器，以排除不需要在模型中的資料。  
  
 同樣地，針對已建立的現有模型，您使用**表格內容**對話方塊來預覽和篩選的資料匯入資料表。  
  
 預覽和篩選功能，**表格內容**，和**Partition Manager**對話方塊是同處理序*用戶端*作業; 也就是說，在此做些什麼作業從資料來源連接至的方式不同，而且會從資料來源; 擷取的資料在伺服器端作業。 用來預覽和篩選資料的認證是使用者目前登入的認證。 事實上，您的認證。 
  
 認證的區隔用於伺服器端和用戶端作業可能會導致您所看到的內容，並在匯入或處理程序 （伺服器端作業） 期間會擷取哪些資料不相符。 如果認證您目前登入而指定的模擬認證不同，資料您看到 [預覽和篩選] 功能中的**表格內容**對話方塊，並匯入期間所提取的資料或處理程序可能會有所不同，資料來源所需的認證。  
  
> [!IMPORTANT]  
>  當製作模型時，請確定您登入的認證和針對模擬所指定的認證具有足夠的權限，以從資料來源擷取資料。
  
##  <a name="bkmk_imp_info_options"></a> 選項。  
 設定模擬時，或編輯現有的資料來源連接屬性時，指定下列選項之一：  
  
**表格式 1400年和更新版本的模型**
 
|選項|描述|  
|------------|-----------------|  
|**模擬帳戶**|指定模型使用的 Windows 使用者帳戶匯入或處理來自資料來源的資料。 網域和使用者帳戶的名稱使用下列格式：**\<網域名稱 >\\< 使用者帳戶名稱\>**。|  
|**模擬目前的使用者**|指定應該從資料來源使用的傳送要求之使用者的身分識別存取資料。 此設定僅適用於 DirectQuery 模式。|  
|**模擬身分識別**|指定要存取資料來源的使用者名稱，但不需要指定帳戶的密碼。 只有在已啟用 Kerberos 委派，並指定應該使用 S4U 驗證時，適用於這項設定。|  
|**模擬服務帳戶**|指定模型使用與管理模型的 Analysis Services 服務執行個體相關聯的安全性認證。|  
|**模擬無人看管的帳戶**|指定 Analysis Services 引擎應使用預先設定無人看管的帳戶來存取資料。|  

> [!IMPORTANT]
> 模擬在某些環境中不支援目前的使用者。 模擬部署到 Azure Analysis Services 連接到內部部署資料來源的表格式模型不支援目前的使用者。 Azure Analysis Services 伺服器資源不會連線到組織的網域中，因為無法針對該網域中的資料來源伺服器驗證用戶端認證。 Azure Analysis Services 也沒有目前與整合 (Azure) 的 SQL Database 支援，讓單一登入 (SSO)。 根據您的環境中，其他的模擬設定也會有限制。 當嘗試使用不支援的模擬設定，則會傳回錯誤。 


**表格式 1200年模型**
 
|選項|描述|  
|------------|-----------------|  
|**特定的 Windows 使用者名稱和密碼**|此選項會指定模型使用 Windows 使用者帳戶匯入或處理來自資料來源的資料。 網域和使用者帳戶的名稱使用下列格式：**\<網域名稱 >\\< 使用者帳戶名稱\>**。 建立新模型，使用 [資料表匯入精靈] 時，此設定會是預設選項。|  
|**服務帳戶**|此選項會指定模型使用與管理該模型之 Analysis Services 服務執行個體相關聯的安全性認證。|  
  
##  <a name="bkmk_impers_sec"></a> 安全性  
 搭配模擬使用的認證會保存在記憶體中 VertiPaq™ 引擎。 認證會永遠不會寫入至磁碟。 如果工作空間資料庫不是記憶體中，在部署模型時，系統會提示使用者輸入用來連接到資料來源並提取資料的認證。  
  
> [!NOTE]  
>  建議您針對模擬認證指定 Windows 使用者帳戶和密碼。 Windows 使用者帳戶可以設定為使用連接到和從資料來源讀取資料所需的最低權限。  
  

  
## <a name="see-also"></a>另請參閱  
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [表格式模型解決方案部署](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
