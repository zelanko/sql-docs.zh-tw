---
title: "SQL Server 機器學習服務跨版本的功能可用性 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 16ca6c44b15c9fb7c1983d5a04175ebbade57895
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>跨版本的 SQL Server 機器學習服務的功能可用性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 機器學習功能都可在 SQL Server 2016 和 SQL Server 2017。 本文列出提供此功能的版本、 說明在特定的版本中，將套用的限制，並列出功能僅適用於特定版本。

 > [!NOTE]
 > SQL Server 機器學習服務 （資料庫） 不包含的一般情況下，[實施](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)獨立 R 伺服器或機器學習伺服器安裝中包含的功能。 實施包含 web 服務部署和裝載，並因此競相其他 SQL Server 作業相同的資源。
 > 
 > 基於這個理由，建議您在支援的預測模型的部署為 web 服務的不同實體伺服器上安裝 SQL Server 2016 R 伺服器 （獨立） 或 SQL Server 2017 機器學習伺服器 （獨立）。 

## <a name="sql-server-2017-machine-learning-services-in-database-and-standalone"></a>SQL Server 2017 機器學習服務 （資料庫） 和 （獨立）

Developer Edition 提供相當於 Enterprise Edition 的效能。 使用 Developer Edition 不支援實際執行環境。

|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------|----------|--------|---|------------------------------|-------|
| R 解譯器 （& s) 專屬的封裝 | 是 | 是 | 否 | 否 | 否 | 
| Python 解譯器和用戶端程式庫 | 是 | 是 | 否 | 否 | 否 | 
| 區塊處理的資料 <br/>（處理大量的資料，超過功能放入記憶體中） | 是 | 否 | 否 | 否 | 否 |
| 向上延展處理 <br/>（2 個以上的處理器） | 是 | 否 | 否 | 否 | 否 |
| 實施 | 是 | 否 | 否 | 否 | 否 |
| [預測](../../t-sql/queries/predict-transact-sql.md)函式 <br/>(執行[原生計分](../sql-native-scoring.md)預先定型的模型，先前儲存在所需的二進位格式) | 是 | 是 | 是 | 是 | 是 |
| R 用戶端相容性 | 是 | 是 | 否 | 否 | 否 | 
| Microsoft R Open | 是 | 是 | 否 | 否 | 否 | 
| Anaconda Python 3.5 | 是 | 是 | 否 | 否 | 否 | 

## <a name="sql-server-2016-r-services-in-database-and-r-server-standalone"></a>SQL Server 2016 R 服務 （資料庫） 與 R Server （獨立）

功能可用性等同於 2017，減去 Python 支援未先 2016年版本的一部分。

## <a name="r-feature-availability-in-azure-sql-database"></a>Azure SQL Database 中的 R 功能可用性
  
初始的測試版本發行後 R 服務目前是**不**Azure SQL Database 中，提供暫止的進一步開發之用。 

## <a name="performance-expectations-for-enterprise-edition"></a>適用於 Enterprise Edition 的效能期望

中的機器學習解決方案的效能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]卻通常超越使用傳統的 R，提供相同的硬體實作。 是因為 SQL Server 中的 R 解決方案可以使用來執行伺服器資源，而且有時候散發到使用多個處理程序**RevoScaleR**函式。 

效能已不已進行評估 Python 解決方案的功能是仍在開發，但是一些相同的優點預期要套用。

使用者也可以預期看到效能和延展性，以相同的機器學習解決方案，如果在 Enterprise Edition vs 中執行相當大的差異。Standard Edition 皆執行相同的 R 函數，使用者應該也可以在效能和延展性上看見顯著的差異。 原因包括支援平行處理，增加可用的機器學習的執行緒和串流處理 （或區塊），可讓 RevoScaleR 函數來處理超過可放入記憶體的資料。 

不過，即使在相同硬體上的效能可能會受到許多因素而定的 R 或 Python 程式碼之外。 這些因素包括競爭要求伺服器資源、 所建立的查詢計畫的類型、 結構描述變更，需要更新統計資料，或建立新的查詢計劃、 分散的情形，以及更多。 可能包含 R 或 Python 程式碼可能會執行以秒為單位下一個工作負載，, 但是需要的預存程序分鐘時執行其他服務。  因此，我們建議您監視伺服器效能，測量機器學習效能時，包括遠端計算內容的網路功能的多個層面。

我們也建議您設定[Resource Governor](../../relational-databases/resource-governor/resource-governor.md) （適用於 Enterprise Edition） 來自訂外部指令碼工作的優先順序，或大量伺服器工作負載之下處理方式。 您可以定義分類函數，以指定的外部指令碼作業的來源並優先處理某些工作負載，限制只有 SQL 查詢所使用的記憶體數量及控制使用以工作負載為基礎的平行處理序數目。

## <a name="see-also"></a>另請參閱

+ [SQL Server 2016 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [SQL Server 2017 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [對運算 R （機器學習伺服器） 中的大型資料的秘訣](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
