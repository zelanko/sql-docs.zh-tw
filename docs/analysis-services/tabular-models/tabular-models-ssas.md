---
title: 表格式模型 |Microsoft 文件
ms.custom: ''
ms.date: 03/30/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 17c1a7ad76522f2cab47ae89c80fd3bcc20b1a79
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="tabular-models"></a>表格式模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  表格式模型是一種 Analysis Services 資料庫，其會在記憶體內部或以 DirectQuery 模式執行，並直接從後端的關聯式資料來源存取資料。 使用的圖案狀態壓縮演算法和多執行緒的查詢處理器，分析引擎送交快速存取表格式模型物件和資料透過報表用戶端應用程式，例如 Power BI 與 Excel。  
  
 DirectQuery 時記憶體中模型都是預設值，是模型，就是替代的查詢模式太大而無法放在記憶體中，或資料的變動程度不適合進行合理處理策略。 DirectQuery 會達到同位檢查的記憶體中模型支援廣泛的資料來源能夠處理導出的資料表和資料行，在 DirectQuery 模型中，透過 DAX 運算式，以連線到後端資料庫中，且查詢的資料列層級安全性導致更快速的輸送量的最佳化。
  
 表格式模型中建立[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用所提供的設計介面來建立模型、 資料表、 關聯性和 DAX 運算式的表格式模型專案範本。 您可以從多個來源匯入資料，然後加入關聯性、計算資料表和資料行、量值、KPI、階層及翻譯，來充實模型。  
  
 模型可以再部署到 Azure Analysis Services 或 SQL Server Analysis Services 的執行個體設定為表格式伺服器模式。 SQL Server Management Studio 中，可以管理已部署表格式模型。 當您的模型成長時，它們可以進行資料分割以最佳化處理和保護，以資料列層級使用以角色為基礎的安全性。  

  
  
