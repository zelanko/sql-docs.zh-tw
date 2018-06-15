---
title: 使用 Analysis Services 開發指令碼語言 (ASSL) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d1c01f567599353d360d8cf4a213e2abaa6c6cff
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025835"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>使用 Analysis Services 指令碼語言 (ASSL) 開發
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services 指令碼語言 (ASSL) 是 XMLA 的延伸模組，它會加入物件定義語言和命令語言，以便直接在伺服器上建立及管理 Analysis Services 結構。 您可以在自訂應用程式中使用 ASSL，以便透過 XMLA 通訊協定與 Analysis Services 通訊。 ASSL 是由兩個部分所組成：  
  
-   資料定義語言 (DDL) 或是物件定義語言會定義及描述 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體，以及執行個體包含的資料庫與資料庫物件。  
  
-   命令語言，例如傳送動作命令**建立**， **Alter**，或**程序**，Analysis Services 執行個體。 這個命令語言述[XML for Analysis &#40;XMLA&#41;參考](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)。  
  
 若要檢視在 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 中描述多維度方案的 ASSL，您可以在專案層級使用 [檢視程式碼] 命令。 您也可以在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 中使用 XMLA 查詢編輯器來建立或編輯 ASSL 指令碼。 您建立的指令碼可在伺服器上用來管理物件或執行命令。  
  
## <a name="see-also"></a>另請參閱  
 [ASSL 物件和物件特性](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)   
 [ASSL XML 慣例](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-xml-conventions.md)   
 [資料來源和繫結 & #40;SSAS 多維度 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
