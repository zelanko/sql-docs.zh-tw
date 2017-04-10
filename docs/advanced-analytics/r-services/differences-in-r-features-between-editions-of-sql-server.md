---
title: "R 功能的 SQL Server 版本之間的差異 | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# R 功能的 SQL Server 版本之間的差異
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 在下列版本的可用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   **Enterprise Edition**  
    
     包含這兩個 R 服務，在資料庫中 SQL Server 2016，以及在 Windows 中，這可以用來連接到各種不同的資料庫和提取資料的小數位數，在分析，但是它不會執行資料庫中的 R 伺服器 （獨立） 的分析。 也包含 **DeployR**, ，這可以用來將 R 指令碼和模型部署為 Web 服務。  

     無限制。 最佳化的效能和延展性，透過平行處理和串流處理。 不適合在可用的記憶體中，使用大型資料集的 Suopprts 分析 **ScaleR** 函式。  
  
     SQL Server 中的資料庫中分析支援外部指令碼來自訂伺服器資源使用的資源管理。  
  
-   **Developer Edition**  

    相同的功能，為企業版。不過，開發人員版本不能在實際執行環境。  

  
  
-   **Standard Edition**  
  
     具有分析資料庫中的所有功能都隨附企業版中，除了有彈性的資源控管。 效能和延展性也是限制︰ 可以處理的資料，伺服器記憶體不足，而且處理受限於單一計算執行緒，即使是使用 **ScaleR** 函式。
  
-   **Express 版本**  
  
     只有 Express Edition with Advanced Services 提供 R 服務。 效能限制是類似於標準版。  
  
 如需其他產品功能的詳細資訊，請參閱 [支援的 SQL Server 2016 的版本功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  

> [!NOTE]
>
> + Microsoft R Open 是隨附於所有版本。
> + Microsoft R 用戶端可以使用的所有版本。
  
## Enterprise Edition  
 R 中的解決方案的效能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預計通常會比任何傳統 R 實作中，指定相同的硬體，因為可以使用伺服器資源來執行 R 和有時候散發到多個處理序使用 **ScaleR** 函式。  
  
 使用者也可以預期看到效能和延展性，以相同的 R 函數執行 Enterprise Edition vs 中相當大的差異。標準版。 原因包括支援平行處理、 資料流，以及增加可用的 R 背景工作處理的執行緒。  
  
 不過，即使在相同硬體上的效能可能會受到許多因素，包括競爭伺服器資源需求、 所建立的查詢計畫的類型、 結構描述變更的 R 程式碼之外需要更新統計資料或建立新的查詢計劃、 分散程度，以及更多內容。 也可包含的 R 程式碼可能會執行以秒為單位下一個工作負載，, 但是需要的預存程序分時執行其他服務。  因此，我們建議您監視伺服器效能，當量化 R 工作的效能，包括遠端計算內容的網路功能的多種層面。  

我們也建議您設定 [資源管理員](../../relational-databases/resource-governor/resource-governor.md) （適用於企業版） 來自訂 R 作業會排列優先順序或處理大量伺服器工作負載下的方式。 您可以定義分類函數指定 R 工作的來源和優先處理某些工作負載、 限制的 SQL 查詢所使用的記憶體量，並控制使用的工作負載為基礎的平行處理序數目。  
  
## Developer Edition  
 Developer Edition 提供同等的 Enterprise Edition 的效能不過，開發人員版本的使用不支援實際執行環境。  
  
  
## Standard Edition  
 Standard Edition 甚至應該提供一些效能優點，相較於標準的 R 封裝提供相同的硬體設定。  
  
 不過，標準版不支援資源管理員。 使用資源管理員是自訂伺服器資源來支援各種的 R 工作負載，例如訓練與評分模型的最佳方式。  
  
 標準版也提供有限的效能和延展性，相較於 Enterprise 與 Developer 版本。 具體而言，所有的 **ScaleR** 函式和封裝已包括標準版，但它可以使用的處理序數目有限的服務，會啟動，並管理 R 指令碼。 此外，指令碼處理的資料必須納入記憶體中。  
  
  
## Express Edition with Advanced Services  
 Express Edition 受限於標準版相同的限制。  
  
## 另請參閱  
 [SQL Server 2016 版本支援的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  