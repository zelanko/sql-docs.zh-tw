---
title: "外掛程式演算法 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- third-party algorithms [Analysis Services]
- algorithms [data mining], creating
- plugin algorithms [Analysis Services]
ms.assetid: fe364ddc-576e-42fc-9ced-baa399992f92
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3e2006e4d91906311b16e51b1b0b25d577c89387
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="plugin-algorithms"></a>外掛程式演算法
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]除了演算法， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供，有許多其他您可以使用資料採礦的演算法。 因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為協力廠商所建立的「外掛程式」演算法提供一項機制。 只要演算法遵循特定的標準，就可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 內使用，就像使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法一樣。 外掛程式演算法具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供的所有演算法功能。  
  
 如需 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用於與外掛程式演算法通訊之介面的完整描述，請參閱建立自訂演算法和自訂模型檢視器的範例，這些範例會在 [CodePlex](http://go.microsoft.com/fwlink/?LinkID=87843) 網站上發佈。  
  
## <a name="algorithm-requirements"></a>演算法需求  
 若要將演算法外掛至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，您必須實作下列 COM 介面：  
  
 **IDMAlgorithm**  
 實作會產生模型的演算法，並實作結果模型的預測作業。  
  
 **IDMAlgorithmNavigation**  
 允許瀏覽器存取模型的內容。  
  
 **IDMPersist**  
 允許 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]儲存和載入演算法定型的模型。  
  
 **IDMAlgorithmMetadata**  
 描述演算法的功能和輸入參數。  
  
 **IDMAlgorithmFactory**  
 為實作演算法介面的物件建立執行個體，並允許 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 存取演算法中繼資料介面。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用這些 COM 介面與外掛程式演算法通訊。 雖然您使用的外掛程式演算法必須支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB for Data Mining 規格，但不必支援該規格中的所有資料採礦選項。 您可以使用 [MINING_SERVICES](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md) 結構描述資料列集，來決定演算法的功能。 此結構描述資料列集，會列出每一個外掛程式演算法提供者的資料採礦支援選項。  
  
 您必須先註冊新的演算法，才能與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]一起使用。 若要註冊演算法，請在您要包含演算法之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的 .ini 檔案中包含下列資訊：  
  
-   演算法名稱  
  
-   ProgID (這是選擇性，且只有外掛程式演算法才會包含)  
  
-   指出是否啟用演算法的旗標  
  
 下列程式碼範例說明如何註冊新的演算法：  
  
 `<ConfigurationSettings>`  
  
 `...`  
  
 `<DataMining>`  
  
 `...`  
  
 `<Algorithms>`  
  
 `...`  
  
 `<Sample_Plugin_Algorithm>`  
  
 `<Enabled>1</Enabled>`  
  
 `<ProgID>Microsoft.DataMining.SamplePlugInAlgorithm.Factory</ProgID>`  
  
 `</Sample_PlugIn_Algorithm>`  
  
 `...`  
  
 `</Algorithms>`  
  
 `...`  
  
 `</DataMining>`  
  
 `...`  
  
 `</ConfigurationSettings>`  
  
## <a name="see-also"></a>請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [DMSCHEMA_MINING_SERVICES 資料列集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)  
  
  
