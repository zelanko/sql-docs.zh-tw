---
title: '&lt;來源資料查詢&gt;|Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 83dbe0c2ea6eb066f208223acd2c6062f964fcf3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938081"
---
# <a name="ltsource-data-querygt"></a>&lt;來源資料查詢&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  若要培訓資料採礦模型，並從採礦模型建立預測，您必須存取資料的外部[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資料庫。 您使用\<來源資料查詢 > 子句中的資料採礦延伸模組 (DMX) 來定義這個外部的資料。 [插入&#40;DMX&#41;](../dmx/insert-into-dmx.md)， [FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)，並[SELECT FROM NATURAL PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)所有的陳述式會使用 **\<來源資料查詢 >** 。  
  
## <a name="query-types"></a>查詢類型  
 指定來源資料的三種最常見的方式為：  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 這個陳述式會使用現有的資料來源，查詢 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之外的資料。  
  
 雖然**OPENQUERY**是功能類似於**OPENROWSET**， **OPENQUERY**具有下列優點：  
  
-   DMX 查詢會更容易撰寫與**OPENQUERY**。 您不必在每次撰寫查詢時建立新的連接字串，可以利用資料來源中現有的連接字串。 資料來源物件也可以控制個別使用者的資料存取。  
  
-   管理員對於伺服器上之資料的存取方式，有更大的控制權。 例如，管理員可以管理哪些提供者會載入伺服器，以及可以存取哪些外部資料。  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 這個陳述式會使用現有的資料來源，查詢 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之外的資料。  
  
 [圖形&#40;DMX&#41;](../dmx/source-data-query-shape.md)  
 這個陳述式會查詢多重資料來源，以建立巢狀資料表。 藉由使用**圖形**，您可以將多個來源的資料合併成單一的階層式資料表。 這可以讓您利用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的能力將資料表內嵌在資料表中，建立巢狀資料表。  
  
 若要指定來源資料，您也可以使用下列選項：  
  
-   任何有效的 DMX 陳述式  
  
-   任何有效的多維度運算式 (MDX) 陳述式  
  
-   傳回預存程序的資料表  
  
-   XML for Analysis (XMLA) 資料列集  
  
-   資料列集參數  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組&#40;DMX&#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [巢狀資料表&#40;Analysis Services-資料採礦&#41;](../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  
