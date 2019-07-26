---
title: 在 Management Studio 中使用自訂報表監視 R Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: effcfe458fc004fd8fb44bb58095e91a2fb56b8d
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470062"
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>使用 Management Studio 中的自訂報表監視機器學習服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

為了讓您更輕鬆地管理用於機器學習服務的實例, 產品小組已提供一些您可以新增至 SQL Server Management Studio 的範例自訂報表。 在這些報告中, 您可以查看詳細資料, 例如:

- Active R 或 Python 會話
- 實例的配置設定
- 機器學習作業的執行統計資料
- R Services 的擴充事件
- 安裝在目前實例上的 R 或 Python 套件

本文說明如何安裝和使用專為機器 leaerning 所提供的自訂報表。 

如需 Management Studio 中報表的一般簡介, 請參閱[Management Studio 中的自訂報表](../../ssms/object/custom-reports-in-management-studio.md)。

## <a name="how-to-install-the-reports"></a>如何安裝報表

報表是使用 SQL Server Reporting Services 設計而成，但可直接從 SQL Server Management Studio 使用，即使執行個體上未安裝 Reporting Services 亦可。 

使用這些報表︰

* 從 GitHub 存放庫下載 RDL 檔案以取得 SQL Server 產品範例。
* 將檔案新增至 SQL Server Management Studio 所使用的自訂報表資料夾。
* 在 SQL Server Management Studio 中開啟報表。


### <a name="step-1-download-the-reports"></a>步驟 1： 下載報表

1. 開啟包含[SQL Server 產品範例](https://github.com/Microsoft/sql-server-samples)的 GitHub 存放庫, 並下載範例報表。 

    + [SSMS 自訂報表](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

    > [!NOTE]
    > 這些報告可以搭配 SQL Server 2017 Machiine Learning 服務, 或 SQL Server 2016 R Services 使用。

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

## <a name="report-list"></a>報表清單

GitHub 中的產品範例存放庫目前包含下列報告:

+ **R Services - 使用中的工作階段**

  使用此報表來查看目前已連線至 SQL Server 實例並執行機器學習作業的使用者。 
  
+ **R Services - 組態**

  使用此報表來查看外部腳本執行時間和相關服務的設定。 報表會指出是否需要重新啟動，並檢查所需的網路通訊協定。 
  
  在 SQL Server 中執行作為計算內容的機器學習工作需要有隱含的驗證。 若要確認是否已設定隱含驗證, 報表會驗證群組 SQLRUserGroup 是否有資料庫登入。

 + **R Services - 設定執行個體** 

   此報表旨在協助您設定機器學習服務。 您也可以執行這份報表, 以修正上述報告中所找到的設定錯誤。
 
+ **R Services - 執行統計資料**

  使用此報表可查看機器學習作業的執行統計資料。 例如，您可以取得已執行的 R 指令碼總數、平行執行次數和最常使用的 RevoScaleR 函式。 按一下 [ **VIEW SQL Script** ] 以取得此報表背後的完整 t-sql 程式碼。

  報表目前只監視 RevoScaleR 套件函式的統計資料。

+ **R Services - 擴充的事件**

  使用此報表來查看可用於監視與外部腳本執行時間相關之工作的擴充事件清單。 按一下 [ **VIEW SQL Script** ] 以取得此報表背後的完整 t-sql 程式碼。

+ **R Services - 套件**

  使用此報表來查看 SQL Server 實例上所安裝的 R 或 Python 套件清單。

+ **R Services - 資源使用狀況**

  使用此報表可透過外部腳本執行, 來查看 CPU、記憶體和 i/o 資源的耗用量。 您也可以檢視外部資源集區的記憶體設定。

## <a name="see-also"></a>另請參閱

[監視服務](managing-and-monitoring-r-solutions.md)

[R Services 的擴充事件](extended-events-for-sql-server-r-services.md)
