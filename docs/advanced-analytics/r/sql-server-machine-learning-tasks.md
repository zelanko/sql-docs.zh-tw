---
title: "SQL Server 機器學習工作 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: c0e7a0929d5caa84df1a1fb02894db08313a36bd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/06/2017

---
# <a name="sql-server-machine-learning-tasks"></a>SQL Server 機器學習服務工作

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 結合了開放原始碼 R 語言搭配企業級工具的威力與彈性，來進行資料儲存與管理、工作流程開發，以及報告和視覺化。 本主題說明在機器學習生命週期，以及 SQL Server 如何支援人員會在機器學習中的 enagged 四個不同資料專業人員的需求。

## <a name="machine-learning-life-cycle"></a>機器學習生命週期

機器學習並不是短期的工作，而是長期處理程序接觸的資料在企業中的所有層面。 機器學習的開頭的業務目標和規則、 識別和感應器和商務應用程式資料的集合。 機器學習多半取決於程序來擷取、 處理和儲存資料，並考量用於儲存、 擷取和稽核資料的原則時，會越來越重要。 最後，機器學習服務現在是報告和分析，以及客戶 engagement 及意見反應的策略的重要 omponent。



SQL Server 是適合 machine learning 中，因為它橋接器許多機器學習程序中出現間距：

+ 適用於內部部署或雲端中
+ 每個階段的企業資料處理，包括商業智慧整合
+ 支援增強的資料安全性
+ 提供資源管理和稽核

## <a name="data-professionals-and-how-they-use-machine-learning"></a>資料專業人員和如何它們使用機器學習服務

### <a name="data-scientists"></a>資料科學家

資料科學家可以存取各種工具來進行資料分析和機器學習，範圍從 Excel 或免費的開放原始碼平台，到昂貴且需要深入技術知識的統計套件。 不過，與 SQL Server 的整合提供獨特的優點：

+ 使用您選擇的 R 開發環境來開發和測試解決方案。
+ 將計算發送到資料庫，避免資料移動，同時又能符合企業安全性原則。
+ 特殊的 R 封裝和應用程式開發介面會改善效能和小數位數。 您就不再受限於單一執行緒、 記憶體繫結架構的 R，並可以處理大型資料集和多執行緒、 多核心、 多處理序的計算。
+ R 程式碼可以輕鬆地部署到生產環境以及企業級工具、 應用程式、 其他資料庫和儀表板所呼叫。
+ 資料科學家可以部署和更新分析解決方案，同時滿足企業資料管理，包括安全性和存取稽核的一般需求
+ 程式碼可攜性： 輕鬆地針對其他資料來源，例如 Hadoop 重新使用您的 R 程式碼

### <a name="application-and-database-developers"></a>應用程式和資料庫開發人員

資料庫開發人員負責將多項技術整合在一起，並集結所有的結果，讓整個企業一起共用。 資料庫開發人員與應用程式開發人員、SQL 開發人員及資料科學家合作設計解決方案、建議資料管理方法，以及架構和部署解決方案。 

與 SQL Server 的整合資料的開發人員使用機器學習服務提供下列優勢：

+ 使用熟悉的工具與 R 指令碼互動。 可讓資料科學家便可在資料開發人員會將使用 SQL Server Management Studio 方案的部署工作中 RStudio。 沒有其他記錄的 R 或 Python 的解決方案。
+ 最佳化混合和比對 SQL 和 R，或 SQL 和 Python。 許多時候複雜的作業，大型資料集可以執行更有效率地使用 T-SQL 中的 SQL Server 功能，例如記憶體 columnstoreindexes 或非常快速的彙總。 使用的機器學習語言是很合理，並使用 SQL 來移動及處理資料。
+ 毫不費力地將大量資料，例如在實際執行資料產生預測分數必須重複執行的工作自動化。
+ 從任何使用應用程式執行 R 或 Python 指令碼[!INCLUDE[tsql](../../includes/tsql-md.md)]。 直接呼叫預存程序來建立參數化的模型、 產生複雜的繪圖，或輸出的預測。
+ **RevoScaleR**和**revoscalepy**應用程式開發介面可以處理大型資料集，並受益於多執行緒、 多核心、 多處理序中的資料庫內部計算。

如需相關工作的資訊，請參閱：
+ [Operationalizing Your R Code](../../advanced-analytics/r-services/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>資料庫管理員

資料庫管理員必須將競爭專案和優先順序整合至單一窗口︰資料庫伺服器。 他們不只應將資料存取權提供給資料科學家，還必須提供給各種報表開發人員、商務分析人員和商務資料取用者，同時維護操作和報告資料存放區的健全狀況。 在企業中，DBA 是建置與部署適用於資料科學之有效基礎結構的一個重要部分。 

SQL Server 提供的資料庫系統管理員必須支援資料科學角色的唯一功能：

+ SQL server 的安全性： 的架構[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]保持您資料庫的安全和隔離的資料庫執行個體的操作的外部指令碼工作階段執行。 您可以指定誰有權限執行機器學習指令碼，以及誰可以安裝新的 R 封裝，使用資料庫角色。

+ R 和 Python 的工作階段會執行不同的處理序，以確保您的伺服器會繼續如往常般執行，即使外部指令碼發生問題。

+ 使用 SQL Server 資源管理機制可讓您控制的記憶體和處理序配置給外部的執行階段，以防止從大量計算危及整體伺服器效能。

如需相關工作的資訊，請參閱：
+ [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

### <a name="architects-and-etl-designers"></a>架構設計人員和 ETL 設計人員

架構設計人員設計跨越機器學習生命週期的所有層面的整合式工作流程。 資料工程師會設計和建置 ETL 解決方案，判斷如何最佳化特徵設計工作的一組屬於的機器學習程序。 通常，整體的資料平台必須設計成競爭及補充商務需求之間取得平衡。

由於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 已與其他 Microsoft 工具密切整合 (例如，商務智慧和資料倉儲堆疊、企業雲端和行動工具，以及 Hadoop)，因此可為想要提升進階分析的資料工程師或系統架構設計人員提供一連串優點。

+ 熟悉的開發工具來開發 R，並將 Python 的方案。 您可以呼叫任何 Python 或 R 指令碼，使用系統預存程序，來填入資料集、 產生圖形，或取得預測。 沒有更多設計平行的工作流程中的資料科學和 ETL 工具。 Azure Data Factory 和 Azure SQL Database 的支援可讓您更容易轉換和管理資料，並使用機器學習工作流程中的雲端資料來源。

+ 排程和管理使用 Microsoft R Server 中實施功能。

如需相關工作的資訊，請參閱：

+ [建立在 SQL Server 中使用 R 的工作流程](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)


