---
title: "機器學習功能的 SQL Server 版本之間的差異 |Microsoft 文件"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9b520b7fc7e97498f4b46a43ad991558025123a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---

# <a name="differences-in-machine-learning-features-between-editions-of-sql-server"></a>機器學習功能的 SQL Server 版本之間的差異
 
 機器學習支援下列版本的 SQL Server 2016 和 SQL Server 2017 有：

## <a name="summary-of-differences"></a>差異的摘要

-   **Enterprise Edition**
    
     SQL Server 2017 包括機器學習服務 （資料庫。 SQL Server 2016 包含 R Services。 此功能支援的資料庫分析在 SQL Server，包括使用 SQL Server 做為運算環境。
     
     SQL Server 2017 包括 Microsoft Machine Learning 伺服器 （獨立）。 SQL Server 2016 包含 Microsoft R Server （獨立）。 此功能支援實施機器學習服務不需要使用 SQL Server 做為運算環境。

     沒有任何限制於這些功能在企業版，提供最佳化的效能和延展性，透過平行處理和串流。 這個版本也最大化平台支援用於串流處理和平行執行。
     
     使用 SQL Server 資料庫中分析支援支援資源監管，外部指令碼，以自訂的伺服器資源使用狀況。
     
     較新版本的 Microsoft R Server 包括實施引擎，可支援快速、 安全部署的改良的版本，且共用的 R 方案。 如需詳細資訊，請參閱[mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)。

-   **Developer Edition**

     具有和 Enterprise Edition 相同的功能，不過 Developer Edition 無法用於實際執行環境。  
  
-   **Standard Edition**

     已分析資料庫中的所有功能都包含使用 Enterprise 版時，除了資源控管。 效能和延展性也是有限： 可以處理的資料必須符合伺服器記憶體，且處理僅限於單一計算執行緒，即使是使用**RevoScaleR**函式。
  
-   **Express 和 Web 版本**
  
     只有 Express Edition with Advanced Services 包含機器學習功能。 效能限制與 Standard Edition 類似。 Web edition 不適合工作，例如建立機器學習模型。不過，您可以使用預測函數來執行計分其他地方使用定型的模型。

-   **Azure SQL Database**
  
     在 Azure SQL Database 目前不支援機器學習功能，例如 R，並將 Python 指令碼。
     
     如需詳細資訊和相關當此功能即將，公告，請參閱 SQL Server 部落格： [Python 中 SQL Server 2017： 增強式資料庫中的機器學習服務](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


### <a name="languages-supported-in-all-editions"></a>所有版本中支援的語言

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

Developer Edition 提供與 Enterprise Edition 相等的效能，不過並不支援在實際執行環境中使用 Developer Edition。

## <a name="machine-learning-in-standard-edition"></a>機器學習中 Standard Edition

在使用相同硬體組態的情況下，與標準 R 封裝相比，Standard Edition 應該可以提供一些效能優點。

Standard Edition 不支援資源管理員。 使用資源管理機制是以自訂伺服器資源用來支援不同的工作負載，例如模型定型和計分的最佳方式。

與 Enterprise Edition 和 Developer Edition 相比，Standard Edition 也只能提供受限制的效能和延展性。 所有**RevoScaleR**函式和封裝已包括 Standard Edition，但它可以使用的處理序數目有限的服務會啟動，並管理 R 指令碼。 此外，由程式碼所處理的資料必須能納入記憶體中。  相同的限制適用於將使用的方案**revoscalepy**。

## <a name="machine-learning-in-express-edition-with-advanced-services"></a>機器學習 Express edition with Advanced Services

Express Edition 具有和 Standard Edition 相同的限制。

## <a name="machine-learning-in-web-edition"></a>機器學習中 Web Edition

Web edition 不支援執行 R 或 Python 指令碼。 不過，您可以使用預測函數來執行[原生計分](../sql-native-scoring.md)定型不同的 SQL Server 或 R Server 執行個體上，則儲存在所需的二進位格式的模型上。

## <a name="next-steps"></a>後續的步驟

如需詳細資訊，請參閱：

+ [SQL Server 2016 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [SQL Server 2017 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2017.md)

如需有關 SQL Server 中的其他功能的詳細資訊，請參閱：

+ [SQL Server 2016 的版本及支援功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) 

如需 Microsoft R 功能及如何最佳化您的方案大型資料集的詳細資訊，請參閱[Microsoft R Server](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)文件。
