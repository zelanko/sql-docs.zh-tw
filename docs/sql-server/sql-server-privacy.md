---
description: SQL Server 隱私權補充
title: SQL Server 隱私權補充 | Microsoft Docs
ms.date: 09/30/2020
ms.prod: sql
ms.technology: release-landing
ms.reviewer: mikeray
ms.custom: ''
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords: ''
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: f8356b5c07e6d85d9359276740fdd30adc200493
ms.sourcegitcommit: ef20f39a17fd4395dd2dd37b8dd91b57328a751c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/28/2020
ms.locfileid: "92793805"
---
# <a name="sql-server-privacy-supplement"></a>SQL Server 隱私權補充

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

本文摘要說明使用已連線到網際網路的功能，可收集匿名的功能使用方式和診斷資料並傳送給 Microsoft。 SQL Server 可能會收集標準電腦資訊以及關於使用方式和效能的資料，這些資訊可能會傳送給 Microsoft，並基於改善產品品質、安全性和可靠性的目的加以分析。

本文是整體 [Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=521839)的增補合約。 本文中的資料分類只適用於 SQL Server 內部部署產品的版本。 它不適用於下列項目：

- Azure SQL Database
- [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-telemetry-ssms.md)
- SQL Server Data Tools (SSDT)
- Azure Data Studio
- 資料庫移轉小幫手
- SQL Server 移轉小幫手
- MS-SQL 延伸模組

「允許的使用方式情節」的定義。 在本文內容中，Microsoft 定義「允許的使用方式情節」作為 Microsoft 所啟始動作或活動。

## <a name="access-control"></a>存取控制

用來保護 SQL Server 安裝內登入、使用者或帳戶的認證相關資訊。

### <a name="examples-of-access-control"></a>存取控制範例

- 密碼
- 憑證

### <a name="permitted-usage-scenarios"></a>允許的使用方式情節

|狀況 |存取限制 |保留需求 |
|---------|---------|---------|
|這些認證永遠不會透過使用方式和診斷資料流出使用者電腦。 |- |- |
|「損毀傾印」可能包含「存取控制資料」。 |- |損毀傾印：最多 30 天。 |
|透過「使用者意見反應」，這些認證絕不能離開使用者電腦，除非客戶手動予以插入 |限制為供 Microsoft 內部使用且協力廠商不可存取。 |使用者意見反應：最多 1 年|
|&nbsp;|&nbsp;|&nbsp;|

## <a name="customer-data"></a>客戶資料

客戶資料會直接或間接定義為儲存在使用者資料表內的資料。 資料包括可能儲存在使用者資料表內之查詢文字內的統計資料或使用者常值。

### <a name="examples-of-customer-data"></a>客戶資料範例

- 任何使用者資料表的資料列內所儲存的資料值。
- 包含任何使用者資料表資料列內值複本的統計資料物件。
- 包含常值的查詢文字。

### <a name="permitted-usage-scenarios"></a>允許的使用方式情節

|狀況  |存取限制  |保留需求 |
|---------|---------|---------|
|此資料不會透過使用方式和診斷資料流出使用者電腦。 |- |- |
|損毀傾印可能包含客戶資料，並發出給 Microsoft。 |- |損毀傾印：最多 30 天。 |
|客戶同意後，即可將包含客戶資料的使用者意見反應傳送給 Microsoft。 |限制為供 Microsoft 內部使用且協力廠商不可存取。 Microsoft 可以向原始客戶公開資料。 |使用者意見反應：最多 1 年 |

## <a name="personal-data"></a>個人資料

接收自使用者的資料，或從其產品使用而產生的資料。
- 可連結至個別使用者。
- 不包含客戶資料。

### <a name="examples-of-personal-data"></a>個人資料範例

- 介面識別。 完整 IP 位址
- 電腦名稱
- 登入/使用者名稱
- 電子郵件地址的本機部分 (joe@contoso.com)
- 位置資訊
- 客戶識別

### <a name="permitted-usage-scenarios"></a>允許的使用方式情節

|狀況  |存取限制  |保留需求|
|---------|---------|---------|
|此資料不會透過使用方式和診斷資料流出使用者電腦。 |- |- |
|損毀傾印可能包含個人資料，並發出給 Microsoft。 |- |損毀傾印：最多 30 天 |
|客戶識別識別碼可能會發出給 Microsoft，以提供使用者已訂閱的新混合式和雲端功能。 |- |目前沒有這類混合式或雲端功能。|
|客戶同意後，即可將包含客戶資料的使用者意見反應傳送給 Microsoft。|限制為供 Microsoft 內部使用且協力廠商不可存取。 Microsoft 可以向原始客戶公開資料。 |使用者意見反應：最多 1 年 |

## <a name="internet-based-services-data"></a>網際網路服務資料

根據 SQL Server EULA，提供網際網路服務所需的資料。

### <a name="examples-of-internet-based-services-data"></a>網際網路服務資料範例

- 電腦規格資訊
- 瀏覽器名稱/版本
- SQL Server 版本
- 語言代碼
- 已移除特定八位元的 IP 位址
- 地圖資料

### <a name="permitted-usage-scenarios"></a>允許的使用方式情節

