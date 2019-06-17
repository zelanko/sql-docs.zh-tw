---
title: 在 Management Studio-SQL Server Machine Learning 服務中使用自訂報表監視 R Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 55fcb4e145481f98b0cba065ddab75e7cfa0a538
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641982"
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>使用 Management Studio 中的自訂報表監視機器學習服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

若要讓您更輕鬆地管理用於機器學習服務的執行個體，產品小組提供了數個您可以加入 SQL Server Management Studio 的範例自訂報告。 在這些報表中，您可以檢視這類詳細資料：

- 使用中的 R 或 Python 的工作階段
- 執行個體的組態設定
- Machine learning 作業的執行統計資料
- R Services 的擴充的事件
- 目前的執行個體上安裝的 R 或 Python 套件

這篇文章說明如何安裝和使用特別針對機器 leaerning 所提供的自訂報表。 

Management Studio 中報表的一般簡介，請參閱 < [Management Studio 中的自訂報表](../../ssms/object/custom-reports-in-management-studio.md)。

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
    > 報表可以搭配 SQL Server 2017 Machiine 學習服務或 SQL Server 2016 R Services。

2. 若要下載這些範例，您也可以登入 GitHub，建立範例的本機分支。 

### <a name="step-2-copy-the-reports-to-management-studio"></a>步驟 2： 將報表複製到 Management Studio

3. 找到 SQL Server Management Studio 使用的自訂報表資料夾。 自訂報表預設儲存在此資料夾中︰
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   但您可以指定不同的資料夾，或建立子資料夾。

4. 將 *.RDL 檔案複製到自訂報表資料夾。


### <a name="step-3-run-the-reports"></a>步驟 3： 執行報表

5. 在 Management Studio 中，以滑鼠右鍵按一下要執行報表的執行個體 [資料庫]  節點。
6. 依序按一下 [報表]  及 [自訂報表]  。
7. 在 [開啟檔案]  對話方塊中，找出自訂報表資料夾。
8. 選取下載的其中一個 RDL 檔案，再按一下 [開啟]  。

> [!IMPORTANT]
> 某些電腦無法使用這些報表，例如顯示裝置解析度高於 1080p 或為高 DPI 的電腦，或處於某些遠端桌面工作階段中的電腦。 SSMS 的報表檢視器控制項中有一個 Bug，會損毀報表。

## <a name="report-list"></a>報表清單

在 GitHub 中的產品範例存放庫目前包含下列報表：

+ **R Services - 使用中的工作階段**

  若要檢視目前連接到 SQL Server 執行個體並執行機器學習工作的使用者使用此報表。 
  
+ **R Services - 組態**

  若要檢視的外部指令碼執行階段和相關的服務組態中使用此報表。 報表會指出是否需要重新啟動，並檢查所需的網路通訊協定。 
  
  隱含的驗證，才能在 SQL Server 作為計算內容中執行的機器學習工作。 若要確認該隱含的驗證設定，報表會驗證群組 SQLRUserGroup 是否存在的資料庫登入。

 + **R Services - 設定執行個體** 

   此報表可協助您設定機器學習服務。 您也可以執行這份報告來修正前一份報表中找到的組態錯誤。
 
+ **R Services - 執行統計資料**

  您可以使用這份報告來檢視 machine learning 作業的執行統計資料。 例如，您可以取得已執行的 R 指令碼總數、平行執行次數和最常使用的 RevoScaleR 函式。 按一下 **檢視 SQL 指令碼**以取得完整 T-SQL 程式碼後置這份報表。

  報表目前只監視 RevoScaleR 套件函式的統計資料。

+ **R Services - 擴充的事件**

  使用此報表以檢視可用來監視外部指令碼執行階段的相關工作的擴充事件清單。 按一下 **檢視 SQL 指令碼**以取得完整 T-SQL 程式碼後置這份報表。

+ **R Services - 套件**

  使用此報表來檢視 SQL Server 執行個體上安裝的 R 或 Python 套件的清單。

+ **R Services - 資源使用狀況**

  使用此報表來檢視外部指令碼執行的 CPU、 記憶體和 I/O 資源耗用量。 您也可以檢視外部資源集區的記憶體設定。

## <a name="see-also"></a>另請參閱

[監視服務](managing-and-monitoring-r-solutions.md)

[R Services 的擴充事件](extended-events-for-sql-server-r-services.md)
