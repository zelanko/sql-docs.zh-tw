---
title: "使用 R 進行資料探索和建立預測模型 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: "20"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1586c23850daa679aa6804d946ceb0d0a98ad51
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="data-exploration-and-predictive-modeling-with-r"></a>使用 R 的資料探索和預測模型

本主題說明資料科學程序可以透過與 SQL Server 整合的增強功能。

適用於： SQL Server 2016 R Services、 SQL Server 2017 機器 Learnign 服務

## <a name="the-data-science-process"></a>資料科學程序

資料科學家通常使用 R 來探索資料和建置預測模型。 流程通常會在嘗試與失敗間反覆，直到達成良好的預測模型為止。 身為資深的資料科學家，您可能會連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，然後使用 RODBC 封裝將資料擷取到本機工作站，再使用標準 R 封裝建置預測模型。

不過，這個方法有很多的缺點，該 hae 妨礙寬採用 R 企業中的。 

+ 資料移動可能會很緩慢、 效率不佳或不安全
+ R 本身也有其效能與延展限制

當您必須移動及分析大量資料，或電腦的可用記憶體容納不下您使用的資料集時，這些缺點變得更加明顯。

新的可擴充的封裝和隨附的 R 函數[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]幫助您克服這些挑戰的許多。 

## <a name="whats-different-about-revoscaler"></a>什麼是 RevoScaleR 有關不同？

**RevoScaleR** 封裝包含某些熱門 R 函數的實作，這些函數經過重新設計，而得以提供平行處理原則與規模。 如需詳細資訊，請參閱[分散式運算使用 RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)。

RevoScaleR 封裝也支援變更 *「執行內容」*(execution context)。 這表示對於整個解決方案或一個函數，您都可以指定使用裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦資源來執行計算，而不使用您的本機工作站。 這樣做有多項優點：您可以避免不必要的資料移動，也可以運用伺服器電腦上更多的計算資源。

## <a name="r-environment-and-packages"></a>R 環境和封裝

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中支援的 R 環境包含由多個封裝支援及延伸的執行階段、開放原始碼語言和圖形化引擎。 該語言允許使用封裝實作的各種延伸模組。  

### <a name="using-other-r-packages"></a>使用其他 R 封裝

除了隨附於 Microsoft Machine Learning 的專屬 R 程式庫，您可以使用幾乎任何的 R 封裝在您的方案，包括：

+ 來自公用儲存機制的一般用途 R 套件。 您可以從公用儲存機制取得最熱門的開放原始碼 R 封裝，像是 CRAN 的主機便擁有超過 6000 個可供資料科學家使用的封裝。
  
  就 Windows 平台而言，R 套件會以 ZIP 檔案的形式提供，並可依據 GPL 授權來下載及安裝。  
  
  如需如何安裝協力廠商封裝以用在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的相關資訊，請參閱 [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]提供的其他封裝及程式庫。   
  
     **RevoScaleR** 套件包含高效能巨量資料分析、支援一般資料科學工作的改良版函數、適用於貝氏機率的最佳化學習工具、線性迴歸、時間序列模型和類神經網路，以及進階數學程式庫。  
  
     **RevoPemaR** 封裝可讓您使用 R 開發自己的平行外部記憶體演算法。  
  
     如需這些封裝及其使用方式的詳細資訊，請參閱[什麼是 RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction)和[開始使用 RevoPemaR](https://msdn.microsoft.com/microsoft-r/pemar-getting-started)。 

+ **MicrosoftML**包含高度最佳化的機器學習演算法和資料轉換，從 Microsoft 資料科學小組的集合。 許多的演算法也會在 Azure 機器學習中使用。 如需詳細資訊，請參閱[使用 MicrosoftML 封裝](../../advanced-analytics/using-the-microsoftml-package.md)。

### <a name="r-development-tools"></a>R 開發工具

在開發 R 解決方案時，請務必下載 Microsoft R 用戶端。 此免費下載包含支援遠端運算內容以及可擴充 alorithms 所需的程式庫：

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]：**一個 R 執行階段發行版本及一組可提升標準 R 作業效能的套件，例如 Intel Math Kernel Library。  
  
+ **RevoScaleR：**一個可讓您將計算推送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 R 套件。 [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]隨附的可調式新封裝和 R 函數來克服這些挑戰。 它也包含一組常見的 R 函數，這些函數已經過重新設計，可提供更佳的效能和延展性。 您可以依據 **rx** 前置詞識別這些改良的函數。 它也包含適用於各種來源的增強型資料提供者；這些函數的前面會加上 **Rx**。

您可以使用任何支援 R，例如的 Windows 架構的程式碼編輯器[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]或 RStudio。 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] 的下載也包含適用於 R 的常見命令列工具，例如 RGui.exe。

## <a name="use-new-data-sources-and-compute-contexts"></a>使用新的資料來源和計算內容

當使用 RevoScaleR 封裝連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，尋找要在 R 程式碼中使用這些函式：

+ **RxSqlServerData** 是 RevoScaleR 封裝中提供的函數，可改進 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]隨附的可調式新封裝和 R 函數來克服這些挑戰。
  
     您可以在 R 程式碼中使用此函數來定義 *「資料來源」*(data source)。 資料來源物件會指定資料所在的伺服器和資料表，並管理從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]讀取資料及寫入其中的工作。
  
-   **RxInSqlServer** 可用來指定「計算內容」。  也就是說，您可以指定要在您的本機工作站還是裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦上執行 R 程式碼。  如需詳細資訊，請參閱[RevoScaleR 函數](https://msdn.microsoft.com/microsoft-r/scaler/scaler)。
  
     當您設定計算內容時，只會影響到支援遠端執行內容的計算，也就是 RevoScaleR 套件及相關函數所提供的 R 作業。 一般而言，以標準 CRAN 套件為基礎的 R 方案無法在遠端計算內容中執行，但如果是由 T-SQL 啟動，則可以在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦上執行。 不過，您可以使用 `rxExec` 函數來呼叫個別的 R 執行階段，然後從遠端在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中執行它們。

如需如何建立和使用資料來源和執行內容的範例，請參閱這些教學課程：

+ [資料科學深入探討](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [使用 Microsoft R 資料分析](https://msdn.microsoft.com/en-us/microsoft-r/data-analysis-in-microsoft-r)

## <a name="deploy-r-code-to-production"></a>部署到生產環境的 R 程式碼

資料科學的其中一個重點是將您的分析提供給他人，或使用預測模型改進商務結果或程序。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，當您的 R 指令碼或模型就緒時，就能輕鬆移到生產環境。

如需如何移動程式碼以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相關資訊，請參閱 [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md)隨附的可調式新封裝和 R 函數來克服這些挑戰。

通常，部署程序一開始會清理您的指令碼，以排除生產環境不需要的程式碼。 當您移動靠近計算的資料時，您可能會發現更有效率地移動、 摘要或呈現比執行 r 中的所有資料的方式 我們建議，資料科學家，請洽詢資料庫開發人員有關如何改善效能，尤其是這個解決方案會執行資料清理或工程的功能可能會在 SQL 中更有效率。 您可能需要對 ETL 程序進行變更，以確保用於模型建置或評分的工作流程不會失敗，並且輸入資料是以正確的格式提供。

## <a name="see-also"></a>請參閱

[比較基底 R 與 ScaleR 函數](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)

[與 SQL Server 搭配運作的 ScaleR 函數](../../advanced-analytics/r/scaler-functions-for-working-with-sql-server-data.md)
