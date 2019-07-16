---
title: 資料採礦 (SSAS) |Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 163314576f609d6fc34ba55b05eff841d1361182
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210110"
---
# <a name="data-mining-ssas"></a>資料採礦 (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

> [!IMPORTANT]
> 在 SQL Server Analysis Services 2017 中已被取代的資料採礦。 文件不會更新已被取代的功能。 若要進一步了解，請參閱[Analysis Services 回溯相容性 (SQL 2017)](../analysis-services-backward-compatibility-sql2017.md)。

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自 2000 版本後，藉由提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的資料採礦，已是預測分析中的佼佼者。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦的結合，針對包含資料清理和準備、預測分析機器學習和報表提供整合平台。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦包括多個標準演算法，包括 EM 和 k-means 叢集模型，類神經網路、羅吉斯迴歸與線性迴歸、決策樹和貝氏機率分類分類器。 所有模型已都整合視覺效果以協助您開發、改善及評估模型。  將資料採礦整合至商業智慧方案，可協助您對複雜問題做出明智的決策。  
  
## <a name="benefits-of-data-mining"></a>資料採礦的優點  
 資料採礦 (也稱為預測分析和機器學習服務) 使用經過詳盡研究的統計原則來探索資料的模式。 您可以將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的資料採礦演算法套用至資料，以預測趨勢、識別模式、建立規則和建議、分析複雜資料集中的事件順序，以及取得新觀點。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，資料採礦功能強大、可以存取，而且與許多人喜歡用於分析和報表的工具整合在一起。  
  
## <a name="key-data-mining-features"></a>主要資料採礦功能  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦提供下列功能，以支援整合式資料採礦方案：  
  
-   多個資料來源：您可以使用任何表格式資料來源的資料採礦，包括試算表和文字檔。 您也可以輕鬆對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中建立的 OLAP Cube 進行採礦。 但是，您無法使用記憶體中資料庫內的資料。  
  
-   整合式資料清理、資料管理及報表： [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供分析及清理資料的工具。 您可以建立 ETL 程序針對模型來清理資料，而 ssISnoversion 和也可讓您輕鬆地重新定型及更新模型。  
  
-   多個可自訂的演算法：除了提供叢集、 類神經網路及決策樹等演算法之外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也支援開發您自己的自訂外掛程式演算法。  
  
-   模型測試基礎結構：測試您的模型使用交叉驗證的重要的統計工具的資料集，分類矩陣、 增益圖和散佈圖等。 輕鬆建立及管理測試集和定型集。  
  
-   查詢和鑽研：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦提供 DMX 語言，將預測查詢整合至應用程式。 您也可以從模型中擷取詳細統計資料和模式，並鑽研到案例資料。  
  
-   用戶端工具：除了 SQL Server 提供的開發和設計 studio，您可以使用資料採礦增益集適用於 Excel 來建立、 查詢及瀏覽模型。 或建立自訂用戶端，包括 Web 服務。  
  
-   指令碼語言支援和 managed API:所有的資料採礦物件皆完全可程式化。 您可以透過 MDX、XMLA 或 PowerShell Extensions for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]編寫指令碼。 使用資料採礦延伸模組 (DMX) 語言快速查詢及編寫指令碼。  
  
-   安全性和部署：提供以角色為基礎的安全性，透過[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，包括鑽研到模型及結構化資料的個別權限。 輕鬆將模型部署至其他伺服器，讓使用者可以存取模式或執行預測  
  
## <a name="in-this-section"></a>本節內容  
 本節中的主題介紹 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦的主要功能及相關工作。  
  
-   [資料採礦概念](../../analysis-services/data-mining/data-mining-concepts.md)  
  
-   [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [採礦結構 &#40;Analysis Services-資料採礦 &#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
-   [採礦模型 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
-   [測試及驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
-   [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)  
  
-   [資料採礦方案](../../analysis-services/data-mining/data-mining-solutions.md)  
  
-   [資料採礦工具](../../analysis-services/data-mining/data-mining-tools.md)  
  
-   [資料採礦架構](../../analysis-services/data-mining/data-mining-architecture.md)  
  
-   [安全性概觀 &#40;資料採礦&#41;](../../analysis-services/data-mining/security-overview-data-mining.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server R 服務](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
