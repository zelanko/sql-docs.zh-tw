---
title: 多維度模型方案部署 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e5f4b4f7f30ec9f94993e34596d348ae22842fd
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023955"
---
# <a name="multidimensional-model-solution-deployment"></a>多維度模型方案部署
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您完成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的開發之後，即可將資料庫部署至 Analysis Services 伺服器。 Analysis Services 提供六種可能的部署方法，可用來將資料庫移至測試伺服器或實際伺服器。 此處以優點的順序列出這些方法：AMO 自動化、XMLA、部署精靈、部署公用程式、同步處理精靈、備份與還原。  
  
 本主題包含下列各節：  
  
 [部署方法](#bkmk_meth)  
  
 [部署考量因素](#bkmk_considerations)  
  
 [相關工作](#bkmk_rel)  
  
##  <a name="bkmk_meth"></a> 部署方法  
  
|方法|說明|連結|  
|------------|-----------------|----------|  
|**分析管理物件 (AMO) 自動化**|AMO 提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]完整命令集的程式設計介面，包括可用於方案部署的命令。 AMO 自動化是方案部署的方法之一，雖然彈性最高，但是也需要撰寫程式。  使用 AMO 自動化的主要優點在於，您可以搭配 AMO 應用程式使用 SQL Server Agent，根據預設排程執行部署。|[使用分析管理物件 & #40; 開發AMO & #41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|**XMLA**|使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，即可針對現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中繼資料產生 XMLA 指令碼，然後在另一部伺服器上執行該指令碼來重新建立初始資料庫。 透過定義部署處理，然後在 XMLA 指令碼中編纂和儲存部署處理，可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中輕易地形成 XMLA 指令碼。 一旦儲存的檔案中具有 XMLA 指令碼後，您就可以輕易地根據排程來執行指令碼，或在直接連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的應用程式中內嵌指令碼。<br /><br /> 您也可以使用 SQL Server Agent，在預設的基礎上執行 XMLA 指令碼，但是使用 XMLA 指令碼的彈性不如 AMO。 AMO 會裝載完整的管理命令範圍，提供較廣泛的功能。|[使用 XMLA 部署模型方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**部署精靈**|使用 [部署精靈]，即可使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案產生的 XMLA 輸出檔來部署專案的中繼資料至目的地伺服器。 使用 [部署精靈] 時，您可以直接從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 檔案進行部署，如同由專案建置的輸出目錄所建立的一樣。<br /><br /> 使用 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 的主要優點在於其便利性。 就像是您可以儲存 XMLA 指令碼以供 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]稍後使用一樣，您也可以儲存 [部署精靈] 指令碼。 您可以透過部署公用程式，在命令提示字元處以互動方式執行 [部署精靈]。|[使用部署精靈部署模型方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**部署公用程式**|部署公用程式可讓您在命令提示字元之下啟動 Analysis Services 部署引擎。|[使用部署公用程式部署模型方案](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**同步處理資料庫精靈**|使用 [同步處理資料庫精靈]，即可同步處理任何兩個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫之間的中繼資料和資料。<br /><br /> [同步處理精靈] 可以從來源伺服器，將資料和中繼資料複製到目的地伺服器。 如果目的地伺服器沒有您要部署的資料庫複本，則會將新資料庫複製到目的地伺服器。 如果目的地伺服器已經有相同資料庫的複本，則會更新目的地伺服器上的資料庫，以使用來源資料庫的中繼資料和其他資料。|[同步處理 Analysis Services 資料庫](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)|  
|**備份與還原**|備份提供傳送 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫最簡單的方式。 從 [備份] 對話方塊，您可以設定選項的組態，並可隨後從對話方塊本身來執行備份。 或者，您可建立可依需求頻率來儲存和執行的指令碼。<br /><br /> 備份和還原不像其他部署方法一般常用，但卻是可在最小基礎結構需求內快速完成部署的方法。|[備份與還原 Analysis Services 資料庫](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_considerations"></a> 部署考量因素  
 在部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案之前，請先考量這些問題中的哪些問題適用於您的解決方案，然後檢閱相關連結，以了解對付問題的方法：  
  
|考量|詳細資訊連結|  
|-------------------|------------------------------|  
|這個解決方案需要什麼硬體和軟體資源？|[Analysis Services 部署的需求和考量](../../analysis-services/multidimensional-models/requirements-and-considerations-for-analysis-services-deployment.md)|  
|如何部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案範圍以外的相關物件，例如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝、報表或關聯式資料庫結構描述？||  
|如何在部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中載入和更新資料？<br /><br /> 如何在部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中更新中繼資料 (例如計算)？|本主題中的[部署方法](#bkmk_meth) 。|  
|您是否要授與使用者透過網際網路存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料的權限？|[設定 HTTP 存取 Analysis Services 上 Internet Information Services & #40; IIS & #41;8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|  
|您是否要提供對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料的連續查詢存取權限？|[Analysis Services 部署的需求和考量](../../analysis-services/multidimensional-models/requirements-and-considerations-for-analysis-services-deployment.md)|  
|您是否要使用連結物件或遠端分割區在分散式環境中部署物件？|[建立及管理本機資料分割 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)、[建立及管理遠端資料分割 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md) 和[連結量值群組](../../analysis-services/multidimensional-models/linked-measure-groups.md)。|  
|您如何保護 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料的安全？|[授權的存取權的物件和作業 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)|  
  
##  <a name="bkmk_rel"></a> 相關工作  
 [Analysis Services 部署的需求和考量](../../analysis-services/multidimensional-models/requirements-and-considerations-for-analysis-services-deployment.md)  
  
 [使用 XMLA 部署模型方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)  
  
 [使用部署精靈部署模型方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
 [使用部署公用程式部署模型方案](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  
