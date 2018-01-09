---
title: "機器學習生命週期和小組流程 |Microsoft 文件"
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: a39a9061df724175d72e4b38c883fdf2495234ad
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="machine-learning-lifecycle-and-personas"></a>機器學習生命週期和角色

因為它們需要的技巧和一組不同專業人員的共同作業，可能很複雜，機器學習服務專案。 本文說明在機器學習生命週期，資料專業人員參與機器學習和 SQL Server 如何支援需求的型別中主要的工作。

> [!TIP]
> 
> 開始在機器學習服務專案之前，我們建議您檢閱的工具和所提供的最佳作法[Microsoft 小組資料科學程序](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/)，或 TDSP。 此程序已建立的機器學習顧問 microsoft 合併計劃和機器學習服務專案上逐一查看的最佳作法。 TDSP 採用業界標準，CRISP-DM，例如具有它的根節點，但是併入最近的作法，例如 DevOps 和視覺效果。

## <a name="machine-learning-life-cycle"></a>機器學習生命週期

機器學習是複雜的程序接觸的資料在企業中，所有層面，而許多機器學習服務專案最後花費的時間，而且比預期更複雜。 以下是一些機器學習服務需要的資料專業人員在企業中支援的方式：

+ 機器學習的目標和商務規則識別碼的開頭。
+ 機器學習專業人員必須知道的儲存、 擷取及稽核資料的原則。
+ 集合可能適用的資料是下一步。  資料來源必須受到識別，並從感應器和商務應用程式擷取適當的資料。 
+ 機器學習工作的品質，多半取決於不只是資料可用，但程序用於擷取、 處理及儲存資料的類型。 
+ 沒有機器學習服務專案將堅固和的策略報告和分析，並可能是客戶參與意見反應。

SQL Server 可協助橋接許多企業資料專業人員和機器學習專家之間的差距：

+ 資料可以儲存在內部部署或雲端中
+ 每個階段的企業資料處理，包括 reporting 和 ETL 整合 SQL Server
+ SQL Server 支援的資料安全性、 資料備援和稽核
+ 提供資源管理

## <a name="data-scientists"></a>資料科學家

資料科學家使用的各種工具進行資料分析和機器學習，範圍從 Excel 或免費的開放原始碼平台，到昂貴且需要深入技術知識的統計套件。 不過，搭配 SQL Server 中使用 R 或 Python 提供相較於這些傳統的工具獨特的優點：

+ 您可以開發和測試解決方案使用您選擇的開發環境，然後部署 R 或 Python 程式碼做為 T-SQL 程式碼的一部分。
+ 將複雜的計算 off，資料科學家的膝上型電腦和伺服器，避免資料移動，以符合企業安全性原則。
+ 特殊的 R 封裝和應用程式開發介面會改善效能和小數位數。 您就不再受限於單一執行緒、 記憶體繫結架構的 R，並可以處理大型資料集和多執行緒、 多核心、 多處理序的計算。
+ 程式碼可攜性： 方案可以在 SQL Server，或執行 Hadoop 或 Linux 中使用[Server 機器學習](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 一次程式碼中，部署任何地方。

## <a name="application-and-database-developers"></a>應用程式和資料庫開發

資料庫開發人員負責將多項技術整合在一起，並集結所有的結果，讓整個企業一起共用。 資料庫開發人員，適用於應用程式開發人員、 SQL 開發人員和資料科學家，來設計解決方案、 建議資料管理方法，和架構設計人員或部署方案。

與 SQL Server 的整合資料開發人員提供許多優點︰

+ 資料科學家可以在工作中 RStudio、 資料開發人員部署使用 SQL Server Management Studio 方案。 沒有其他記錄的 R 或 Python 的解決方案。
+ 使用 T-SQL、 R 和 Python 的最佳最佳化您的方案。 更有效率地使用比 SQL Server 中 r 運用您的資料庫專業人員的知識來改善效能的機器學習解決方案，使用記憶體中資料行存放區索引，就可以執行複雜的作業，大型資料集和使用 SQL 集合式作業的彙總。 
+ 毫不費力地將大量資料，例如在實際執行資料產生預測分數必須重複執行的工作自動化。 
+ 存取參數化 R 或 Python 指令碼會使用任何應用程式從[!INCLUDE[tsql](../../includes/tsql-md.md)]。 直接呼叫預存程序為模型定型、 產生的繪圖，或輸出的預測。
+ 應用程式開發介面可以串流處理大型資料集，並受益於多執行緒、 多核心、 多處理序中的資料庫內部計算。

如需相關工作的資訊，請參閱：
+ [運用您的 R 程式碼](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>資料庫管理員

資料庫管理員必須將競爭專案和優先順序整合至單一窗口︰資料庫伺服器。 他們不只應將資料存取權提供給資料科學家，還必須提供給各種報表開發人員、商務分析人員和商務資料取用者，同時維護操作和報告資料存放區的健全狀況。 在企業中，DBA 是建置與部署適用於資料科學之有效基礎結構的一個重要部分。 

SQL Server 提供的資料庫系統管理員必須支援資料科學角色的唯一功能：

+ SQL server 的安全性： 的架構[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]保持您資料庫的安全和隔離的資料庫執行個體的操作的外部指令碼工作階段執行。 您可以指定誰執行機器學習指令碼，並使用資料庫角色來管理封裝的權限。

+ R 和 Python 的工作階段會執行不同的處理序，以確保您的伺服器會繼續如往常般執行，即使外部指令碼發生問題。

+ 使用 SQL Server 資源管理機制可讓您控制的記憶體和處理序配置給外部的執行階段，以防止從大量計算危及整體伺服器效能。

如需相關工作的資訊，請參閱：
+ [管理及監視機器學習服務方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>架構設計人員及資料工程師

架構設計人員設計跨越機器學習生命週期的所有層面的整合式工作流程。 資料工程師會設計和建置 ETL 解決方案，判斷如何最佳化功能的機器學習的工程工作。 整體的資料平台必須設計成競爭的業務需求之間取得平衡。

由於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 已與其他 Microsoft 工具密切整合 (例如，商務智慧和資料倉儲堆疊、企業雲端和行動工具，以及 Hadoop)，因此可為想要提升進階分析的資料工程師或系統架構設計人員提供一連串優點。

+ 使用系統預存程序，來填入資料集、 產生圖形，或取得預測，以呼叫任何 Python 或 R 指令碼。 沒有更多設計平行的工作流程中的資料科學和 ETL 工具。 Azure Data Factory 和 Azure SQL Database 的支援可讓您更容易使用機器學習工作流程中的雲端資料來源。

+ 排程和管理的機器學習工作，請在 SQL Server 中，根據 Integration Services、 SQL 代理程式或 Azure Data Factory 使用標準的自動化工作流程。 或者，使用[實施功能](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)Server 機器學習中。

如需相關工作的資訊，請參閱：

+ [在 SQL Server 中建立機器學習服務工作流程](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

