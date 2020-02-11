---
title: 資料採礦（SSAS） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], about data mining
ms.assetid: b1c912da-72f6-4d96-89c8-55a2c4f19e88
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28b623333adaced772f85572091543f124894f4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084817"
---
# <a name="data-mining-ssas"></a>資料採礦 (SSAS)
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供併入資料採礦的方案一個整合式平台。 您可以使用關聯式資料或 Cube 資料建立具有預測分析的商業智慧方案。  
  
## <a name="benefits-of-data-mining"></a>資料採礦的優點  
 資料採礦使用適當研究的統計原則探索資料中的模式，並協助您針對複雜的問題，做出明智的決策。 您可以將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的資料採礦演算法套用至資料，以預測趨勢、識別模式、建立規則和建議、分析複雜資料集中的事件順序，以及取得新觀點。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，資料採礦功能強大、可以存取，而且與許多人喜歡用於分析和報表的工具整合在一起。 請參閱本節中的連結，以取得有關入門所需之資料採礦的廣大背景。  
  
## <a name="key-data-mining-features"></a>主要資料採礦功能  
 SQL Server 提供下列功能，以支援整合式資料採礦方案：  
  
-   多個資料來源：您不必建立資料倉儲或 OLAP Cube 來進行資料採礦。 您可以使用外部提供者的表格式資料、試算表，甚至文字檔。 您也可以輕鬆對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中建立的 OLAP Cube 進行採礦。 但是，您無法使用記憶體中資料庫內的資料。  
  
-   整合式資料清理、資料管理及 ETL：Data Quality Services 提供分析及清理資料的進階工具。 Integration Services 可用來建立 ETL 程序，該程序不僅可以用來清理資料，也可以用來建立、處理、定型及更新模型。  
  
-   多個可自訂的演算法：除了提供叢集、類神經網路及決策樹等演算法之外，此平台也支援開發您自己的自訂外掛程式演算法。  
  
-   模型測試基礎結構：使用交叉驗證、分類矩陣、增益圖及散佈圖等重要的統計工具，來測試您的模型和資料集。 輕鬆建立及管理測試集和定型集。  
  
-   查詢和鑽研：建立預測查詢、擷取模型模式和統計資料，以及鑽研到案例資料。  
  
-   用戶端工具：除了 SQL Server 提供的開發和設計 Studio 之外，您也可以使用 Excel 的資料採礦增益集建立、查詢及瀏覽模型， 或建立自訂用戶端，包括 Web 服務。  
  
-   指令碼語言支援和 Managed API：所有資料採礦物件皆可完整程式化。 您可以透過 MDX、XMLA 或 PowerShell Extensions for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]編寫指令碼。 使用資料採礦延伸模組 (DMX) 語言快速查詢及編寫指令碼。  
  
-   安全性和部署：透過 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供以角色為基礎的安全性，包括鑽研到模型及結構化資料的個別權限。 輕鬆將模型部署至其他伺服器，讓使用者可以存取模式或執行預測  
  
## <a name="in-this-section"></a>本節內容  
 本節中的主題介紹 SQL Server 資料採礦的主要功能及相關工作。  
  
-   [資料採礦概念](data-mining-concepts.md)  
  
-   [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [&#40;Analysis Services 的採礦結構-資料採礦&#41;](mining-structures-analysis-services-data-mining.md)  
  
-   [&#40;Analysis Services 的採礦模型-資料採礦&#41;](mining-models-analysis-services-data-mining.md)  
  
-   [測試和驗證 &#40;資料採礦&#41;](testing-and-validation-data-mining.md)  
  
-   [資料採礦查詢](data-mining-queries.md)  
  
-   [資料採礦方案](data-mining-solutions.md)  
  
-   [資料採礦工具。](data-mining-tools.md)  
  
-   [資料採礦架構](data-mining-architecture.md)  
  
-   [&#40;資料採礦&#41;的安全性總覽](security-overview-data-mining.md)  
  
  
