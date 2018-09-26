---
title: 表格式模型 |Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1f894ad30f6344eb832cb9549a60c7f60071188c
ms.sourcegitcommit: e34e9cd1b1ec02393dc88b1f0471023a7f7f278b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506128"
---
# <a name="tabular-models"></a>表格式模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Analysis Services 中的表格式模型是記憶體中或在 DirectQuery 模式中，連接到資料直接從後端關聯式資料來源執行的資料庫。 藉由使用的新狀態壓縮演算法和多執行緒的查詢處理器，Analysis Services Vertipaq 分析引擎，提供快速存取透過報表用戶端應用程式，Power BI 和 Excel 等表格式模型物件和資料。  
  
 記憶體中模型都是預設值，DirectQuery 是替代的查詢模式的模型，不是太大而無法放在記憶體中，或資料的變動程度不適合進行合理處理策略。 DirectQuery 可達到同位檢查的記憶體中模型，透過各式各樣的資料來源，能夠處理導出的資料表和資料行，在 DirectQuery 模型中，透過連線到後端資料庫及查詢的 DAX 運算式的資料列層級安全性的支援更快速的輸送量會造成的最佳化。
  
 表格式模型中建立[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用表格式模型專案範本。 專案範本提供的設計介面建立語意模型物件，例如資料表、 資料分割、 關聯性、 階層、 量值和 Kpi。 
  
 表格式模型可以部署到 Azure Analysis Services 或 SQL Server Analysis Services 表格式伺服器模式設定的執行個體。 SQL Server Management Studio 中，可以管理已部署的表格式模型。 

在大部分情況下，將 SQL Server Analysis Services 和 Azure Analysis Services 中，適用於此處的表格式模型化文件。 Azure Analysis Services 專屬的文件發佈與其他 Azure 文件。 若要進一步了解，請參閱[Azure Analysis Services 文件](https://docs.microsoft.com/azure/analysis-services/)。
  
