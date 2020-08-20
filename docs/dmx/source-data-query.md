---
description: '&lt;來源資料查詢&gt;'
title: '&lt;來源資料查詢 &gt; |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fedb3472755a8147e10aef046c7a7fc435b356cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500758"
---
# <a name="ltsource-data-querygt"></a>&lt;來源資料查詢&gt;
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  若要訓練資料採礦模型並從採礦模型建立預測，您必須存取資料庫外部的資料 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 您可以 \<source data query> 在資料採礦延伸模組 (DMX) 中使用子句來定義此外部資料。 [插入 &#40;dmx&#41;](../dmx/insert-into-dmx.md)中，[從 &#60;模型中選取&#62; 預測聯結 &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)，然後[選取 [從自然預測聯結](../dmx/select-from-model-prediction-join-dmx.md)語句全部使用] **\<source data query>** 。  
  
## <a name="query-types"></a>查詢類型  
 指定來源資料的三種最常見的方式為：  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 這個陳述式會使用現有的資料來源，查詢 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之外的資料。  
  
 雖然 **openquery** 在函數中類似于 **OPENROWSET**，但是 **openquery** 有下列優點：  
  
-   使用 **OPENQUERY**可以更輕鬆地撰寫 DMX 查詢。 您不必在每次撰寫查詢時建立新的連接字串，可以利用資料來源中現有的連接字串。 資料來源物件也可以控制個別使用者的資料存取。  
  
-   管理員對於伺服器上之資料的存取方式，有更大的控制權。 例如，管理員可以管理哪些提供者會載入伺服器，以及可以存取哪些外部資料。  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 這個陳述式會使用現有的資料來源，查詢 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之外的資料。  
  
 [DMX&#41;圖形 &#40;](../dmx/source-data-query-shape.md)  
 這個陳述式會查詢多重資料來源，以建立巢狀資料表。 藉由使用 **圖形**，您可以將多個來源的資料結合成單一階層式資料表。 這可以讓您利用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的能力將資料表內嵌在資料表中，建立巢狀資料表。  
  
 若要指定來源資料，您也可以使用下列選項：  
  
-   任何有效的 DMX 陳述式  
  
-   任何有效的多維度運算式 (MDX) 陳述式  
  
-   傳回預存程序的資料表  
  
-   XML for Analysis (XMLA) 資料列集  
  
-   資料列集參數  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;Analysis Services 資料採礦&#41;的嵌套資料表 ](https://docs.microsoft.com/analysis-services/data-mining/nested-tables-analysis-services-data-mining)  
  
  
