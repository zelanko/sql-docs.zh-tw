---
title: 選取建立方法 （Cube 精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubewizard.cubedefinition.f1
ms.assetid: 985d3b5b-7891-465b-862d-f7e75431b342
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 48a6ef3849e91f606cb94ae7fa1f7c67817bfff7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152801"
---
# <a name="select-creation-method-cube-wizard"></a>選取建立方法 (Cube 精靈)
  使用 **[選取建立方法]** 頁面，即可指定建立 Cube 的方式。  
  
## <a name="options"></a>選項。  
 **使用現有的資料表**  
 選取此選項，即可使用資料來源中的現有資料表來建立 Cube。 這個精靈將引導您完成根據現有資料表選取並定義量值群組和維度，以便建立新 Cube 的程序。  
  
 **建立空白 cube**  
 選取此選項，即可建立空白的 Cube。 當您想要手動建立所有項目，或者 Cube 中的所有量值群組都是連結的量值群組時，這個選項就很有用。  
  
> [!NOTE]  
>  只有當您使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案時，才能使用這個選項，但是當您直接連接至 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫時，則無法使用這個選項。  
  
 **資料來源中建立資料表**  
 選取此選項，即可先建立 Cube，然後根據 Cube 定義，在資料來源中產生新的資料表。  
  
> [!NOTE]  
>  若要使用這個選項，您必須擁有在基礎資料來源中建立物件的權限。  
  
 選取此選項將使 **[範本]** 選項成為可用。  
  
 **範本**  
 選取您想要用來建立 Cube 的範本。 範本會提供一組以特定商業用途為目標的定義。  
  
> [!NOTE]  
>  只有在您已經選取 [在資料來源中建立資料表] 時，才能使用這個選項。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 物件&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [多維度模型中的 cube](multidimensional-models/cubes-in-multidimensional-models.md)   
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
