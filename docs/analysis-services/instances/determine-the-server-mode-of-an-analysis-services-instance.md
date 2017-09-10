---
title: "判斷伺服器模式的 Analysis Services 執行個體 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e556fb1-ca37-4f06-8f8f-f187cb0fdb37
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 74951b1fd998740bff623f93685f7ee98155c595
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="determine-the-server-mode-of-an-analysis-services-instance"></a>判斷 Analysis Services 執行個體的伺服器模式
  Analysis Services 可安裝為以下三種伺服器模式之一：多維度和資料採礦 (預設模式)、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，以及表格式。 Analysis Services 執行個體的伺服器模式是在安裝期間您選擇安裝伺服器選項時決定。  
  
 伺服器模式決定您所建立和部署的方案類型。 如果您沒有安裝伺服器軟體並且想要知道伺服器的安裝模式，可以使用本主題中的資訊來判斷模式。 如需特定模式下功能可用性的詳細資訊，請參閱[比較表格式和多維度解決方案 &#40;SSAS&#41;](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)。  
  
 如果您不要使用所安裝的伺服器模式，則必須解除安裝，然後選擇偏好的模式並重新安裝軟體。 或者，您可以在同一部電腦上安裝 Analysis Services 的其他執行個體，以便讓多個執行個體執行不同模式。  
  
## <a name="server-icons-in-object-explorer"></a>物件總管中的伺服器圖示  
 判斷伺服器模式最簡單的方法是在 SQL Server Management Studio 中連接到伺服器，並且在物件總管中注意伺服器名稱旁的圖示。 下圖顯示以多維度、表格式和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模式部署的三個 Analysis Services 執行個體：  
  
 ![物件總管圖示，每個伺服器模式](../../analysis-services/instances/media/ssas-ssms-servermodes.gif "每種伺服器模式的物件總管圖示")  
  
## <a name="viewing-deploymentmode-property-in-msmdsrvini-file"></a>檢視 MSMDSRV.INI 檔案中的 DeploymentMode 屬性  
 或者，您可以在每個 Analysis Services 執行個體中的 msmdsrv.ini 檔案檢查 **DeploymentMode** 屬性。 此屬性的值會識別伺服器模式。 有效值為 0 (多維度)、1 (SharePoint) 或 2 (表格式)。 您必須是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 系統管理員 (亦即伺服器角色的成員)，才能開啟 msmdsrv.ini 檔案。 此檔案包含結構化 XML。 您可以使用記事本或任何文字編輯器來檢視此檔案。  
  
> [!CAUTION]  
>  請不要變更 **DeploymentMode** 屬性的值。 不支援在安裝伺服器後手動變更此屬性。  
  
## <a name="about-the-deploymentmode-property"></a>關於 DeploymentMode 屬性  
 **DeploymentMode** 屬性會判斷 Analysis Services 伺服器執行個體的運作內容。 此屬性在對話方塊、訊息和文件集中稱為「伺服器模式」。 此屬性是由安裝程式根據您安裝 Analysis Services 的方式初始化。 此屬性應該僅被視為內部屬性，永遠使用安裝程式所指定的值。  
  
 這個屬性的有效值包括：  
  
|Value|描述|  
|-----------|-----------------|  
|0|這是預設值。 它指定多維度模式，用於服務使用 MOLAP、HOLAP 和 ROLAP 儲存以及資料採礦模型的多維度資料庫。|  
|1|指定要與 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署一起安裝的 Analysis Services 執行個體。 請不要變更 Analysis Services 執行個體的部署模式屬性，因為它是屬於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝的一部分。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 如果您變更模式，資料將不再於伺服器上執行。|  
|2|指定用於裝載使用記憶體中儲存或 DirectQuery 儲存之表格式模型資料庫的表格式模式。|  
  
 每個模式彼此之間是獨佔的。 設定為表格式模式的伺服器無法執行包含 Cube 和維度的 Analysis Services 資料庫。 如果基礎電腦硬體可以支援它，您就可以在相同的電腦上安裝多個 Analysis Services 執行個體，並將每個執行個體設定為使用不同的部署模式。 請記住，Analysis Services 是非常耗用資源的應用程式。 建議在相同的系統上，僅針對高階伺服器部署多個執行個體。  
  
## <a name="see-also"></a>請參閱＜  
 [安裝 Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)   
 [以多維度及資料採礦模式安裝 Analysis Services](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Power Pivot for SharePoint 2010 安裝](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)   
 [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)   
 [表格式模型方案 &#40;SSAS 表格式 &#41;](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)   
 [多維度模型方案 &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [採礦模型 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
