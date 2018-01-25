---
title: "開始使用 SQL Server 機器學習 |Microsoft 文件"
ms.custom: SQL2016_New_Updated
ms.date: 12/07/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: "34"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 8a6e15767282d347fc92b7decf2963d85827cf6f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="getting-started-with-sql-server-machine-learning"></a>開始使用 SQL Server 機器學習

SQL Server 中的機器學習服務被設計來支援資料科學工作而不會暴露安全性風險或移動資料 unnecesarily 資料中。

+ 在 SQL Server 2016 中，您可以使用您最愛的 R 工具，但縮放數十億個資料錄將分析時來提升效能。 整合與 SQL Server 的機器學習也表示，您可以將 R 程式碼放入實際執行而不必重新撰寫程式碼。

+ SQL Server 2017 增加對 Python 程式碼中，支援使用相同的擴充性架構。

本主題描述使用 R 或 Python 資料庫內，進行關鍵案例，並提供資源，可協助您開始使用您自己的解決方案。

適用於： SQL Server 2016 R Services、 SQL Server 2017 機器學習服務 （資料庫）

> [!NOTE]
> SQL Server 2016 包括 R 語言的支援。 Python 語言的支援需要 SQL Server 2017 CTP 2.0。

## <a name="step-1-set-up-sql-server-machine-learning-services"></a>步驟 1： 設定 SQL Server 機器學習服務

1. 執行 SQL Server 安裝程式並安裝 SQL Server 資料庫引擎的至少一個執行個體。
2. 新增支援的外部執行階段執行的功能。
3. 在 SQL Server 2016 中，預設會新增 R。 在 SQL Server 2017，您必須選取要新增的語言。 您可以選取 [R] 或 [Python]，或同時啟用。
4. 當安裝完成後時，執行一些額外的步驟，以啟用外部指令碼執行，並重新啟動伺服器。

**資源**

+ [設定機器學習服務與 SQL Server](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

> [!TIP]  
> 需要為 R 作業建立伺服器，但不需要 SQL Server？ 請嘗試 [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx)。  

## <a name="step-2-develop-your-r-or-python-solutions"></a>步驟 2： 開發 R 或 Python 解決方案

資料科學家通常使用 R 或 Python 自己膝上型電腦或開發工作站上，瀏覽資料，並建置並微調預測模型，直到達成良好的預測模型為止。 

SQL Server 中的機器學習服務，與沒有需要變更此程序。 安裝完成之後，您可以執行 R 或 Python 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機或遠端方式：

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **使用您偏好的 IDE**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 用戶端元件為資料科學家提供了所有進行實驗與開發所需的工具。 這些工具包括 R 執行階段 (大幅提升標準 R 作業效能的 Intel 核心數學程式庫)，以及一組支援在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中執行 R 程式碼的增強型 R 套件。  

+ **使用遠端或本機**。 資料科學家可以連線至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，一如往常將資料帶入用戶端進行本機分析。 但更好的解決方案是使用 **ScaleR** API，將計算推送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦，避免高成本且不安全的資料移動。

+ **內嵌 R 或 Python 指令碼中的[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序**。 當您的程式碼已完整最佳化時，將其包裝在預存程序中，可以避免不必要的資料移動，並最佳化資料處理工作。


**資源**

+ 安裝[R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)或 RStudio。  

## <a name="step-3-optimize"></a>步驟 3： 最佳化

模型上的企業資料縮放就緒時，資料科學家通常能夠搭配 DBA 或 SQL 開發人員最佳化程序，例如：

+ 特徵工程
+ 擷取資料和資料轉換
+ 計分

傳統上使用 R 的資料科學家會有問題的效能和延展性，尤其是使用大型資料集。 這是因為通用執行階段實作是單一執行緒，而且可以容納放入本機電腦上的可用記憶體的資料集。 與 SQl Server 機器學習服務整合提供多項功能，以提升效能、 更多資料：

+ **RevoScaleR**。: 此 R 封裝包含某些熱門 R 函數，經過重新設計可提供平行處理原則與規模的實作。 此套件包含能進一步提升效能與延展性的函數，方法是將計算推送至通常記憶體較大且運算能力更佳的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。

+ **revoscalepy**。 此 Python 程式庫，新的和僅適用於 SQL Server 2017 CTP 2.0 實作 RevoScaleR 中, 最受歡迎的函式，例如遠端計算內容和許多支援的演算法分散式處理。

+ 選擇工作的最佳語言。  R 最適用於統計計算很難使用 SQL 實作。 透過資料的集合式作業，利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]達到最佳效能。 使用記憶體中資料庫引擎非常快速的計算資料行。

**資源**

+ [效能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R 和資料最佳化](../../advanced-analytics/r/r-and-data-optimization-r-services.md)


## <a name="step-4-deploy-and-consume"></a>步驟 4： 部署和使用

R 指令碼或模型可供生產環境使用之後，資料庫開發人員可能會內嵌程式碼或模型預存程序，以便儲存的 R 或 Python 程式碼可以呼叫的應用程式。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 儲存及執行 R 程式碼有許多優點︰您可以使用方便的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 介面和所有發生在資料庫中的計算，避免不必要的資料移動。

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **安全且可延伸**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用全新的擴充性架構，保持您資料庫引擎的安全，並隔離 R 工作階段。 您也可以控制可以執行 R 指令碼的使用者，同時可以指定 R 程式碼可以存取的資料庫。 您可以控制配置給 R 執行階段的資源數量，以避止從大量計算危及整體伺服器效能。

+ **排程和稽核**。 執行外部指令碼工作時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 您可以控制和稽核資料供資料科學家。 您也可以排定工作並撰寫包含外部的 R 或 Python 指令碼，就像任何其他 T-SQL 作業或預存程序，您會排程工作流程。

若要充分利用的資源管理和安全性功能在 SQL Server 中，部署程序可能包括下列工作：

+ 將 R 程式碼轉換成可以在預存程序中以最佳方式執行的函式
+ 設定安全性，以及鎖定特定的工作所使用的封裝
+ 啟用資源管理

**資源**

+ [資源管理針對 R](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [SQL Server 的 R 封裝管理](../../advanced-analytics/r/r-package-management-for-sql-server-r-services.md)

## <a name="quick-starts"></a>快速入門

讀取此逐步解說來了解完整的工作流程，從探索資料建立模型，並將它部署至 SQL Server。

+ [資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

了解如何使用 RevoScaleR 封裝可延展和高效能分析。

+ [資料科學深入探討︰使用 RevoScaleR 套件](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

特別是針對資料開發人員-提供所有的 R 程式碼 ！ 了解如何將 SQL 預存程序來建立，或定型模型，內嵌 R，並從預存的模型取得預測。

+ [適用於 SQL 開發人員的資料庫內進階分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

從預存程序呼叫，了解語法。

+ [在 Transact-SQL 中使用 R 程式碼](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

## <a name="solutions"></a>方案

如需其他範例，包括業界 = 特定解決方案範本，請參閱[SQL Server 機器學習教學課程](../tutorials/machine-learning-services-tutorials.md)。
