---
title: SQL Server 資料採礦增益集，適用於 Office |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71717e002c55cea94f46e62643c74f4773e0a51d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="sql-server-data-mining-add-ins-for-office"></a>適用於 Office 的 SQL Server 資料採礦增益集

  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 適用於 Office 的資料採礦增益集是一組輕量型的預測分析工具，可讓您使用 Excel 中的資料建立用於預測、建議或探索的分析模型。  
  
> [!IMPORTANT]
> 資料採礦增益集適用於 Office 不支援 Office 2016 或更新版本。
  
 此增益集中的精靈和資料管理工具會針對以下這些常見的資料採礦工作提供逐步指示：  
  
-   **在模型化之前組織及清除資料。** 使用儲存在 Excel 中或任何 Excel 資料來源的資料。 您可以建立並儲存連接，以便重複使用資料來源、重複進行實驗或重新定型模型。  
  
-   **分析、取樣和準備。** 許多有經驗的資料採礦人員指出，有多達 70-90% 的資料採礦專案是花費在資料準備上。 增益集可以藉由提供 Excel 中的視覺效果和精靈幫助您進行這些常見的工作，讓這項工作進行得更快：  
  
    -   分析資料並了解其分佈情形和特性。  
  
    -   透過隨機取樣或超取樣建立定型和測試資料集。  
  
    -   尋找極端值並移除或取代它們。  
  
    -   重定資料標籤來提升分析的品質。  
  
-   **透過有人監督或無人監督的學習技術來分析模式。** 透過容易使用的精靈的指引來執行一些最常見的資料採礦工作，包括叢集分析、購物籃分析和預測。  
  
     此增益集中包含一般熟知的機器學習演算法，其中包括貝氏機率分類、羅吉斯迴歸、群集、時間序列以及類神經網路。  
  
     如果您還不熟悉資料採礦，則可以從 **[查詢]** 精靈取得建立預測查詢的協助。  
  
     進階使用者則可以使用具有拖放功能的 **[進階查詢編輯器]** 來建立自訂 DMX 查詢，或使用 Excel VBA 來將預測自動化。  
  
-   **記載和管理。** 建立了資料集以及一些模型之後，就可以透過產生資料的統計摘要和模型參數來記載您的工作與您的見解。  
  
-   **探索和視覺化。** 資料採礦並不是一種可以全面自動化的活動，您需要探索及了解結果並採取有意義的動作。 增益集可藉由提供 Excel 的互動式檢視器、讓您自訂模型圖表的 Visio 範本，以及將圖表和資料表匯出到 Excel 進行額外的篩選或修改的功能，幫助您進行探索。  
  
-   **部署與整合。** 當您建立了實用的模型時，使用管理工具將模型從試驗伺服器匯出到另一個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體，讓您的模型實際執行。  
  
     您也可以將模型留在當初建立的伺服器上，但是使用 Integration Services 或 DMX 指令碼重新整理定型資料並執行預測。  
  
     進階使用者還可使用 **[追蹤]** 功能查看傳送至伺服器的 XMLA 和 DMX 陳述式。  
  
## <a name="getting-started"></a>快速入門  
 如需詳細資訊，請參閱 [適用於 Office 的資料採礦增益集包含的內容](http://go.microsoft.com/fwlink/p/?LinkId=616849)  
  
## <a name="support-and-requirements"></a>支援與需求  
 適用於 Office 的 SQL Server 資料採礦增益集是免費下載的軟體。 您必須已安裝下列其中一個 Office 版本，才能使用這些工具：  
  
-   Office 2010，32 位元或 64 位元版本  
  
-   Office 2013，32 位元或 64 位元版本  
  
> [!WARNING]  
>  請務必下載符合您 Excel 版本的增益集版本。  
  
 資料採礦增益集需要連接以下其中一個 SQL Server Analysis Services 版本：  
  
-   Enterprise  
  
-   Business Intelligence  
  
-   Standard  
  
 根據您連接的 SQL Server Analysis Services 版本而定，某些進階演算法可能會無法使用。 如需詳細資訊，請參閱 [Features Supported by the Editions of SQL Server 2016](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)(SQL Server 2016 版本支援的功能)。  
  
 其他安裝的說明，請參閱下載中心上的此頁面： [http://www.microsoft.com/download/details.aspx?id=29061](http://www.microsoft.com/download/details.aspx?id=29061)  
  
  
