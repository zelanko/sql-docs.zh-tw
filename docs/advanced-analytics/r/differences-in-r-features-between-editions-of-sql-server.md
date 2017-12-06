---
title: "機器學習功能的 SQL Server 版本之間的差異 |Microsoft 文件"
ms.custom: 
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e599ab78d2b6a6ede13b1da1e6edf5167405fc2c
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="differences-in-machine-learning-features-between-editions-of-sql-server"></a>機器學習功能的 SQL Server 版本之間的差異
 
 使用 SQL Server 2016 和 SQL Server 2017 機器學習的支援。 本文列出支援功能的版本、 說明套用在特定的版本中的其他限制，並列出功能僅適用於特定版本。

 > [!NOTE]
 > 一般情況下，並不包含 SQL Server 機器學習[實施](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)Microsoft R Server 或 Server 機器學習中所包含的功能。
 > 
 > 如果您需要這些功能，您可以安裝 Microsoft R Server 機器學習分開，以支援的預測模型的部署為 web 服務。 

## <a name="summary-of-differences"></a>差異的摘要

-   **Enterprise Edition**
    
     SQL Server 2017 包括機器學習服務 （資料庫。 SQL Server 2016 包含 R Services。 此功能支援的資料庫分析在 SQL Server，包括使用 SQL Server 做為運算環境。
     
     SQL Server 2017 包括 Microsoft Machine Learning 伺服器 （獨立）。 SQL Server 2016 包含 Microsoft R Server （獨立）。 此功能支援實施機器學習服務不需要使用 SQL Server 做為運算環境。

     沒有任何限制於這些功能在企業版，提供最佳化的效能和延展性，透過平行處理和串流。 這個版本也最大化平台支援用於串流處理和平行執行。 這表示，不同於 Standard Edition 中，輸入資料不需要放入記憶體，但是可以資料流處理。
     
     使用 SQL Server 資料庫中分析支援支援資源監管，外部指令碼，以自訂的伺服器資源使用狀況。
     
     較新版本的 Microsoft R Server 和機器學習伺服器包括實施引擎，可支援快速、 安全部署的改良的版本，且共用的 R 方案。 如需詳細資訊，請參閱[實施 analytics 使用機器學習 Server](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)。

-   **Developer Edition**

     具有和 Enterprise Edition 相同的功能，不過 Developer Edition 無法用於實際執行環境。  
  
-   **Standard Edition**

     已分析資料庫中的所有功能都包含使用 Enterprise 版時，除了資源控管。 效能和延展性也會受到限制： 可以處理的資料必須符合伺服器記憶體，且處理僅限於單一計算執行緒，即使是使用**RevoScaleR**函式。
  
-   **Express 和 Web 版本**
  
     只有 Express Edition with Advanced Services 包含機器學習功能。 效能限制與 Standard Edition 類似。 
     
     Web Edition 不適合工作，例如建立機器學習模型。 不過，您可以使用預測函數來執行計分其他地方使用定型的模型。

-   **Azure SQL Database**
  
     初始的測試版本發行後 R 服務目前是**不**Azure SQL Database 中，提供暫止的進一步開發之用。 

### <a name="external-script-languages-supported"></a>支援的外部指令碼語言

所有版本都支援下列機器學習語言：

+ SQL Server 2017: R 和 Python
+ 只有 SQL Server 2016: R

Microsoft R Open 包含在所有版本內。

Microsoft R Client 可以搭配所有版本運作。

## <a name="machine-learning-in-enterprise-edition"></a>機器學習在企業版

中的機器學習解決方案的效能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]卻通常超越使用傳統的 R，提供相同的硬體實作。 是因為 SQL Server 中的 R 解決方案可以使用來執行伺服器資源，而且有時候散發到使用多個處理程序**RevoScaleR**函式。 

效能已不已進行評估 Python 解決方案的功能是仍在開發，但是一些相同的優點預期要套用。

使用者也可以預期看到效能和延展性，以相同的機器學習解決方案，如果在 Enterprise Edition vs 中執行相當大的差異。Standard Edition 皆執行相同的 R 函數，使用者應該也可以在效能和延展性上看見顯著的差異。 原因包括支援平行處理，增加可用的機器學習的執行緒和串流處理 （或區塊），可讓 RevoScaleR 函數來處理超過可放入記憶體的資料。 

不過，即使在相同硬體上的效能可能會受到許多因素而定的 R 或 Python 程式碼之外。 這些因素包括競爭要求伺服器資源、 所建立的查詢計畫的類型、 結構描述變更，需要更新統計資料，或建立新的查詢計劃、 分散的情形，以及更多。 可能包含 R 或 Python 程式碼可能會執行以秒為單位下一個工作負載，, 但是需要的預存程序分鐘時執行其他服務。  因此，我們建議您監視伺服器效能，測量機器學習效能時，包括遠端計算內容的網路功能的多個層面。

我們也建議您設定[Resource Governor](../../relational-databases/resource-governor/resource-governor.md) （適用於 Enterprise Edition） 來自訂外部指令碼工作的優先順序，或大量伺服器工作負載之下處理方式。 您可以定義分類函數，以指定的外部指令碼作業的來源並優先處理某些工作負載，限制只有 SQL 查詢所使用的記憶體數量及控制使用以工作負載為基礎的平行處理序數目。

## <a name="machine-learning-in-developer-edition"></a>機器學習中 Developer Edition

Developer Edition 提供相當於 Enterprise Edition 的效能。

使用 Developer Edition 不支援實際執行環境。

## <a name="machine-learning-in-standard-edition"></a>機器學習中 Standard Edition

在使用相同硬體組態的情況下，與標準 R 封裝相比，Standard Edition 應該可以提供一些效能優點。

Standard Edition 不支援資源管理員。 標準版也提供有限的效能和延展性，相較於 Enterprise 和 Developer edition。

所有**RevoScaleR**函式和封裝已包括 Standard Edition，但它可以使用的處理序數目有限的服務會啟動，並管理 R 指令碼。 此外，由程式碼所處理的資料必須能納入記憶體中。

相同的限制適用於將使用的方案**revoscalepy**。

## <a name="machine-learning-in-express-edition-with-advanced-services"></a>機器學習 Express edition with Advanced Services

Express Edition 具有和 Standard Edition 相同的限制。

## <a name="machine-learning-in-web-edition"></a>機器學習中 Web Edition

Web edition 不支援執行 R 或 Python 指令碼。 不過，您可以使用[預測](../../t-sql/queries/predict-transact-sql.md)函式來執行[原生計分](../sql-native-scoring.md)定型不同的 SQL Server 或 R Server 執行個體上，則儲存在所需的二進位格式的模型上。

## <a name="next-steps"></a>後續的步驟

如需詳細資訊，請參閱：

+ [SQL Server 2016 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [SQL Server 2017 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2017.md)

如需有關 SQL Server 中的其他功能的詳細資訊，請參閱：

+ [版本和支援的 SQL Server 2016 功能](../../sql-server/editions-and-components-of-sql-server-2016.md) 

如需有關如何最佳化您的方案大型資料集的詳細資訊，請參閱[計算大型的資料，在 R 的秘訣](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)文件。
