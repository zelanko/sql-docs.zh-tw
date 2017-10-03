---
title: "在 Azure SQL Database 中使用 R |Microsoft 文件"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 619921bbf00801fd5930a1c1b110e69a9fd05a81
ms.contentlocale: zh-tw
ms.lasthandoff: 09/30/2017

---
# <a name="using-r-in-azure-sql-database"></a>在 Azure SQL Database 中使用 R

年 10 月 2017年為準，Azure SQL Database 會支援 R 程式碼中的資料庫使用預存程序，類似於 SQL Server 2016 中的 R 服務的執行。

本文章提供功能的概觀，並說明已知的限制。

> [!NOTE]
> 此版本是初始的預覽版本，並僅供測試和只能瀏覽。 實際執行版本將於 2018年一段時間發行。 確切的發行日期與建置將會根據使用者意見反應。 因此我們建議您嘗試的功能，然後讓我們知道哪些功能很重要。 
> 
> 發行排程的相關資訊，請參閱[SQL Server 部落格](https://blogs.technet.microsoft.com/dataplatforminsider/)或[Microsoft R Server 部落格](https://blogs.msdn.microsoft.com/rserver/)。

## <a name="features"></a>功能

預覽版本提供下列功能：

+ 呼叫以便於部署的機器學習解決方案使用預存程序的 R
+ 取得使用可以連接到您的雲端資料庫的任何應用程式模型中的分數
+ 支援使用預測函數中，而不需使用 R 執行階段快速計分的原生計分

如需預覽版本特有的限制，請參閱[限制與已知的問題](#bkmk_restrictions)。

### <a name="components"></a>Components

整體的架構是類似的 SQL Server 機器 R Services。

**安全性**

+ SQL Server 信任 Launchpad 管理 R 工作的執行，並控制處理程序的存留期。 

**R 封裝**

+ 預覽版本包含 Microsoft R Open 3.3.3，與 Microsoft R Server 9.2 版本。 [RevoScaleR 封裝](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)會預先安裝。

+ 某些 R 封裝已經被移除或修改，以降低 Azure 環境中的使用量。 例如， **mrsdeploy**未包含在 Azure SQL Database。

**[效能]**

+ 定型和計分從任何模型的資料可放入記憶體的支援。  可用的記憶體數量，取決於資料庫的版本。 
+ 使用支援一般的平行處理原則@parallel= 1 個引數，以及執行 R 指令碼資料流 
+ 在預覽中，限制同時執行，每個資料庫的單一 R 指令碼。

**語言**

未來版本藍圖包含其他的封裝和 Python 的支援。

## <a name="restrictions"></a>限制

本節列出一些其他的限制套用至預覽版本。

### <a name="upgrading-r-components-and-adding-packages-not-supported"></a>升級 R 元件，並加入不支援封裝

Azure SQL Database 是受管理的服務，客戶不應該用來管理的 R 元件的升級。 預覽版本，請使用已安裝的套件。

可用時，將會發行到 R 與其他機器學習服務元件的升級。

### <a name="availability"></a>可用性

執行 R 與其他機器學習中 Azure SQL Database 的指令碼的功能是在美國西部地區只是預覽功能。 擴充到其他區域，例如西歐，更新的版本有所規劃。

Azure SQL Database 中執行 R 需要足夠的儲存體和記憶體。 目前支援下列資料庫服務層和效能層級：

+ Premium 服務層： P1、 P2、 P4、 P6、 P11、 P15 
+ Premium RS 服務層： PRS1，PRS2，PRS4 PRS6 
+ 進階彈性集區： 125 Edtu 或更新版本 
+ Premium RS 彈性集區： 125 Edtu 或更新版本 

### <a name="resource-management"></a>資源管理

此版本不支援自訂 R 安裝，或是用來監視使用 R 指令碼的能力。

例如，您無法啟用只在特定資料庫上的執行 R 指令碼。

無法預覽版本提供的 DMV sys.dm_db_resource_stats，用來監視 R 指令碼，CPU 和記憶體使用量。

### <a name="other-limitations"></a>其他限制

不支援下列功能： 

+ 無法使用 MicrosoftML 封裝。
+ 封裝管理功能，例如建立外部程式庫不支援。
+ 從 R 用戶端執行指令碼時，您無法使用 Azure SQL database 做為遠端的運算環境。 必須使用預存程序 sp_execute_external_script 執行 R 指令碼。 呼叫預存程序的指令碼無法使用其他計算內容。
+ 您無法執行需要平行執行的接收函式的呼叫。
+ 從 R 指令碼的回送連接到 SQL Server 不支援。 換句話說，您不能從 R 指令碼外部呼叫另一個 ODBC 資料來源。

## <a name="get-started"></a>快速入門

SQL Server 開發小組的這項公告包含簡短的範例，您可以執行在 Azure SQL 資料庫，以嘗試建立 R 模型及產生預測。

+ [定型和 Azure SQL Database 中的分數模型](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-preview-of-machine-learning-services-with-r-support-in-azure-sql-database/)

