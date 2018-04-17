---
title: 通過個人化擴充 OLAP |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Services, extensibility
ms.assetid: 348e49fc-4390-43c1-9b6c-61b386ff4373
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6d79c5755acb987452b96324518aa875f1920d8a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="extending-olap-through-personalizations"></a>通過個人化擴充 OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Analysis Services 提供許多內建函式的多維度運算式 (MDX) 和資料採礦延伸模組 (DMX) 語言搭配使用。 這些函數是設計用來進行標準統計計算與階層中周遊成員間等工作。 不過，就如同其他複雜且功能強大的產品一樣，總是有進一步擴充產品功能的需求。  
  
 因此，Analysis Services 可讓您將組件和個人化的延伸模組加入到服務的執行個體，在標準功能不足時，完成您的商務需求。  
  
## <a name="assemblies"></a>組件  
 組件可以讓您延伸 MDX 和 DMX 的商務功能。 您可以將想要的功能建立成程式庫 (例如動態連結程式庫 (DLL))，然後將該程式庫當成組件加入 Analysis Services 執行個體或 Analysis Services 資料庫中。 程式庫中的公用方法便公開給 MDX 和 DMX 運算式、程序、計算、動作，以及用戶端應用程式，作為使用者自訂函數。  
  
## <a name="personalized-extensions"></a>個人化的延伸模組  
 SQL Server Analysis Services 個人化延伸模組是實作外掛程式架構之概念的基礎。 Analysis Services 個人化延伸模組是比現有 Managed 組件架構更簡單精緻的版本，會在整個 Analysis Services <xref:Microsoft.AnalysisServices.AdomdServer> 物件模型、多維度運算式 (MDX) 語法和結構描述資料列集中公開。  
  
## <a name="see-also"></a>請參閱  
 [多維度模型組件管理](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Analysis Services 個人化延伸模組](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
  
