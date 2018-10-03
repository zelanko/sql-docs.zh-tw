---
title: 方法 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1e073eae6637b726a473ea7bf95057ed1548982
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088588"
---
# <a name="methods-xmla"></a>方法 (XMLA)
  XML for Analysis (XMLA) 通訊協定會使用兩個方法：`Discover`並`Execute`，以提供標準的方式，讓應用程式存取的執行個體上的資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 由於這些方法是使用簡易物件存取通訊協定 (SOAP) 叫用的，因此它們會接受使用 XML 格式的輸入並以 XML 格式傳遞輸出。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會遵照 XML for Analysis 1.1 規格來實作這兩種方法。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題將描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所實作的 XMLA 方法。  
  
|方法|描述|  
|------------|-----------------|  
|[探索方法&#40;XMLA&#41;](xml-elements-methods-discover.md)|從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體中擷取資訊，例如可用資料庫的清單或有關特定物件的詳細資料。 使用 `Discover` 方法所擷取的資料取決於傳遞給它的參數值。|  
|[Execute 方法&#40;XMLA&#41;](xml-elements-methods-execute.md)|將 XMLA 命令傳送至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 這包括涉及資料傳輸的要求，例如擷取或更新伺服器資料的要求。|  
  
## <a name="see-also"></a>另請參閱  
 [XML 項目&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [XML 資料型別&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [XML 項目&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  
