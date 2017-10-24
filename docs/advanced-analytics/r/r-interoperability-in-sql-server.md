---
title: "SQL Server R Services 中的 R 互通性 | Microsoft Docs"
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0506b950-34b3-4f11-8e2f-d067a58015bd
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b494e320bf52a98ea02cae6dc3c7feb41aea4217
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="r-interoperability-in-sql-server"></a>SQL Server 中的 R 互通性

本主題著重於 SQL Server 中的執行的機制，並說明 Microsoft R 和開放原始碼 r 的差異

適用於： SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

其他元件的相關資訊，請參閱[SQL Server 中的新元件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md)。

### <a name="open-source-r-components"></a>開放原始碼 R 元件

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 包含一組完整散發的基底 R 封裝和工具。 如需基底散發隨附內容的詳細資訊，請參閱安裝期間安裝於下列預設位置的文件︰`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

在安裝 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 期間，您必須同意 GNU 公用授權的條款。 之後，您就可以執行標準的 R 封裝，而不需進一步修改，就如同在 R 的任何其他開放原始碼散發中一樣。

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 不會以任何方式修改 R 執行階段。 R 執行階段是在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 處理序外部執行，而且可在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 以外獨立執行。 不過，強烈建議您不要在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用 R 時執行這些工具，以避免資源爭用。

與特定 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體相關聯的 R 基底封裝散發，可以在與該執行個體相關聯的資料夾中找到。 比方說，如果您安裝 R 服務的預設執行個體時，R 程式庫位於此資料夾預設：

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library

同樣地，預設執行個體相關聯的 R 工具會依預設位於此資料夾中：

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin

如需 Microsoft R 的不同，您可能會收到來自 CRAN R 基底散發方式的詳細資訊，請參閱[R 語言和 Microsoft R 產品與功能的互通性](https://docs.microsoft.com/en-us/r-server/what-is-r-server-interoperability)

### <a name="additional-r-packages-from-microsoft-r"></a>其他的 R 封裝，從 Microsoft R

除了基底 R 散發，[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]包含某些專屬的 R 封裝，以及用來平行執行的 R，也支援在遠端計算內容中執行 R 的架構。

這個 R 功能的組合 (R 基底散發加上已增強的 R 功能和封裝) 稱為 **Microsoft R**。如果您安裝 Microsoft R Server (獨立式)，就會取得一組與使用 SQL Server R Services (資料庫內) 所安裝封裝完全相同的封裝，但位於不同的資料夾中。

Microsoft R 包括 Intel Math Kernel Library 的散發，這是用來儘可能加快數學處理的速度。 例如，基本線性代數 (BLAS) 程式庫適用於許多附加元件封裝以及 R 本身。 如需詳細資訊，請參閱下列文章：

+ [Intel Math Kernel 如何加快 R 的速度 (英文)](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)
+ [將 R 連結至多執行緒數學程式庫的效能優點 (英文)](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)

Microsoft R 的最重要新增項目包括 **RevoScaleR** 和 **RevoPemaR** 封裝。 這些是已大量使用 C 或 C++ 撰寫以用來獲取較佳效能的 R 封裝。

+ **RevoScaleR。** 包含各種不同的 API 以進行資料操作和分析。 API 已經最佳化，可分析因過大而無法納入記憶體的資料集，以及執行分散在數個核心或處理器上的計算。

   RevoScaleR API 也支援使用資料子集來獲取更佳的延展性。 換句話說，大多數 RevoScaleR 函數都可在資料區塊上運作，並使用更新演算法來彙總結果。 因此，以 RevoScaleR 函數為基礎的 R 方案可以使用非常大型的資料集，而且不會受限於本機記憶體。

  RevoScaleR 封裝也支援 .XDF 檔案格式，以便更快速移動和儲存用於分析的資料。 XDF 格式會使用單欄式儲存體、具可攜性，且可用來從各種來源載入然後操作資料，包括文字、SPSS 或 ODBC 連線。 

+ **RevoPemaR。** PEMA 代表平行外部記憶體演算法。 **RevoPemaR** 封裝提供 API，讓您可用來開發自己的平行演算法。 如需詳細資訊，請參閱 [RevoPemaR 入門指南 (英文)](https://docs.microsoft.com/r-server/r/how-to-developer-pemar)。

我們也建議您嘗試[MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)，新的封裝，從 Microsoft R，支援遠端執行 R 程式碼和可延展分散處理，使用提升的機器學習演算法由 Microsoft Research 開發。

## <a name="next-steps"></a>後續的步驟

[架構概觀](../../advanced-analytics/r/architecture-overview-sql-server-r.md)

[SQL Server 中支援 R 的元件](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md)

[安全性概觀](../../advanced-analytics/r/security-overview-sql-server-r.md)


