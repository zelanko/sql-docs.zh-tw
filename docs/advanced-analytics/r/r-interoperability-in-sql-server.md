---
title: SQL Server R Services 中的 R 互通性 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: da739700cabb6a9d691d5f284cd6f0532898393f
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979020"
---
# <a name="r-interoperability-in-sql-server"></a>SQL Server 中的 R 互通性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題著重在針對 SQL Server 中的 R 執行的機制，並說明 Microsoft R 與開放原始碼 r 之間的差異

適用於： SQL Server 2016 R Services、 SQL Server 2017 Machine Learning 服務

如需其他元件的資訊，請參閱[SQL Server 中的新元件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md)。

### <a name="open-source-r-components"></a>開放原始碼 R 元件

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 包含一組完整散發的基底 R 封裝和工具。 如需基底散發隨附內容的詳細資訊，請參閱安裝期間安裝於下列預設位置的文件︰`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

在安裝 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 期間，您必須同意 GNU 公用授權的條款。 之後，您就可以執行標準的 R 封裝，而不需進一步修改，就如同在 R 的任何其他開放原始碼散發中一樣。

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 不會以任何方式修改 R 執行階段。 R 執行階段是在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 處理序外部執行，而且可在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 以外獨立執行。 不過，強烈建議您不要在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用 R 時執行這些工具，以避免資源爭用。

與特定 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體相關聯的 R 基底封裝散發，可以在與該執行個體相關聯的資料夾中找到。 例如，如果您安裝 R Services 的預設執行個體時，R 程式庫位於此資料夾預設：

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library

同樣地，預設執行個體相關聯的 R 工具會位於此資料夾預設：

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin

如需 Microsoft R 有何不同，您可能會收到從 CRAN R 基底散發的詳細資訊，請參閱[R 語言和 Microsoft R 產品與功能的互通性](https://docs.microsoft.com/r-server/what-is-r-server-interoperability)

### <a name="additional-r-packages-from-microsoft-r"></a>從 Microsoft R 的其他 R 套件

除了基底 R 散發，[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]包括一些專屬的 R 封裝，以及用來平行執行 R，也支援在遠端計算內容中的 執行 R 的架構。

這個 R 功能的組合 (R 基底散發加上已增強的 R 功能和封裝) 稱為 **Microsoft R**。如果您安裝 Microsoft R Server (獨立式)，就會取得一組與使用 SQL Server R Services (資料庫內) 所安裝封裝完全相同的封裝，但位於不同的資料夾中。

Microsoft R 包括 Intel Math Kernel Library 的散發，這是用來儘可能加快數學處理的速度。 例如，基本線性代數 (BLAS) 程式庫適用於許多附加元件封裝以及 R 本身。 如需詳細資訊，請參閱下列文章：

+ [Intel Math Kernel 如何加快 R 的速度 (英文)](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)
+ [將 R 連結至多執行緒數學程式庫的效能優點 (英文)](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)

Microsoft R 的最重要新增項目包括 **RevoScaleR** 和 **RevoPemaR** 封裝。 這些是已大量使用 C 或 C++ 撰寫以用來獲取較佳效能的 R 封裝。

+ **RevoScaleR。** 包含各種不同的 API 以進行資料操作和分析。 API 已經最佳化，可分析因過大而無法納入記憶體的資料集，以及執行分散在數個核心或處理器上的計算。

   RevoScaleR API 也支援使用資料子集來獲取更佳的延展性。 換句話說，大多數 RevoScaleR 函數都可在資料區塊上運作，並使用更新演算法來彙總結果。 因此，以 RevoScaleR 函數為基礎的 R 方案可以使用非常大型的資料集，而且不會受限於本機記憶體。

  RevoScaleR 封裝也支援 .XDF 檔案格式，以便更快速移動和儲存用於分析的資料。 XDF 格式會使用單欄式儲存體、具可攜性，且可用來從各種來源載入然後操作資料，包括文字、SPSS 或 ODBC 連線。 

+ **RevoPemaR。** PEMA 代表平行外部記憶體演算法。 **RevoPemaR** 封裝提供 API，讓您可用來開發自己的平行演算法。 如需詳細資訊，請參閱 [RevoPemaR 入門指南 (英文)](https://docs.microsoft.com/r-server/r/how-to-developer-pemar)。

我們也建議您試著[MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)，新的封裝，從支援遠端執行 R 程式碼，並可調整的分散式處理的 Microsoft R 使用改善的機器學習服務演算法由 Microsoft Research 所開發。

## <a name="next-steps"></a>後續的步驟

[架構概觀](../../advanced-analytics/r/architecture-overview-sql-server-r.md)

[SQL Server 中支援 R 的元件](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md)

[安全性概觀](../../advanced-analytics/r/security-overview-sql-server-r.md)

