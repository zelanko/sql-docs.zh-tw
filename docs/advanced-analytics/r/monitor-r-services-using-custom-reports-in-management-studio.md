---
title: "使用 Management Studio 中的自訂報表監視 R Services | Microsoft Docs"
ms.custom: 
ms.date: 02/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5933c72c-ba63-4966-b882-75719ef8428e
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14f6d6d7373afd452f06acae43f7023de136bc71
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="monitor-r-services-using-custom-reports-in-management-studio"></a>使用 Management Studio 中的自訂報表監視 R Services
為易於管理 SQL Server R Services，產品小組提供了多個您可以新增至 SQL Server Management Studio 的範例自訂報表，以檢視 R Services 詳細資料，例如︰

- 使用中的 R 工作階段清單
- 目前執行個體的 R 組態
- R 執行階段的執行統計資料
- R Services 的擴充事件清單
- 目前的執行個體上所安裝的 R 套件清單

本主題說明如何安裝和使用報表。 如需 Management Studio 自訂報表的詳細資訊，請參閱 [Management Studio 中的自訂報表](~/ssms/object/custom-reports-in-management-studio.md)。

## <a name="how-to-install-the-reports"></a>如何安裝報表

報表是使用 SQL Server Reporting Services 設計而成，但可直接從 SQL Server Management Studio 使用，即使執行個體上未安裝 Reporting Services 亦可。 

使用這些報表︰

* 從 GitHub 存放庫下載 RDL 檔案以取得 SQL Server 產品範例。
* 將檔案新增至 SQL Server Management Studio 所使用的自訂報表資料夾。
* 在 SQL Server Management Studio 中開啟報表。


### <a name="step-1-download-the-reports"></a>步驟 1： 下載報表

1. 開啟包含 [SQL Server 產品範例 (英文)](https://github.com/Microsoft/sql-server-samples) 的 GitHub 存放庫，並從此頁面下載範例報表： 

   + [SSMS 自訂報表](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/ssms-custom-reports)
      
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

GitHub 的產品範例存放庫目前包含下列 SQL Server R Services 報表︰

+ **R Services - 使用中的工作階段**

  使用本報表檢視目前連接到 SQL 執行個體並執行 R 作業的使用者。 
  
+ **R Services - 組態**

  使用本報表檢視 R 執行階段和 R Services 組態的屬性。 報表會指出是否需要重新啟動，並檢查所需的網路通訊協定。 
  
  在 SQL 計算內容中執行 R 時需要隱含驗證，為檢查此項目，報表會驗證群組 SQLRUserGroup 是否有資料庫登入存在。

  > [!NOTE]
  > 如需有關這些欄位的詳細資訊，請參閱 Hadley Wickam 執筆的 [Package metadata](http://r-pkgs.had.co.nz/description.html)(套件中繼資料)。 例如，推出 R 執行階段的 *Nickname* 欄位，以協助區分版本。 

 + **R Services - 設定執行個體** 

   這份報表目的為幫助您在安裝後設定 R Services。 若未正確設定 R Services，您可以在前一份報表中加以執行。
 
+ **R Services - 執行統計資料**

  使用本報表檢視 R Services 的執行統計資料。 例如，您可以取得已執行的 R 指令碼總數、平行執行次數和最常使用的 RevoScaleR 函式。
  報表目前只監視 RevoScaleR 套件函式的統計資料。
  按一下 [View SQL Script (檢視 SQL 指令碼)]  取得此報表的 T-SQL 程式碼。 

+ **R Services - 擴充的事件**

  使用本報表檢視可用於監視 R 指令碼執行的擴充事件清單。 
  按一下 [View SQL Script (檢視 SQL 指令碼)]  取得此報表的 T-SQL 程式碼。

+ **R Services - 套件**

  使用本報表檢視 SQL Server 執行個體上所安裝的 R 套件清單。 報表目前包含這些套件屬性︰ 
  + 套件 (名稱)
  + Version 
  + 相依
  + 授權
  + 建置
  + LIB 路徑

+ **R Services - 資源使用狀況**

  使用本報表檢視 SQL Server R 指令碼執行所使用的 CPU、記憶體和 I/O 資源。 您也可以檢視外部資源集區的記憶體設定。 


## <a name="see-also"></a>另請參閱

[監視 R Services](../../advanced-analytics/r-services/monitoring-r-services.md)

[R Services 的擴充事件](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)


