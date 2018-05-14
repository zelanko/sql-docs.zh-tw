---
title: 方法 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f42c986f8ebb3be2126335663a0716049e908ab0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="xml-elements---methods"></a>XML 項目-方法
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  XML for Analysis (XMLA) 通訊協定會使用兩種方法，**探索**和**Execute**來提供存取資訊的執行個體上的應用程式的標準方式[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 由於這些方法是使用簡易物件存取通訊協定 (SOAP) 叫用的，因此它們會接受使用 XML 格式的輸入並以 XML 格式傳遞輸出。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會遵照 XML for Analysis 1.1 規格來實作這兩種方法。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題將描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所實作的 XMLA 方法。  
  
|方法|Description|  
|------------|-----------------|  
|[Discover 方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體中擷取資訊，例如可用資料庫的清單或有關特定物件的詳細資料。 與擷取的資料**探索**方法取決於參數傳遞給它的值。|  
|[Execute 方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|將 XMLA 命令傳送至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 這包括涉及資料傳輸的要求，例如擷取或更新伺服器資料的要求。|  
  
## <a name="see-also"></a>另請參閱  
 [XML 項目 & #40;XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML 資料類型 & #40;XMLA & #41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML 項目 & #40;XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
