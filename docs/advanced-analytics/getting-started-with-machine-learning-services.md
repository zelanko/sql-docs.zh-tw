---
title: "開始使用 SQL Server 中的機器學習 |Microsoft 文件"
ms.custom: 
ms.date: 11/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 812cedf6f23adcd99baf24954d9f598bd281fc7c
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="getting-started-with-machine-learning-in-sql-server"></a>開始使用 SQL Server 中的機器學習服務

Microsoft 提供在內部部署和雲端的機器學習解決方案的整合、 可擴充組：

+ **整合式**，因為您可以在 SQL Server 中執行 R 或 Python。 這可讓您輕鬆地合併企業處理 ETL 和報告功能與資料科學工作，例如工程、 模型建立和計分的功能。
+ **可擴充**，因為資料科學家可以開發和測試解決方案，以在膝上型電腦，而且再將它部署到多個平台分散式或平行處理的索引鍵作業例如模型定型和計分。 支援的平台包括 Windows、 Hadoop 和 Spark 上的 SQL Server。

本文章會提供資源的連結，在 Microsoft Machine Learning 平台的每項產品。

## <a name="machine-learning-in-sql-server"></a>機器學習中 SQL Server

+ SQL Server 2017

  從 SQL Server 2017 開始，您現在可以使用 Python 程式碼中 SQL Server。 若要反映更廣泛的支援方案中多個語言 （敬請期待 ！），並在名稱已變更為[!INCLUDE[rsql-productnamenew-md](../includes/rsql-productnamenew-md.md)]。 現在您可以使用 SQL 工具來執行 R 或 Python 程式碼來自動化機器學習工作。 或者，使用 SQL Server 電腦，做為_計算內容_從遠端的開發環境中啟動的工作。

    + [SQL Server 中的 python 架構概觀](/python/architecture-overview-sql-server-python.md)
    + [設定 SQL Server R 服務或機器學習服務](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

+ SQL Server 2016

  SQL Server 2016 中使用預存程序的 SQL Server 支援執行 R 程式碼。 這可讓您輕鬆地使用 SQL 工具來自動化機器學習工作。 或者，您可以從遠端的膝上型電腦或 R 開發環境中，執行 R 程式碼時使用的 SQL Server 電腦_計算內容_。

  這項整合提供您的資料安全性，並可讓您管理及平衡 r 所使用的資源

    + [取得已啟動與 SQL Server R Services](r/getting-started-with-sql-server-r-services.md)
    + [設定 SQL Server R 服務或機器學習服務](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

## <a name="microsoft-machine-learning-server-microsoft-r-server"></a>Microsoft 的機器學習伺服器 (Microsoft R Server)

若要安裝的選項[!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)]所提供的 SQL Server 2017 支援企業客戶想要執行分散式、 可調整的機器學習工作，但不需要使用 SQL Server 資料庫引擎，例如要使用 SQL 計算的整合內容。

在 SQL Server 2016 中，使用選項來安裝[!INCLUDE[rsql-platform-md](../includes/rsql-platformnew-md.md)]。
  
  + [歡迎使用機器學習伺服器](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)
  
您也可以安裝[!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]或[!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)]透過特定平台安裝程式：

  + [在 Windows 上安裝](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
  + [Linux 上安裝](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-linux-install)
  + [在 Hadoop 上安裝](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-hadoop-install)

> [!IMPORTANT]
> 如果您想要執行 Python 使用 R 伺服器，請確定安裝最新版本中， [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)]，這是只能透過[!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]安裝程式：
> 
>    + [設定 Microsoft R Server 或 Server 機器學習](../advanced-analytics/r/create-a-standalone-r-server.md)

## <a name="related-products"></a>相關的產品

+ [設定資料科學用戶端](../advanced-analytics/r/set-up-a-data-science-client.md)

  如果您已經安裝其中一項機器學習伺服器產品，本文章提供如何設定用於開發和測試解決方案，包括工具和必要的程式庫的另一部電腦的相關資訊。

+ [資料科學虛擬機器](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

  快速啟動您的項目插入機器學習服務藉由取得此完整的機器學習服務透過 Azure Marketplace 的方案。 （經常縮短為 「 DSVM"） 的 data science 虛擬機器包含 SQL Server、 Microsoft Machine Learning 伺服器和所有開發工具。
  
  提供 Windows 10 的全新可自訂外觀，Windows 2016 Preview 版上執行最新版本的資料科學虛擬機器 (DSVM)。 它隨附預先設定的 NVIDIA 驅動程式、 CUDA Toolkit 8.0 和 GPU 工作負載的 NVIDIA cuDNN 程式庫。

## <a name="resources-for-learning"></a>學習資源

+ [機器學習教學課程](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)

  從這裡開始了解使用機器學習解決方案中找到的所有資源清單[!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]或[!INCLUDE[sssql15-md](../includes/sssql15-md.md)]。

### <a name="r-tutorials"></a>R 教學課程

+ [SQL Server R 教學課程](../advanced-analytics/tutorials/sql-server-r-tutorials.md)

   了解如何在 SQL Server 中執行 R、 建立和使用遠端計算內容，或在使用 SQL Server 的 R 執行模擬。
   
   包含 「 提供的所有程式碼 」 教學課程，讓您可以從 SQL Server Management Studio 中，執行完整的 R 解決方案，而不需曾開啟 R IDE ！

+ [瀏覽 25 精簡函式中 R 和 ScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

   不熟悉 R 嗎？ 想知道如何 Microsoft R （或 RevoScaleR） 與比較標準 R 嗎？ R 伺服器，請參閱這些快速啟動。

### <a name="python-tutorials"></a>Python 教學課程

+ [SQL Server Python 教學課程](../advanced-analytics/tutorials/sql-server-r-tutorials.md)

  了解如何在中執行 Python [!INCLUDE[ssnoversion](../includes/ssnoversion.md)]。 使用 Python 建置模型，並使用它來評分 SQL Server 資料。

   SQL 開發人員的端對端解決方案提供您要從 SQL Server Management Studio 中執行 Python 程式碼。

+ [發佈和取用的 Python 程式碼](../advanced-analytics/python/publish-consume-python-code.md)

  本逐步解說提供的模型部署到使用 Server 機器學習 web 服務所需的所有程式碼。

### <a name="product-samples-with-code"></a>使用程式碼產品範例

從 SQL Server 開發團隊這些解決方案 Python 或 R 中執行，並示範機器學習服務整合與商務應用程式的常見案例。

+ [Build an intelligent app with SQL Server and R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

+ [建置與 SQL Server，並將 Python 的智慧型應用程式](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

### <a name="data-science-solution-templates"></a>資料科學方案範本

從 Microsoft 資料科學小組解決方案範本代表專供特定產業或案例的完整範例方案。 它們被要做為建置組塊，可協助您實作快速，解決方案或以示範最佳作法。 每個範本包含範例資料和可自訂的程式碼。

+ [方案範本](../advanced-analytics/tutorials/data-science-scenarios-and-solution-templates.md)

## <a name="next-steps"></a>後續的步驟

[開始使用 SQL Server 機器學習服務](../advanced-analytics/r/getting-started-with-sql-server-r-services.md)

[開始使用 Microsoft 機器學習服務伺服器](../advanced-analytics/r/getting-started-with-microsoft-r-server-standalone.md)
