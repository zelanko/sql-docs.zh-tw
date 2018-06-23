---
title: 多維度模型中的 cube |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- OLAP objects [Analysis Services], cubes
- cubes [Analysis Services], about cubes
- cubes [Analysis Services]
- OLAP [Analysis Services], cubes
ms.assetid: e0f7acf3-4b07-41fc-a5fc-ac30b4a56c54
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4c32903245da975c9a62d6b7600abbe074b19bc2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023894"
---
# <a name="cubes-in-multidimensional-models"></a>多維度模型中的 Cube
  Cube 是包含用於分析之資訊的多維度結構；Cube 主要由維度和量值構成。 維度定義 Cube 的結構 (可進一步切割資料)，而量值提供使用者感興趣的彙總數值。 如同邏輯結構，Cube 允許用戶端應用程式擷取 (量值的) 值，就如同值包含在 Cube 的資料格中一樣；資料格是為每個可能的摘要值所定義。 Cube 中的資料格是由維度成員的交集所定義，並且包含該特定交集處之量值的彙總值。  
  
## <a name="benefits-of-using-cubes"></a>使用 Cube 的優點  
 Cube 提供儲存所有相關資料以進行分析的單一位置。  
  
## <a name="components-of-cubes"></a>Cube 的元件  
 Cube 是由下列元件構成：  
  
|元素|描述|  
|-------------|-----------------|  
|維度|[多維度模型中的維度](dimensions-in-multidimensional-models.md)|  
|量值和量值群組|[多維度模型中建立量值和量值群組](create-measures-and-measure-groups-in-multidimensional-models.md)|  
|資料分割|[多維度模型中的資料分割](partitions-in-multidimensional-models.md)|  
|「檢視方塊」|[多維度模型中的檢視方塊](perspectives-in-multidimensional-models.md)|  
|階層|[建立使用者定義階層](user-defined-hierarchies-create.md)|  
|動作|[多維度模型中的動作](actions-in-multidimensional-models.md)|  
|關鍵效能指標 (KPI)|[關鍵效能指標&#40;Kpi&#41;多維度模型中](key-performance-indicators-kpis-in-multidimensional-models.md)|  
|[新增命名集]|[多維度模型中的計算](calculations-in-multidimensional-models.md)|  
|翻譯|[多維度模型中的翻譯](translations-in-multidimensional-models-analysis-services.md)|  
  
## <a name="related-tasks"></a>相關工作  
  
|主題|描述|  
|-----------|-----------------|  
|[使用 Cube 精靈建立 Cube](create-a-cube-using-the-cube-wizard.md)|描述如何使用 Cube 精靈來定義 Cube、維度、維度屬性和使用者自訂階層。|  
|[多維度模型中建立量值和量值群組](create-measures-and-measure-groups-in-multidimensional-models.md)|描述如何定義量值群組。|  
|[多維度模型中的計算](calculations-in-multidimensional-models.md)|描述如何定義及設定 MDX 指令碼中的計算。|  
|[多維度模型中的動作](actions-in-multidimensional-models.md)|描述如何定義及設定動作。|  
|[多維度模型中的檢視方塊](perspectives-in-multidimensional-models.md)|描述如何定義及設定檢視方塊。|  
|[定義預存程序](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|描述如何使用預存程序。|  
  
  