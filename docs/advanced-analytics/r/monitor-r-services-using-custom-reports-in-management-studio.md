---
title: "使用 Management Studio 中的自訂報表監視 R Services | Microsoft Docs"
ms.custom: 
ms.date: 10/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5933c72c-ba63-4966-b882-75719ef8428e
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 141d0e3114a59a9b280ceee6d599f97ef16919c7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>監視使用 Management Studio 中自訂報告的機器學習服務

若要讓您輕鬆地管理用於機器學習服務執行個體，產品團隊提供數個範例自訂報告，您可以加入 SQL Server Management Studio。 在這些報表中，您可以檢視這類詳細資料：

- 使用中的 R 或 Python 的工作階段
- 執行個體的組態設定
- 機器學習工作的執行統計資料
- R 服務的擴充的事件
- 目前的執行個體上安裝 R 或 Python 封裝

本文說明如何安裝及使用特別為機器 leaerning 所提供的自訂報表。 

Management Studio 中報表的一般簡介，請參閱[在 Management Studio 中的自訂報告](../../ssms/object/custom-reports-in-management-studio.md)。

## <a name="how-to-install-the-reports"></a>如何安裝報表

報表是使用 SQL Server Reporting Services 設計而成，但可直接從 SQL Server Management Studio 使用，即使執行個體上未安裝 Reporting Services 亦可。 

使用這些報表︰

* 從 GitHub 存放庫下載 RDL 檔案以取得 SQL Server 產品範例。
* 將檔案新增至 SQL Server Management Studio 所使用的自訂報表資料夾。
* 在 SQL Server Management Studio 中開啟報表。


### <a name="step-1-download-the-reports"></a>步驟 1： 下載報表

1. 開啟包含 GitHub 儲存機制[SQL Server 產品範例](https://github.com/Microsoft/sql-server-samples)，並下載範例報表。 

    + [SSMS 自訂報表](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

    > [!NOTE]
    > 報表可以搭配 SQL Server 2017 Machiine 學習 Services 或 SQL Server 2016 R Services。

2. 若要下載這些範例，您也可以登入 GitHub，建立範例的本機分支。 

### <a name="step-2-copy-the-reports-to-management-studio"></a>步驟 2： 將報表複製到 Management Studio

3. 找到 SQL Server Management Studio 使用的自訂報表資料夾。 自訂報表預設儲存在此資料夾中︰
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   但您可以指定不同的資料夾，或建立子資料夾。

4. 將 *.RDL 檔案複製到自訂報表資料夾。


### <a name="step-3-run-the-reports"></a>步驟 3： 執行報表

5. 在 Management Studio 中，以滑鼠右鍵按一下要執行報表的執行個體 [資料庫]  節點。
6. 依序按一下 [報表] 及 [自訂報表] 。
7. 在 [開啟檔案]  對話方塊中，找出自訂報表資料夾。
8. 選取下載的其中一個 RDL 檔案，再按一下 [開啟] 。

> [!IMPORTANT]
> 某些電腦無法使用這些報表，例如顯示裝置解析度高於 1080p 或為高 DPI 的電腦，或處於某些遠端桌面工作階段中的電腦。 SSMS 的報表檢視器控制項中有一個 Bug，會損毀報表。

## <a name="report-list"></a>報告清單

產品範例儲存機制，在 GitHub 中的目前包含下列報表：

+ **R Services - 使用中的工作階段**

  使用此報表來檢視目前連接到 SQL Server 執行個體並執行機器學習工作的使用者。 
  
+ **R Services - 組態**

  若要檢視的外部指令碼執行階段和相關的服務組態使用此報表。 報表會指出是否需要重新啟動，並檢查所需的網路通訊協定。 
  
  隱含的驗證，才能在 SQL Server 做為運算環境中執行的機器學習工作。 若要確認設定，隱含的驗證，此報表會確認群組 SQLRUserGroup 是否存在的資料庫登入。

 + **R Services - 設定執行個體** 

   此報表被要幫助您設定機器學習。 您也可以執行此報表來修正之前的報表中找到的組態錯誤。
 
+ **R Services - 執行統計資料**

  您可以使用這份報表來檢視機器學習工作的執行統計資料。 例如，您可以取得已執行的 R 指令碼總數、平行執行次數和最常使用的 RevoScaleR 函式。 按一下**檢視 SQL 指令碼**取得這份報告背後的完整 T-SQL 程式碼。

  報表目前只監視 RevoScaleR 套件函式的統計資料。

+ **R Services - 擴充的事件**

  使用此報表來檢視擴充事件，可供監視與外部指令碼執行階段相關的工作清單。 按一下**檢視 SQL 指令碼**取得這份報告背後的完整 T-SQL 程式碼。

+ **R Services - 套件**

  使用此報表來檢視 SQL Server 執行個體上安裝的 R 或 Python 封裝清單。

+ **R Services - 資源使用狀況**

  使用此報表來檢視外部指令碼執行的 CPU、 記憶體和 I/O 資源耗用量。 您也可以檢視外部資源集區的記憶體設定。

## <a name="see-also"></a>另請參閱

[監視 R Services](../../advanced-analytics/r-services/monitoring-r-services.md)

[R Services 的擴充事件](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)
