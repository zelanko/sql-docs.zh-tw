---
title: SQL Server 隱私權補充 | Microsoft Docs
ms.date: 4/25/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 63425a2a280154522c0219a89033e67c4e8bdeda
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51703257"
---
# <a name="sql-server-privacy-supplement"></a>SQL Server 隱私權補充
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文摘要說明 SQL Server 內使用之不同資料物件的行為，以及如何使用物件來傳遞個人或機密方式的資訊。 本文是整體 [Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=521839)的增補合約。 本文中的資料分類只適用於 SQL Server 內部部署產品的版本。 它不適用於下列項目：

- Azure SQL Database
- SQL Server Management Studio (SSMS)
- SQL Server Data Tools (SSDT)
- Azure Data Studio
- Data Migration Assistant
- SQL Server 移轉小幫手
- MS-SQL 延伸模組

「允許的使用方式情節」的定義。 在本文內容中，Microsoft 定義「允許的使用方式情節」作為 Microsoft 所啟始的動作或活動。

## <a name="access-control"></a>存取控制

用來保護 SQL Server 安裝內登入、使用者或帳戶的認證相關資訊。

### <a name="examples-of-access-control"></a>存取控制範例

- 密碼
- 憑證

### <a name="permitted-usage-scenarios"></a>允許的使用方式情節

|狀況  |存取限制  |保留需求 |
|---------|---------|---------|
|透過「使用意見反應」，這些認證絕不能離開使用者電腦。     |-         |-         |
|「損毀傾印」可能包含「存取控制資料」。     |-         |損毀傾印：最多 30 天。         |
|透過「使用者意見反應」，這些認證絕不能離開使用者電腦，除非客戶手動予以插入    |限制為供 Microsoft 內部使用且協力廠商不可存取。         |使用者意見反應：最多 1 年         |
 |
## <a name="customer-content"></a>客戶內容

客戶內容直接或間接定義為使用者資料表內儲存的資料。 資料包括可能儲存在使用者資料表內之查詢文字內的統計資料或使用者常值。

### <a name="examples-of-customer-content"></a>客戶內容範例

- 任何使用者資料表的資料列內所儲存的資料值。
- 包含任何使用者資料表資料列內值複本的統計資料物件。
- 包含常值的查詢文字。

### <a name="permitted-usage-scenarios"></a>允許的使用方式情節
|狀況  |存取限制  |保留需求 |
|---------|---------|---------|
|透過「使用意見反應」，這項資料不會離開使用者電腦。 |- |- |
|「損毀傾印」可能包含「客戶內容」，並發出給 Microsoft。 |- |損毀傾印：最多 30 天。 |
|客戶與其同意可以傳送包含給 Microsoft 之「客戶內容」的「使用者意見反應」。 |限制為供 Microsoft 內部使用且協力廠商不可存取。 Microsoft 可以向原始客戶公開資料。 |使用者意見反應：最多 1 年 |

## <a name="end-user-identifiable-information-euii"></a>終端使用者識別資訊 (EUII)

接收自使用者的資料，或從其產品使用而產生的資料。
- 可連結至個別使用者。
- 不包含內容。

### <a name="examples-of-end-user-identifiable-information"></a>終端使用者識別資訊範例

- 介面識別。 完整 IP 位址
- 電腦名稱
- 登入/使用者名稱
- 電子郵件地址的本機部分 (joe@contoso.com)
- 位置資訊
- 客戶識別

### <a name="permitted-usage-scenarios"></a>允許的使用方式情節

|狀況  |存取限制  |保留需求|
|---------|---------|---------|
|透過「使用意見反應」，這項資料不會離開使用者電腦。 |- |- |
|損毀傾印可能包含 EUII，並發出給 Microsoft。 |- |損毀傾印：最多 30 天 |
|客戶識別識別碼可能會發出給 Microsoft，以提供使用者已訂閱的新混合式和雲端功能。 |- |目前沒有這類混合式或雲端功能。|
|客戶與其同意可以傳送包含給 Microsoft 之客戶內容的使用者意見反應。|限制為供 Microsoft 內部使用且協力廠商不可存取。 Microsoft 可以向原始客戶公開資料。 |使用者意見反應：最多 1 年 |

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
|客戶與其同意可以傳送包含給 Microsoft 之「客戶內容」的「使用者意見反應」。 |限制為供 Microsoft 內部使用且協力廠商不可存取。 |客戶與其同意可以傳送包含給 Microsoft 之「客戶內容」的「使用者意見反應」。 |
|Power View 和 SQL Reporting Services 地圖項目可能會傳送資料，以使用 Bing 地圖服務。 |限制為工作階段資料 |- |

