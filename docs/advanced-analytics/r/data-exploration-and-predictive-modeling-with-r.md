---
title: 資料探索和使用 R-SQL Server Machine Learning 服務的預測性模型
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2e045d061df813ae004dcb13668c31e68c3b5b5a
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976412"
---
# <a name="data-exploration-and-predictive-modeling-with-r-in-sql-server"></a>資料探索和使用 SQL Server 中 R 的預測模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明資料科學程序透過 SQL Server 與整合的增強功能。

適用於：SQL Server 2016 R Services、 SQL Server 2017 Machine Learnign 服務

## <a name="the-data-science-process"></a>資料科學程序

資料科學家通常使用 R 來探索資料和建置預測模型。 流程通常會在嘗試與失敗間反覆，直到達成良好的預測模型為止。 身為資深的資料科學家，您可能會連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，然後使用 RODBC 封裝將資料擷取到本機工作站，再使用標準 R 封裝建置預測模型。

不過，此方法有許多缺點，該 hae 妨礙企業中更多採用 R 的強大功能。 

+ 資料移動可能會緩慢、 效率不佳，或不安全
+ R 本身也有效能與延展限制

當您需要移動及分析大量資料，或使用不符合您的電腦上可用的記憶體的資料集時，這些缺點變得更加明顯。

新的、 可調整的封裝和隨附的 R 函數[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]幫助您克服當中眾多挑戰。 

## <a name="whats-different-about-revoscaler"></a>什麼是 RevoScaleR 不同？

**RevoScaleR** 封裝包含某些熱門 R 函數的實作，這些函數經過重新設計，而得以提供平行處理原則與規模。 如需詳細資訊，請參閱 <<c0> [ 分散式運算使用 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。

RevoScaleR 封裝也支援變更 *「執行內容」*(execution context)。 這表示對於整個解決方案或一個函數，您都可以指定使用裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦資源來執行計算，而不使用您的本機工作站。 這樣做有多項優點：您可以避免不必要的資料移動，也可以運用伺服器電腦上更多的計算資源。

## <a name="r-environment-and-packages"></a>R 環境和封裝

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中支援的 R 環境包含由多個封裝支援及延伸的執行階段、開放原始碼語言和圖形化引擎。 該語言允許使用封裝實作的各種延伸模組。  

### <a name="using-other-r-packages"></a>使用其他 R 套件

除了隨附於 Microsoft Machine Learning 的專屬 R 程式庫，您可以使用幾乎任何 R 套件中您的解決方案，包括：

+ 來自公用儲存機制的一般用途 R 套件。 您可以從公用儲存機制取得最熱門的開放原始碼 R 封裝，像是 CRAN 的主機便擁有超過 6000 個可供資料科學家使用的封裝。
  
  就 Windows 平台而言，R 套件會以 ZIP 檔案的形式提供，並可依據 GPL 授權來下載及安裝。  
  
  如需如何安裝協力廠商封裝以用在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的相關資訊，請參閱 [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]提供的其他封裝及程式庫。   
  
     **RevoScaleR** 套件包含高效能巨量資料分析、支援一般資料科學工作的改良版函數、適用於貝氏機率的最佳化學習工具、線性迴歸、時間序列模型和類神經網路，以及進階數學程式庫。  
  
     **RevoPemaR** 封裝可讓您使用 R 開發自己的平行外部記憶體演算法。  
  
     如需有關這些封裝和使用方式的詳細資訊，請參閱 <<c0> [ 什麼是 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler)並[RevoPemaR 入門](https://docs.microsoft.com/machine-learning-server/r/how-to-developer-pemar)。 

+ **MicrosoftML**包含高度最佳化的機器學習演算法及 Microsoft 資料科學小組的資料轉換的集合。 許多的演算法也會在 Azure Machine Learning 中使用。 如需詳細資訊，請參閱 < [SQL Server 中的 MicrosoftML](ref-r-microsoftml.md)。

### <a name="r-development-tools"></a>R 開發工具

在開發您的 R 解決方案時，請務必下載 Microsoft R Client。 此免費下載包括支援遠端運算內容以及可調整的 alorithms 所需的程式庫：

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]：** R 執行階段和一組套件，例如 Intel math kernel library，大幅提升標準 R 作業效能的散發套件。  
  
+ **RevoScaleR:** R 封裝，可讓您將計算推送到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. 它也包含一組常見的 R 函數，這些函數已經過重新設計，可提供更佳的效能和延展性。 您可以依據 **rx** 前置詞識別這些改良的函數。 它也包含適用於各種來源的增強型資料提供者；這些函數的前面會加上 **Rx**。

您可以使用這類支援語言，任何以 Windows 為基礎的程式碼編輯器[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]或 RStudio。 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] 的下載也包含適用於 R 的常見命令列工具，例如 RGui.exe。

## <a name="use-new-data-sources-and-compute-contexts"></a>使用新的資料來源和計算內容

當使用 RevoScaleR 封裝連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，尋找以 R 程式碼中使用這些函式：

+ **RxSqlServerData** 是 RevoScaleR 封裝中提供的函數，可改進 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]隨附的可調式新封裝和 R 函數來克服這些挑戰。
  
     您可以在 R 程式碼中使用此函數來定義 *「資料來源」*(data source)。 資料來源物件會指定資料所在的伺服器和資料表，並管理從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]讀取資料及寫入其中的工作。
  
-   **RxInSqlServer** 可用來指定「計算內容」。  也就是說，您可以指定要在您的本機工作站還是裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦上執行 R 程式碼。  如需詳細資訊，請參閱 < [RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。
  
     當您設定計算內容時，只會影響到支援遠端執行內容的計算，也就是 RevoScaleR 套件及相關函數所提供的 R 作業。 一般而言，以標準 CRAN 套件為基礎的 R 方案無法在遠端計算內容中執行，但如果是由 T-SQL 啟動，則可以在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦上執行。 不過，您可以使用 `rxExec` 函數來呼叫個別的 R 執行階段，然後從遠端在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中執行它們。

如需如何建立及使用資料來源與執行內容的範例，請參閱這些教學課程：

+ [資料科學深入探討](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [使用 Microsoft R 的資料分析](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)

## <a name="deploy-r-code-to-production"></a>將 R 程式碼部署至生產環境

資料科學的其中一個重點是將您的分析提供給他人，或使用預測模型改進商務結果或程序。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，當您的 R 指令碼或模型就緒時，就能輕鬆移到生產環境。

如需如何移動程式碼以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相關資訊，請參閱 [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md)隨附的可調式新封裝和 R 函數來克服這些挑戰。

通常，部署程序一開始會清理您的指令碼，以排除生產環境不需要的程式碼。 當您移動更接近計算的資料時，您可能會發現更有效率地移動、 摘要，或呈現比在 r 中的所有資料的方式 建議資料科學家，請洽詢資料庫開發人員有關如何改善效能，特別是當方案執行資料清理或特徵工程以可能會在 SQL 中更有效率。 您可能需要對 ETL 程序進行變更，以確保用於模型建置或評分的工作流程不會失敗，並且輸入資料是以正確的格式提供。

## <a name="see-also"></a>另請參閱

[基底 R 與 RevoScaleR 函數的比較](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)

[SQL Server 中的 RevoScaleR 程式庫](ref-r-revoscaler.md)
