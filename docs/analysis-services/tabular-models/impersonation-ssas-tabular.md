---
title: "在 Analysis Services 表格式模型中的模擬 |Microsoft 文件"
ms.custom: 
ms.date: 10/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 128cadc90dd4c2fa76d8174e8537598ec805c027
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="impersonation"></a>模擬 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]本主題會提供表格式模型作者了解如何登入認證 Analysis services 連接時使用的資料來源匯入和處理 （重新整理） 資料。  

##  <a name="bkmk_conf_imp_info"></a>設定模擬  
 其中，而在有哪些內容可讓您決定設定模擬資訊的方式。 建立新的模型專案時，模擬被設定在 SQL Server Data Tools (SSDT)，當您連接到資料來源匯入資料。 一旦部署模型時，可以設定模擬模型資料庫連接字串屬性中使用 SQL Server Management Studio (SSMS)。 Azure Analysis Services 中的表格式模型，您可以使用 SSMS 或**以檢視： 指令碼**瀏覽器為基礎的設計工具在編輯 JSON Model.bim 檔案中的模式。
  
##  <a name="bkmk_how_imper"></a>模擬的使用方式  
 *「模擬」* (Impersonation) 是伺服器應用程式 (例如 Analysis Services) 假設用戶端應用程式身分識別的功能。 可以執行 analysis Services 會使用執行服務帳戶，不過，伺服器建立的資料來源，連接時，它會使用模擬，讓資料匯入和處理的存取檢查。  
  
 用於模擬的認證會與您目前登入使用的認證不同。 登入的認證會製作模型時使用特定的用戶端作業的使用者。  
  
 請務必了解如何模擬認證會指定上並保護，以及內容中的兩個您登入之間的差異會使用使用者認證，並使用其他的模擬認證時。  
  
 **了解伺服器端認證**  
 
當資料匯入或處理時，會使用模擬認證來連接到資料來源並提取資料。 這是*伺服器端*因為主控工作空間資料庫的 Analysis Services 伺服器連接到資料來源並提取資料的用戶端應用程式內容中執行的作業。  
  
 當您將模型部署到 Analysis Services 伺服器時，如果工作空間資料庫在部署模型時位於記憶體中，就會將認證傳遞到部署模型所在的 Analysis Services 伺服器。 使用者認證絕不會存放在磁碟上。  
  
 當已部署的模型處理從資料來源的資料時，保存在記憶體中資料庫的模擬認證可用來連接到資料來源並提取資料。 此程序由管理模型資料庫的 Analysis Services 伺服器，因為這是第一次是伺服器端作業。  
  
 **了解用戶端認證**  
  
 當製作新模型或資料來源加入至現有的模型，您連接到資料來源並選取要匯入模型資料表和檢視。 在 資料表匯入精靈 」 或 「 取得 Data\Query 設計工具預覽和篩選功能，您會看到您匯入資料的範例。 您也可以指定篩選，來排除不需要包含在模型中的資料。  
  
 同樣地，針對已經建立的現有模型，您使用**表格內容**對話方塊來匯入資料表的預覽和篩選資料。  
  
 預覽和篩選功能，**表格內容**，和**資料分割管理員**對話方塊是同處理序*用戶端*作業，也就是所完成的作業在此作業不同於資料來源連接至的方式，而且資料從資料來源; 提取伺服器端作業。 用於預覽和篩選資料的認證就是目前登入之使用者的認證。 事實上，您的認證。 
  
 認證的區隔用於伺服器端和用戶端作業可能會導致在您所看到的內容和匯入或處理序 （伺服器端作業） 期間擷取哪些資料不相符。 如果認證您目前登入使用，而且指定的模擬認證不同，資料所示的預覽和篩選功能或**表格內容**對話方塊，並匯入期間提取的資料或程序可能會根據資料來源所需的認證而不同。  
  
> [!IMPORTANT]  
>  當製作模型時，請確定您使用登入的認證和針對模擬所指定的認證具有足夠的權限，來從資料來源擷取資料。  
  
##  <a name="bkmk_imp_info_options"></a> 選項。  
 設定模擬時，或編輯現有的資料來源連接屬性時，指定下列選項：  
  
**1400 （含） 以上的表格式模型**
 
|選項|Description|  
|------------|-----------------|  
|**模擬帳戶**|指定模型使用的 Windows 使用者帳戶匯入或處理來自資料來源的資料。 網域和使用者帳戶的名稱使用下列格式：**\<網域名稱 >\\< 使用者帳戶名稱\>**。|  
|**模擬目前的使用者**|指定應該從資料來源使用的傳送要求之使用者的身分識別存取資料。 此模式僅適用於直接查詢模式。|  
|**模擬身分識別**|指定要存取資料來源的使用者名稱，但不需要指定帳戶的密碼。 已啟用 Kerberos 委派，且指定應該使用 S4U 驗證時，才適用這個模式。|  
|**模擬服務帳戶**|指定模型使用與管理模型之 Analysis Services 服務執行個體相關聯的安全性認證。|  
|**模擬無人看管的帳戶**|指定 Analysis Services 引擎應使用預先設定無人看管的帳戶來存取資料。|  


**表格式 1200年模型**
 
|選項|Description|  
|------------|-----------------|  
|**特定的 Windows 使用者名稱和密碼**|這個選項會指定模型使用 Windows 使用者帳戶匯入或處理來自資料來源的資料。 網域和使用者帳戶的名稱使用下列格式：**\<網域名稱 >\\< 使用者帳戶名稱\>**。 使用 [資料表匯入精靈] 建立新模型這是預設選項。|  
|**服務帳戶**|此選項會指定模型使用與管理該模型之 Analysis Services 服務執行個體相關聯的安全性認證。|  
  
##  <a name="bkmk_impers_sec"></a> 安全性  
 搭配模擬使用的認證會保存在記憶體中由 VertiPaq™ 引擎。 認證永遠不會寫至磁碟。 如果工作空間資料庫不是記憶體中，在部署模型時，就會提示使用者輸入用來連接到資料來源並提取資料的認證。  
  
> [!NOTE]  
>  建議您針對模擬認證指定 Windows 使用者帳戶和密碼。 Windows 使用者帳戶可以設定為使用連接到與來自資料來源讀取資料所需的最低權限。  
  

  
## <a name="see-also"></a>另請參閱  
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [資料來源](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [表格式模型方案部署](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
