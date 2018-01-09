---
title: "部署及使用分析使用 mrsdeploy |Microsoft 文件"
ms.custom: 
ms.date: 08/20/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aea4adeaa86c8e641c44d5b58186247544a0e379
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="deploy-and-consume-analytics-using-mrsdeploy"></a>部署和使用使用 mrsdeploy 分析

Microsoft R Server 包含實施功能， **mrsdeploy**，支援這些工作：

+ 發佈和管理 R，並將 Python 模型和 web 服務的形式的程式碼
+ 使用這些用戶端應用程式內的服務

本主題提供如何啟用和設定功能的相關資訊。

如需支援的案例一般資訊**mrsdeploy**，請參閱[實施 R server](https://docs.microsoft.com/r-server/what-is-operationalization)。

## <a name="using-mrsdeploy-for-operationalization"></a>使用實施 mrsdeploy

Word*實施*可能代表許多的意思：

+ 將模型發行至 web 服務使用，應用程式的能力
+ 可擴充或分散式運算的支援
+ 一次開發、 部署許多次
+ 快速計分，這兩個單一資料列和批次計分

如果您已安裝 SQL server 的機器學習服務*實施*就是您 R 或 Python 程式碼包裝在預存程序。 任何應用程式就可以呼叫預存程序，來重塑模型、 產生分數，或建立報表。 您也可以自動化工作使用 SQL Server 中的現有排程的機制。

不過，Microsoft R Server 提供用於部署支援的不同機制使用來執行分散式的 R 作業支援的 R 工作和一個系統管理公用程式的發行的 web 服務。 Microsoft R Server 會使用中的函式**mrsdeploy**封裝來建立與遠端的計算節點的工作階段，主控台應用程式中執行 R 程式碼。

R 伺服器的這個部署功能可提供下列優勢：

+ 分析 web 服務的角色型存取控制

    決定誰可以發行、 更新和刪除他們自己的 web 服務，也可以更新和刪除的 web 服務的人員發行的其他使用者，以及誰可以只有清單，並使用 web 服務。

+ 更快計分
  
  您可以使用計分與支援的 R 模型物件的即時增進計分作業的速度。

+ 發佈為 web 服務的 Python 程式碼

  如需範例，請參閱[發行和取用的 Python 程式碼](./python/publish-consume-python-code.md)。

+ 非同步批次耗用量

  透過批次執行現在使用以非同步方式呼叫大型的輸入資料的 web 服務。

+ 方格的 [web] 和 [計算] 節點的自動調整

  提供可讓您輕鬆地組織一組的 R 伺服器 Vm 在 Azure 中，然後再進行設定以方格的運用分析和遠端執行的指令碼範本。 此方格可以向上或向下根據 CPU 使用量。

+ 非同步的遠端執行

    現在支援使用**mrsdeploy** R 封裝。 若要繼續在開發環境中使用遠端指令碼執行期間，執行 R 指令碼以非同步方式使用`async`參數。 當您執行長時間執行的指令碼，這是特別有用。

## <a name="requirements-and-configuration"></a>需求和組態

SQL Server 2017 CTP 2.0 和更新版本包含這項功能之前僅能使用 R 伺服器，以及未安裝 SQL Server R services。 **Mrsdeploy**封裝已安裝的 SQL Server 電腦上，如果您選取選項來安裝**Microsoft Machine Learning 伺服器**，從**共用功能**SQL Server 安裝程式一節。

一般而言，我們不建議您在執行 SQL Server 機器學習服務在相同電腦上安裝 Server 機器學習。 我們建議您安裝**Microsoft Machine Learning 伺服器**SQL Server 從一部電腦上，然後設定該電腦上的 實施功能。

不過，如果您需要將其一起安裝，請遵循服務已成功設定下列額外步驟。

1. 安裝 DotNetCore 1.1

    如果.NET Core 還未安裝 SQL Server 的一部分，您必須再開始 R Server 安裝程式來進行安裝。

2. 安裝 Microsoft 機器學習服務伺服器。

3. 安裝程式完成之後**Microsoft Machine Learning 伺服器**，請手動新增下列登錄機碼的**mrsdeploy**，以指定 R_SERVER 檔案的基底資料夾。 

    + 建立新的登錄機碼`H_KEY_LOCAL_MACHINE\SOFTWARE\R Server\Path`
    + 索引鍵的值設定`"C:\Program Files\Microsoft SQL Server\140\R_SERVER"`。

4. 完成，請開啟[管理員公用程式](https://docs.microsoft.com/r-server/operationalize/configure-use-admin-utility)。

5. 繼續設定**mrsdeploy**服務如這裡所述：[系統管理員的組態](https://docs.microsoft.com/r-server/operationalize/configure-start-for-administrators)

6. 如需詳細資訊，請參閱[mrsdeploy 函式](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)。
