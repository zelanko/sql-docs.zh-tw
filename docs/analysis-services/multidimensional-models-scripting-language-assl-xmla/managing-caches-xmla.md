---
title: 管理快取 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1080db165770b414d15e4ffb43daf5466021a71a
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147053"
---
# <a name="managing-caches-xmla"></a>管理快取 (XMLA)
  您可以使用[ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla) XML for Analysis (XMLA) 以清除指定的維度或是資料分割的快取中的命令。 清除快取會強制[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]重建該物件的快取。  
  
## <a name="specifying-objects"></a>指定物件  
 [物件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性**ClearCache**命令可以包含只針對下列物件的其中一個物件參考。 如果物件參考不是用於下列其中一個物件，就會發生錯誤：  
  
 [資料庫]  
 針對資料庫中包含的所有維度與資料分割清除快取。  
  
 維度  
 清除指定維度的快取。  
  
 Cube  
 針對 Cube 量值群組中包含的所有資料分割清除快取。  
  
 量值群組  
 針對量值群組中包含的所有資料分割清除快取。  
  
 資料分割  
 清除指定資料分割的快取。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
