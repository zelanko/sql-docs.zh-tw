---
title: 機器學習服務生命週期和小組程序-SQL Server 機器學習服務
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4d19c103f2e90220bc7d80a1da65eb0352252ad6
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511285"
---
# <a name="machine-learning-lifecycle-and-personas"></a>機器學習服務生命週期和角色
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

因為它們需要的技能與專業人員一不同組的共同作業，可能很複雜，機器學習專案。 本文說明機器學習服務生命週期，資料專業人員參與 machine learning 和 SQL Server 如何支援需求的型別中主要的工作。

> [!TIP]
> 
> 您開始使用 machine learning 專案之前，我們建議您檢閱的工具與所提供的最佳做法[Microsoft Team Data Science Process](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/)，或 TDSP。 此程序已建立的機器學習合併計劃和反覆進行機器學習服務專案的最佳作法的 microsoft 的顧問。 TDSP 的根源在於 CRISP-DM，等業界標準，但包含最近的作法，例如 DevOps 和視覺效果。

## <a name="machine-learning-life-cycle"></a>機器學習服務生命週期

Machine learning 是複雜的程序所接觸的資料，在企業中，所有層面，最後會花費的時間，比預期還更複雜的許多機器學習專案。 以下是一些機器學習服務，需要在企業中的資料專業人員的支援方式：

+ 機器學習服務開始的目標，以及商務規則的識別碼。
+ 機器學習服務專業人員必須知道的儲存、 擷取及稽核資料的原則。
+ 集合可能適用的資料是下一步。  必須識別資料來源，並從感應器和商務應用程式中擷取適當的資料。 
+ 機器學習服務工作品質是高度依賴不只是資料可用，但程序用來擷取、 處理和儲存資料的類型。 
+ 任何機器學習服務專案就不算完整報告和分析，並可能是客戶參與及意見反應的策略。

SQL Server 可協助您搭起橋樑的企業資料專業人員和機器學習專家之間的差距，許多：

+ 資料可以儲存在內部部署或雲端中
+ SQL Server 整合的企業資料處理，包括 reporting 和 ETL 每個階段
+ SQL Server 支援的資料安全性、 資料備援和稽核
+ 提供資源管理

## <a name="data-scientists"></a>資料科學家

資料科學家使用各種工具，進行資料分析和機器學習，範圍從 Excel 或免費的開放原始碼平台，到昂貴需要深入技術知識的統計套件。 不過，使用 R 或 Python 與 SQL Server 所提供的一些獨特的優點，相較於這些傳統工具：

+ 您可以開發和測試解決方案，使用您選擇的開發環境，然後將您的 R 或 Python 程式碼部署為 T-SQL 程式碼的一部分。
+ 將複雜的計算資料科學家的膝上型電腦關閉，然後到伺服器，避免資料移動，以符合企業安全性原則。
+ 透過特殊的 R 封裝與 Api 已獲得改善的效能和延展性。 您就不再受限於單一執行緒與記憶體繫結架構的 R，並可以處理大型資料集和多執行緒、 多核心、 多處理序的計算。
+ 程式碼可攜性：解決方案可以在 SQL Server，或執行 Hadoop 或 Linux 中使用[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 程式碼一次，隨處部署。

## <a name="application-and-database-developers"></a>應用程式和資料庫開發人員

資料庫開發人員負責將多項技術整合在一起，並集結所有的結果，讓整個企業一起共用。 資料庫開發人員與應用程式開發人員、 SQL 開發人員和資料科學家，來設計解決方案、 建議資料管理方法，和架構設計人員或部署解決方案。

與 SQL Server 整合資料開發人員提供許多優點︰

+ 資料科學家可在 RStudio 中，而資料開發人員部署使用 SQL Server Management Studio 的方案。 沒有更多重新編碼的 R 或 Python 的解決方案。
+ 使用最佳的 T-SQL、 R 和 Python，以最佳化您的解決方案。 更有效地使用比 SQL Server 中 r 運用您的資料庫專業人員的知識來改善效能的機器學習服務解決方案，使用記憶體中資料行存放區索引，就可以執行複雜的作業，大型資料集和使用 SQL 集合式作業的彙總。 
+ 輕鬆將大量資料，例如在實際執行資料產生預測分數必須重複執行的工作自動化。 
+ 存取參數化 R 或 Python 指令碼會使用任何應用程式從[!INCLUDE[tsql](../../includes/tsql-md.md)]。 只要呼叫來定型模型、 產生繪圖，或輸出預測的預存程序。
+ Api 可以串流處理大型資料集，並受益於多執行緒、 多核心、 多處理序在資料庫內計算。

如需相關工作的資訊，請參閱：
+ [運用您的 R 程式碼](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>資料庫管理員

資料庫管理員必須將競爭專案和優先順序整合至單一窗口︰資料庫伺服器。 他們不只應將資料存取權提供給資料科學家，還必須提供給各種報表開發人員、商務分析人員和商務資料取用者，同時維護操作和報告資料存放區的健全狀況。 在企業中，DBA 是建置與部署適用於資料科學之有效基礎結構的一個重要部分。 

SQL Server 提供的資料庫系統管理員必須支援資料科學角色的獨特功能：

+ SQL server 的安全性：架構[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]保護您資料庫的安全和隔離的資料庫執行個體作業的外部指令碼工作階段的執行。 您可以指定誰可以執行機器學習服務指令碼，並使用資料庫角色來管理封裝的權限。

+ R 和 Python 的工作階段會執行在不同的處理序，以確保您的伺服器會繼續如往常般執行，即使外部指令碼發生問題。

+ 使用 SQL Server 的資源管理可讓您控制記憶體和處理序配置給外部的執行階段中，以避免大量計算危及整體伺服器效能。

如需相關工作的資訊，請參閱：
+ [管理及監視機器學習服務方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>架構設計人員和資料工程師

架構設計人員設計跨機器學習服務生命週期的各個層面的整合工作流程。 資料工程師會設計和建置 ETL 解決方案，判斷如何最佳化適用於 machine learning 的功能工程工作。 整體的資料平台必須設計成競爭的業務需求之間取得平衡。

由於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 已與其他 Microsoft 工具密切整合 (例如，商務智慧和資料倉儲堆疊、企業雲端和行動工具，以及 Hadoop)，因此可為想要提升進階分析的資料工程師或系統架構設計人員提供一連串優點。

+ 使用系統預存程序，來填入資料集、 產生圖形，或取得預測，以呼叫任何 Python 或 R 指令碼。 沒有更多設計平行的工作流程中的資料科學和 ETL 工具。 支援 Azure Data Factory 和 Azure SQL Database 可讓您更輕鬆地使用雲端機器學習服務工作流程中的資料來源。

+ 排程和管理機器學習服務工作，請在 SQL Server 中，根據 Integration Services、 SQL 代理程式或 Azure Data Factory 使用標準的自動化工作流程。 或者，您也可以使用[運算化功能](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)在 Machine Learning Server。

如需相關工作的資訊，請參閱：

+ [在 SQL Server 中建立機器學習服務工作流程](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