## <a name="system-metadata"></a>系統中繼資料

在執行伺服器的過程中產生的資料。  資料未包含客戶內容。

### <a name="examples-of-system-metadata"></a>系統中繼資料範例

未包括客戶內容、客戶存取控制或 EUII 時，會將下列各項視為系統中繼資料：

- 資料庫 GUID
- 電腦名稱雜湊
- 執行個體名稱雜湊
- 應用程式名稱
- 行為/使用方式資料
- SQL 客戶體驗改善計畫資料 (SQLCEIP)
- 伺服器設定資料，例如 sp_configure 設定
- 功能設定資料
- 事件名稱和錯誤碼
- 硬體設定和識別，例如 OEM 製造商

Microsoft 會檢查其他程式使用 SQL Server 所設定的應用程式名稱值 (例如：Sharepoint 或協力廠商封裝程式，且會在使用方式資料啟用時在傳送給 Microsoft 的系統中繼資料中包含此資訊)。 客戶不應該放置個人資料 (例如，[系統中繼資料] 欄位中的終端使用者識別資訊)，或建立設計在這些欄位中儲存個人資料的應用程式。 

### <a name="permitted-usage-scenarios"></a>允許的使用方式情節

|狀況  |存取限制  |保留需求|
|---------|---------|---------|
|Microsoft 可以用來改善功能及 (或) 修正目前功能中的 Bug。|限制為供 Microsoft 內部使用且協力廠商不可存取。 |最少 90 天 - 最多 3 年 |
|可以用來對客戶提出建議。  例如，「根據您對產品的使用方式，請考慮使用執行效果更佳的功能 *X*。」 |Microsoft 可以向原始客戶公開資料，例如透過儀表板。 |客戶資料安全性記錄：最少 3 年 - 最多 6 年 |
Microsoft 可以用來進行未來的產品規劃。 |Microsoft 可能會與其他硬體和軟體廠商共用這項資訊，以改善其產品如何與 Microsoft 軟體搭配執行。 |最少 90 天 - 最多 3 年|
|Microsoft 可以用來根據發出的「使用意見反應」來提供雲端服務。 例如，客戶儀表板顯示跨組織之所有 SQL Server 安裝的功能使用方式。 |Microsoft 可以向原始客戶公開資料，例如透過儀表板。 |最少 90 天 - 最多 3 年 |
|客戶與其同意可以傳送包含給 Microsoft 之「客戶內容」的「使用者意見反應」。 |限制為供 Microsoft 內部使用且協力廠商不可存取。 Microsoft 可以向原始客戶公開資料。 |使用者意見反應：最多 1 年 |
|可以使用資料庫名稱和應用程式名稱將資料庫與應用程式分類為已知類別，例如執行由 Microsoft 或其他公司提供之軟體的資料庫與應用程式。|限制為供 Microsoft 內部使用且協力廠商不可存取。|最少 90 天 - 最多 3 年 |

## <a name="object-metadata"></a>物件中繼資料

描述或用來設定伺服器、資料庫、資料表和其他資源的資料。  物件中繼資料包括資料庫資料表和資料行名稱，但不是資料庫資料列內容或其他客戶內容。 客戶不應該放置個人資料 (例如，[物件中繼資料] 欄位中的終端使用者識別資訊)，或建立設計在這些欄位中儲存個人資料的應用程式。 針對下方的已允許使用方式情節，只有雜湊表單會用來判斷使用方式模式以改善產品。 

### <a name="examples-of-object-metadata"></a>物件中繼資料範例

- SQL Server 資料庫名稱
- 資料表名稱和資料行名稱
- 統計資料名稱

### <a name="permitted-usage-scenarios"></a>允許的使用方式情節

|狀況  |存取限制  |保留需求|
|---------|---------|---------|
|Microsoft 可以用來改善功能及 (或) 修正目前功能中的 Bug。 |限制為供 Microsoft 內部使用且協力廠商不可存取。 |最少 90 天 - 最多 3 年|

## <a name="telemetry-controls"></a>遙測控制項

您可於參考此處的指示，來了解如何開啟/關閉產品中的遙測 - https://support.microsoft.com/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
