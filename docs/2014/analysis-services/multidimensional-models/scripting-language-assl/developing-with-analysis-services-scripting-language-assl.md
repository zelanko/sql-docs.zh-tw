---
title: 使用 Analysis Services 指令碼語言（ASSL）進行開發 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services Scripting Language
- ASSL
ms.assetid: ce9aca4d-b7ad-451e-bb7f-20c2b0c03f29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dfdce0d0db35d651d12670ffd3cb1c9437961cd1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62736513"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>使用 Analysis Services 指令碼語言 (ASSL) 開發
  Analysis Services 指令碼語言 (ASSL) 是 XMLA 的延伸模組，它會加入物件定義語言和命令語言，以便直接在伺服器上建立及管理 Analysis Services 結構。 您可以在自訂應用程式中使用 ASSL，以便透過 XMLA 通訊協定與 Analysis Services 通訊。 ASSL 是由兩個部分所組成：  
  
-   資料定義語言 (DDL) 或是物件定義語言會定義及描述 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體，以及執行個體包含的資料庫與資料庫物件。  
  
-   將動作命令 (例如 `Create`、`Alter` 或 `Process`) 傳送到 Analysis Services 執行個體的命令語言。 [XML for Analysis &#40;XMLA&#41; 參考](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)中會討論此命令語言。  
  
 若要檢視在 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 中描述多維度方案的 ASSL，您可以在專案層級使用 [檢視程式碼] 命令。 您也可以在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 中使用 XMLA 查詢編輯器來建立或編輯 ASSL 指令碼。 您建立的指令碼可在伺服器上用來管理物件或執行命令。  
  
## <a name="see-also"></a>另請參閱  
 [ASSL 物件和物件特性](assl-objects-and-object-characteristics.md)   
 [ASSL XML 慣例](assl-xml-conventions.md)   
 [資料來源和繫結 &#40;SSAS 多維度&#41;](../data-sources-and-bindings-ssas-multidimensional.md)  
  
  
