---
title: '&lt;來源資料查詢&gt; |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e523d33da502a971b950e33ec0bd935149ed26f7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892347"
---
# <a name="ltsource-data-querygt"></a>&lt;來源資料查詢&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  若要將資料採礦模型定型並從「採礦模型」建立預測，您必須存取資料庫外部的[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資料。 您可以使用\<資料採礦延伸模組（DMX）中的來源資料查詢> 子句來定義此外部資料。 [插入 &#40;dmx&#41;](../dmx/insert-into-dmx.md)、[從 &#60;模型中選取&#62; 預測聯結 &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)，然後[從自然預測聯結](../dmx/select-from-model-prediction-join-dmx.md)語句中選取 [全部使用** \<來源資料查詢>**]。  
  
## <a name="query-types"></a>查詢類型  
 指定來源資料的三種最常見的方式為：  
  
 [&#40;DMX&#41;的 OPENQUERY](../dmx/source-data-query-openquery.md)  
 這個陳述式會使用現有的資料來源，查詢 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之外的資料。  
  
 雖然**openquery**在 Function to **OPENROWSET**中很類似，但**openquery**具有下列優點：  
  
-   DMX 查詢更容易使用**OPENQUERY**撰寫。 您不必在每次撰寫查詢時建立新的連接字串，可以利用資料來源中現有的連接字串。 資料來源物件也可以控制個別使用者的資料存取。  
  
-   管理員對於伺服器上之資料的存取方式，有更大的控制權。 例如，管理員可以管理哪些提供者會載入伺服器，以及可以存取哪些外部資料。  
  
 [&#40;DMX&#41;的 OPENROWSET](../dmx/source-data-query-openrowset.md)  
 這個陳述式會使用現有的資料來源，查詢 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之外的資料。  
  
 [SHAPE &#40;DMX&#41;](../dmx/source-data-query-shape.md)  
 這個陳述式會查詢多重資料來源，以建立巢狀資料表。 藉由使用 [**圖形**]，您可以將多個來源的資料結合成單一階層式資料表。 這可以讓您利用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的能力將資料表內嵌在資料表中，建立巢狀資料表。  
  
 若要指定來源資料，您也可以使用下列選項：  
  
-   任何有效的 DMX 陳述式  
  
-   任何有效的多維度運算式 (MDX) 陳述式  
  
-   傳回預存程序的資料表  
  
-   XML for Analysis (XMLA) 資料列集  
  
-   資料列集參數  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [Analysis Services 資料採礦&#41;的嵌套資料表 &#40;](https://docs.microsoft.com/analysis-services/data-mining/nested-tables-analysis-services-data-mining)  
  
  
