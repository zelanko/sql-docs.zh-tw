---
title: 使用 Analysis Services 開發指令碼語言 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Analysis Services Scripting Language
- ASSL
ms.assetid: ce9aca4d-b7ad-451e-bb7f-20c2b0c03f29
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b68282f6327ac52cdf47bb761c764609292d7c3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185174"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>使用 Analysis Services 指令碼語言 (ASSL) 開發
  Analysis Services 指令碼語言 (ASSL) 是 XMLA 的延伸模組，它會加入物件定義語言和命令語言，以便直接在伺服器上建立及管理 Analysis Services 結構。 您可以在自訂應用程式中使用 ASSL，以便透過 XMLA 通訊協定與 Analysis Services 通訊。 ASSL 是由兩個部分所組成：  
  
-   資料定義語言 (DDL) 或是物件定義語言會定義及描述 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體，以及執行個體包含的資料庫與資料庫物件。  
  
-   將動作命令 (例如 `Create`、`Alter` 或 `Process`) 傳送到 Analysis Services 執行個體的命令語言。 這個命令語言會討論[XML for Analysis &#40;XMLA&#41;參考](../../xmla/xml-for-analysis-xmla-reference.md)。  
  
 若要檢視在 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 中描述多維度方案的 ASSL，您可以在專案層級使用 [檢視程式碼] 命令。 您也可以在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 中使用 XMLA 查詢編輯器來建立或編輯 ASSL 指令碼。 您建立的指令碼可在伺服器上用來管理物件或執行命令。  
  
## <a name="see-also"></a>另請參閱  
 [ASSL 物件和物件特性](assl-objects-and-object-characteristics.md)   
 [ASSL XML 慣例](assl-xml-conventions.md)   
 [資料來源和繫結&#40;SSAS 多維度&#41;](../data-sources-and-bindings-ssas-multidimensional.md)  
  
  
