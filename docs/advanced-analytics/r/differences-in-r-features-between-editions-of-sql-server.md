---
title: SQL Server 機器學習服務跨版本的功能可用性 |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: b64e836dc8969058e5012197e85fa78d40b87ac6
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>跨版本的 SQL Server 機器學習服務的功能可用性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 機器學習功能都可在 SQL Server 2016 和 SQL Server 2017。 本文列出提供此功能的版本、 說明在特定的版本中，將套用的限制，並列出功能僅適用於特定版本。


## <a name="sql-server-2017-features"></a>SQL Server 2017 功能

Enterprise 和 Developer edition 有相同的功能涵蓋範圍，讓您可以建置方案，以便企業安裝，而不會產生相同的成本。 版本的功能相同，雖然使用 Developer Edition 不支援實際執行環境。

基本和進階整合之間的差異是小數位數。 進階的 integration 可用來在您的電腦可以容納任何大小的資料集的平行處理所有可用的核心。 2 核心，以及適合在記憶體中的資料集是基本的整合。 

（資料庫） 執行個體適用於基本和進階的整合。 獨立伺服器不是資料庫引擎執行個體功能，並提供作為安裝選項只在開發人員和 Enterprise 版本中。

|功能|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|基本的 R 整合|是|是|是|是|否|   
|進階的 R 整合|是|否|否|否|否| 
|基本 Python 整合|是|是|是|是|否|
|進階 Python 整合|是|否|否|否|否| 
|Machine Learning 伺服器 (獨立式)|是|否|否|否|否|   

 > [!NOTE]
 > （獨立） 伺服器提供[實施](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)會包含在 Microsoft （非 SQL-品牌） R 伺服器或機器學習伺服器安裝的功能。 實施包含 web 服務部署和裝載功能。
>
> （資料庫） 安裝，運用解決方案的對等方法利用 database engine 功能，當您將程式碼轉換成可以在預存程序中執行的函式。


## <a name="sql-server-2016-r-features"></a>SQL Server 2016 R 功能

SQL Server 2016 包含只 R 整合。 在 SQL Server 2016、 基本和進階的 R 整合相當於 SQL Server 2017。

## <a name="r-feature-availability-in-azure-sql-database"></a>Azure SQL Database 中的 R 功能可用性
  
初始的測試版本發行後 R 服務已從 Azure SQL Database 中，移除暫止的更進一步的開發。 

## <a name="performance-expectations-for-enterprise-edition"></a>適用於 Enterprise Edition 的效能期望

中的機器學習解決方案的效能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]卻通常超越使用傳統的 R，提供相同的硬體實作。 是因為 SQL Server 中的 R 解決方案可以使用來執行伺服器資源，而且有時候散發到使用多個處理程序**RevoScaleR**函式。 

使用者也可以預期看到效能和延展性，以相同的機器學習解決方案，如果在 Enterprise Edition vs 中執行相當大的差異。Standard Edition 皆執行相同的 R 函數，使用者應該也可以在效能和延展性上看見顯著的差異。 原因包括支援平行處理，增加可用的機器學習的執行緒和串流處理 （或區塊），可讓 RevoScaleR 函數來處理超過可放入記憶體的資料。 

不過，即使在相同硬體上的效能可能會受到許多因素而定的 R 或 Python 程式碼之外。 這些因素包括競爭要求伺服器資源、 所建立的查詢計畫的類型、 結構描述變更，需要更新統計資料，或建立新的查詢計劃、 分散的情形，以及更多。 可能包含 R 或 Python 程式碼可能會執行以秒為單位下一個工作負載，, 但是需要的預存程序分鐘時執行其他服務。  因此，我們建議您監視伺服器效能，測量機器學習效能時，包括遠端計算內容的網路功能的多個層面。

我們也建議您設定[Resource Governor](../../relational-databases/resource-governor/resource-governor.md) （適用於 Enterprise Edition） 來自訂外部指令碼工作的優先順序，或大量伺服器工作負載之下處理方式。 您可以定義分類函數，以指定的外部指令碼作業的來源並優先處理某些工作負載，限制只有 SQL 查詢所使用的記憶體數量及控制使用以工作負載為基礎的平行處理序數目。

## <a name="see-also"></a>另請參閱

+ [SQL Server 2016 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [SQL Server 2017 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [對運算 R （機器學習伺服器） 中的大型資料的秘訣](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
