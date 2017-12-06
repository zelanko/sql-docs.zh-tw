---
title: "SQL Server 機器學習服務的架構概觀 |Microsoft 文件"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9726ba8958f623d3c3c92d18f59f4c25d18fb0b0
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="architecture-overview-for-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的架構概觀 

本主題說明支援的 Python 和 R 指令碼的執行 SQL Server 中的擴充性架構的目標。

它也提供一個概觀如何架構主要為了符合這些目標，如何 R Python 支援和是執行 SQL Server，並整合的優點。

整體來說，擴充性架構則幾乎完全相同的 R 和 Python，稱為 launchers 的詳細資料、 設定選項等等中有些微差異。 如需特定語言的實作的進一步資訊，請參閱下列主題：

- [SQL Server R services 的架構概觀](r/architecture-overview-sql-server-r.md)
- [SQL Server 中的 python 架構概觀](python/architecture-overview-sql-server-python.md)


## <a name="background"></a>背景

在 SQL Server 2016 中，許多變更引進以支援執行 R 指令碼，使用 SQL Server database engine。 在 SQL Server 2017，此基礎結構已提升至加入 Python 語言的支援。

擴充性架構的目的是要建立 SQL Server 之間資料科學語言，例如 R 和 Python，若要減少摩擦時發生資料科學方案移至生產環境，並保護資料，可能會更好的介面公開在資料科學開發程序。

藉由執行受信任的指令碼語言，在受 SQL Server 的安全架構中，資料庫開發人員可以維護安全性，同時允許使用企業資料的資料科學家。

  ![與 SQL Server 的整合目標](media/ml-service-value-add.png "機器學習服務值加入")

- 目前使用者的 R 或 Python 應該可以移植程式碼，且 SQL Server 中執行相當稍加修改。
- SQL Server 中的資料安全性模型會擴充到外部指令碼語言所使用的資料。 換句話說，其他人執行 R 或 Python 指令碼應該無法使用 SQL 查詢中的該使用者無法存取的任何資料。
- 資料庫管理員應該能夠管理外部指令碼所使用的資源管理使用者，以及管理和監視外部程式碼程式庫。
- 系統必須支援基礎的解決方案完全的 R 和 Python，但使用專屬的元件開發的開放原始碼散發由 Microsoft 提供較高的安全性和效能。

## <a name="architecture-core-concepts"></a>架構的核心概念

若要達成這些目標，SQL Server 2016 R Services 和 SQL Server 2017 機器學習服務的 R，並將 Python 的架構為基礎這些核心概念：

+ **多處理序的架構**

  R 和 Python 是開放原始碼語言與豐富且熱心社群支援。 因此，務必要維護與開放原始碼 R，並將 Python 的完整互通性。

  R 和 Python 開放原始碼散發套件會安裝 SQL Server 授權，而且運作獨立從 SQL Server 視。

   此外，Microsoft 提供一組專屬的程式庫提供整合到 SQL Server，包括資料轉譯、 壓縮和每個支援的語言適用對象的最佳化。

+ **安全性**

   更好的安全性表示支援整合式的 Windows 驗證和密碼為基礎的 SQL 登入，做為認證，也一樣安全處理仰賴 SQL Server 進行資料保護和使用 SQL Server 受信任的啟動列 來管理外部指令碼執行與安全用於指令碼中的資料。

+ **延展性和效能**

  與 SQL Server 的整合是改善效益 R，並將 Python 企業中的索引鍵。 可以執行任何 R 或 Python 指令碼，藉由呼叫預存程序，並會傳回結果做為表格式結果直接對 SQL Server，以便輕鬆地產生或取用任何可以傳送 SQL 查詢和處理結果的應用程式的機器學習服務。

  效能最佳化依賴兩個層面同樣功能強大的平台： 資源控管和平行處理使用 SQL Server 和分散式運算演算法中所提供**RevoScaleR**和**revoscalepy**。

## <a name="solution-development-and-deployment"></a>開發及部署方案

除了擴充平台的這些核心目標，SQL Server 中的機器學習服務用以提供強式整合資料庫引擎和 BI 堆疊，與這些優點：

+ 透過傳統的監視工具的效能與資源管理
+ 容易使用的 Python 和 R 資料 BI 套件或應用程式可以取用 SQL 查詢結果
+ 機器學習解決方案的企業開發更低阻礙

我們來看看它實際上的運作方式。

  ![ML 方案開發程序](media/ml-solution-development-process.png "開發和部署使用機器學習服務")

1. 相容性界限內保留資料，可以管理及監視 SQL Server 所使用的資料。 同時，DBA 有誰可以安裝封裝，或在伺服器上執行指令碼的完整控制權。 如果您想要 DBA 也可以委派至資料科學家或經理在資料庫層級的權限。
2. 資料科學家可以建置並測試方案，在其慣用 R 或 Python 環境中，與伺服器中斷連接。
3. SQL 開發人員可以使用熟悉的工具，例如 Management Studio 或 Visual Studio 整合 R 或 Python 程式碼與 SQL Server。 緊密的整合，意味著且熟悉的開發人員可以選擇以最佳化每個工作的最佳工具。 比方說，您可能會使用一些功能工程工作和 R SQL 代表其他項目。 您可能會在 Integration Services 工作來執行複雜的文字分析內嵌 Python 指令碼。
4. 測試和已備妥部署解決方案可以使用 SQL Server 技術，例如資料行存放區索引，以提升效能最佳化。 較新的功能可讓您以批次定型許多小型資料分割的資料集上平行模型 」 或 「 分數 」 數百萬個資料列中使用原生 SQL 程式碼最佳化的機器學習工作。
5. 準備好提起嗎？ 您可以輕鬆地公開預測方案 BI 堆疊或外部應用程式，使用預存程序。

## <a name="related-products"></a>相關的產品

不確定哪一部機器學習解決方案符合您的需求？ 除了 SQL Server 2016 和 SQL Server 2017 中內嵌的分析，Microsoft 會提供下列機器學習平台和服務：

+ [Microsoft R Server 和機器學習伺服器](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)

  多平台環境的開發、 發佈和管理機器學習服務工作
+ [資料科學虛擬機器](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview)

  您需要的機器學習，預先安裝的所有工具。 使用 Jupyter 筆記本、 Python 或。
  
  試用新[Windows 2016 預覽版本](http://aka.ms/dsvm/win2016)，其中包括常用的深入學習架構，例如 CNTK 和 mxNet，以及支援 Windows 容器的 GPU 版本 ！

+ [認知的 azure 服務](https://azure.microsoft.com/services/cognitive-services/)

  各種不同的雲端服務到您的應用程式，包括視訊、 臉部辨識索引自然語言新增 AI 和 ML 情緒偵測與文字分析機器轉譯，以及執行許多更
+ [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)

  雲端為基礎的拖放介面設計機器學習服務工作流程，結合了可自動化及整合與透過 web 服務和 PowerShell 的應用程式

## <a name="see-also"></a>請參閱

[比較 Server 機器學習和 Microsoft R 產品](https://docs.microsoft.com/machine-learning-server/what-is-r-server-interoperability)