|狀況  |存取限制  |保留需求|
|---------|---------|---------| 
|Microsoft 可以用來改善功能及 (或) 修正目前功能中的 Bug。 |限制為供 Microsoft 內部使用且協力廠商不可存取。 Microsoft 可以向原始客戶公開資料。  例如，儀表板 |最少 90 天 - 最多 3 年 |
|客戶同意後，即可將包含客戶資料的使用者意見反應傳送給 Microsoft。 |限制為供 Microsoft 內部使用且協力廠商不可存取。 |客戶同意後，即可將包含客戶資料的使用者意見反應傳送給 Microsoft。 |
|Power View 和 SQL Reporting Services 地圖項目可能會傳送資料，以使用 Bing 地圖服務。 |限制為工作階段資料 |- |

## <a name="non-personal-data"></a>非個人資料

1. 接收自組織的資料，或從其產品使用而產生的資料。 其可連結到組織，但不包含客戶資料。

   - 範例
     - 組織名稱 (例如：Microsoft Corp.)

   - 允許的使用方式情節

     |狀況  |存取限制  |保留需求|
     |---------|---------|---------|
     | Microsoft 可能會收集在 Azure 虛擬機器中所執行 SQL Server 執行個體的一般使用方式資料，用來明確地向客戶提供在 Azure 虛擬機器內使用 SQL Server 時，Azure 內部的額外利益。 | Microsoft 可以向客戶公開資料 (例如透過 Azure 入口網站) 來協助在 Azure 虛擬機器中執行 SQL Server 之客戶存取在 Azure 中執行 SQL Server 才能獲得的利益。 </br></br>Microsoft 在沒有客戶的事先同意之前，不會將此資料用於授權稽核。 | 最少 90 天 - 最多 3 年 |

2. 描述或用來設定客戶建立或提供之伺服器、資料庫、資料表和其他資源的資料。 其包括資料庫資料表和資料行名稱，但不包含資料庫資料列內容或其他客戶資料。 客戶不該在這些欄位中放置任何個人資料，或者建立用途為在這些欄位中儲存個人資料的應用程式。 在以下的允許使用方式案例中，只會使用雜湊表單來判斷使用模式，從而改善產品。

   - 範例
      - SQL Server 資料庫名稱
      - 資料表名稱和資料行名稱
      - 統計資料名稱

    - 允許的使用方式情節

      > [!NOTE]
      > 所有中繼資料值都會在收集前進行雜湊處理。
      >

      |狀況  |存取限制  |保留需求|
      |---------|---------|---------|
      |Microsoft 可以用來改善功能及 (或) 修正目前功能中的 Bug。 |限制為供 Microsoft 內部使用且協力廠商不可存取。 |最少 90 天 - 最多 3 年|

3. 伺服器執行過程中所產生的資料。 其不包含客戶資料、1. 或 2. 中所列的 非個人資料 (如上)、 客戶存取控制資料或個人資料。

   - 範例
     - 資料庫 GUID
     - 電腦名稱雜湊
     - 執行個體名稱雜湊
     - 應用程式名稱
     - 行為/使用方式資料
     - SQL 客戶經驗改進計畫資料 (SQLCEIP)
     - 伺服器設定資料，例如 sp_configure 設定
     - 功能設定資料
     - 事件名稱和錯誤碼
     - 硬體設定和識別，例如 OEM 製造商

   Microsoft 不會檢查由其他使用 SQL Server 之程式所設定的應用程式名稱值 (範例：SharePoint 或協力廠商已封裝程式，並在啟用 [使用狀況資料] 的情況下，將此資訊包含在中繼資料欄位中傳送給 Microsoft)。 客戶不該在這些中繼資料欄位中放置任何個人資料，或者建立用途為在這些欄位中儲存個人資料的應用程式。

   - 允許的使用方式情節

     |狀況  |存取限制  |保留需求|
     |---------|---------|---------|
     |Microsoft 可以用來改善功能及 (或) 修正目前功能中的 Bug。|限制為供 Microsoft 內部使用且協力廠商不可存取。 |最少 90 天 - 最多 3 年 |
     |可以用來對客戶提出建議。  例如，「根據所使用產品方式，請考慮使用執行效果更佳的功能 *X* 。」 |Microsoft 可以向原始客戶公開資料，例如透過儀表板。 |客戶資料安全性記錄：最少 3 年 - 最多 6 年 |
     |Microsoft 可以用來進行未來的產品規劃。 |Microsoft 可能會與其他硬體和軟體廠商共用這項資訊，以改善其產品如何與 Microsoft 軟體搭配執行。 |最少 90 天 - 最多 3 年|
     |Microsoft 可以用來根據發出的使用方式和診斷資料來提供雲端服務。 例如，客戶儀表板顯示跨組織之所有 SQL Server 安裝的功能使用方式。 |Microsoft 可以向原始客戶公開資料，例如透過儀表板。 |最少 90 天 - 最多 3 年 |
     |客戶同意後，即可將包含客戶資料的使用者意見反應傳送給 Microsoft。 |限制為供 Microsoft 內部使用且協力廠商不可存取。 Microsoft 可以向原始客戶公開資料。 |使用者意見反應：最多 1 年 |
     |可以使用資料庫名稱和應用程式名稱將資料庫與應用程式分類為已知類別，例如執行由 Microsoft 或其他公司提供之軟體的資料庫與應用程式。|限制為供 Microsoft 內部使用且協力廠商不可存取。|最少 90 天 - 最多 3 年 |

## <a name="system-generated-logs-controls"></a>系統產生的記錄檔控制項

如需如何在產品中開啟/關閉系統產生記錄檔的指示，請參閱這裡 - [設定 SQL Server 的使用狀況和診斷資料收集 (CEIP)](usage-and-diagnostic-data-configuration-for-sql-server.md)。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
