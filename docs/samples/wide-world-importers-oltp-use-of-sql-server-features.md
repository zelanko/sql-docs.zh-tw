---
title: 使用 SQL Server 特性和功能 |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 01/21/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 69f0027041b4acf45a54d8d8d655bc8772417dc6
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811539"
---
# <a name="use-of-sql-server-features-and-capabilities"></a>使用 SQL Server 特性和功能

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

WideWorldImporters OLTP 資料庫中 SQL Server 特性和功能的使用。

WideWorldImporters 的設計目的是要展示 SQL Server 的許多主要功能, 包括 SQL Server 2016 中引進的最新功能。 下表列出 SQL Server 的特性和功能。 每個資料列也會提供如何在 WideWorldImporters 中使用這些功能的說明。  
&nbsp;

|SQL Server 功能或功能|在 WideWorldImporters 中使用|
|:-------------------------------|:------------------------|
|時態表|有許多時態表, 包括所有的查閱樣式參考資料表和主要實體, 例如 StockItems、客戶和供應商。 使用時態表可讓您方便地追蹤這些實體的歷程記錄。|
|JSON 的 AJAX 呼叫|應用程式經常使用 AJAX 呼叫來查詢這些資料表:人員、客戶、供應商和 StockItems。 呼叫會以 JSON 格式傳回資料。 例如, 請參閱預存`Website.SearchForCustomers`程式。|
|JSON 屬性/值包|有數個數據表具有資料行, 其會保存 JSON 資料以擴充資料表中的關聯式資料。 例如, `Application.SystemParameters`具有應用程式設定的資料行, `Application.People`而且具有可記錄使用者喜好設定的資料行。 這些資料表會使用`nvarchar(max)`資料行來記錄 JSON 資料, 以及使用內建函數`ISJSON`的檢查條件約束, 以確保資料行值是有效的 json。|
|資料列層級安全性 (RLS)|資料列層級安全性 (RLS) 可用來根據角色成員資格來限制對 Customers 資料表的存取。 每個銷售領域都有角色和使用者。 若要查看 RLS 存取限制的作用, 請使用 sample-script 中對應的腳本, 這是[範例版本](https://go.microsoft.com/fwlink/?LinkID=800630)的一部分。|
|即時作業分析|(資料庫的完整版本)核心交易式資料表`Sales.InvoiceLines`和`Sales.OrderLines`都具有非叢集資料行存放區索引, 以支援在交易式資料庫中有效率地執行分析查詢, 對操作工作負載的影響最小。 在相同的資料庫中執行交易和分析也稱為混合式[交易/分析處理 (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP))。 若要查看其實際運作情況, 請使用 sample-script 中對應的腳本, 這是[範例版本](https://go.microsoft.com/fwlink/?LinkID=800630)的一部分。|
|PolyBase|若要查看此 PolyBase 的作用中, 使用外部資料表搭配裝載于 Azure blog 儲存體的公用資料集, 請使用 sample-script 中對應的腳本, 這是[範例版本](https://go.microsoft.com/fwlink/?LinkID=800630)的一部分。|
|記憶體內部 OLTP|(資料庫的完整版本)資料表類型全都是記憶體優化的, 因此資料表值參數 (Tvp) 全都受益于記憶體優化。<br/><br/>這兩個監視資料表`Warehouse.VehicleTemperatures`和`Warehouse.ColdRoomTemperatures`都是記憶體優化的。 記憶體優化可讓 ColdRoomTemperatures 資料表以比傳統磁片資料表更快的速度填入。 VehicleTemperatures 資料表會保存 JSON 承載, 並對 IoT 案例的延伸模組有其本身。 VehicleTemperatures 資料表會進一步適用于涉及 EventHubs、串流分析和 Power BI 的案例。<br/><br/>預存`Website.RecordColdRoomTemperatures`程式是以原生方式編譯, 以進一步改善記錄冷室溫度的效能。<br/><br/>若要查看作用中的記憶體內部 OLTP 範例, 請參閱 workload-drivers 中的車輛位置工作負載驅動程式, 這是[範例版本](https://go.microsoft.com/fwlink/?LinkID=800630)的一部分。|
|叢集資料行存放區索引|(資料庫的完整版本)資料表`Warehouse.StockItemTransactions`使用叢集資料行存放區索引。 此資料表中的資料列數目預期會變大, 而叢集資料行存放區索引會大幅減少資料表的磁片大小, 並改善查詢效能。 此資料表上的修改為僅限插入-在線上工作負載中, 此資料表上沒有更新/刪除, 而叢集資料行存放區索引的執行效果很適合用於插入工作負載。|
|動態資料遮罩|在資料庫架構中, 資料遮罩已套用至資料表`Purchasing.Suppliers`中針對供應商所保留的銀行明細。 非系統管理員的員工將無法存取此資訊。|
|永遠加密|Always Encrypted 的示範包含在可下載的範例 .zip 中, 這是[範例版本](https://go.microsoft.com/fwlink/?LinkID=800630)的一部分。 此示範會建立加密金鑰、對敏感性資料使用加密的資料表, 以及將資料插入資料表中的小型範例應用程式。|
|Stretch Database|`Warehouse.ColdRoomTemperatures`資料表已實作為時態表, 而且在完整版本的範例資料庫中已進行記憶體優化。 封存資料表是以磁片為基礎, 而且可以延伸至 Azure。|
|全文檢索索引|全文檢索索引可改善人員、客戶和 StockItems 的搜尋。 只有當您已在 SQL Server 實例上安裝全文檢索索引時, 才會將索引套用至查詢。 非持續性計算資料行是用來建立 StockItems 資料表中的全文檢索索引。<br/><br/>`CONCAT`用來串連欄位, 以建立已全文檢索索引的 SearchData。<br/>若要在範例中啟用全文檢索索引的使用, 請在資料庫中執行下列語句:<br/><br/>`EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>程式會建立預設全文檢索目錄 (如果尚未存在), 然後以這些視圖的全文檢索版本來取代搜尋視圖)。<br/><br/>請注意, 在 SQL Server 中使用全文檢索索引時, 必須在安裝期間選取全文檢索選項。 Azure SQL Database 不需要和特定設定即可啟用全文檢索索引。|
|已編制索引的保存計算資料行|SupplierTransactions 和 CustomerTransactions 中使用的索引保存計算資料行。|
|檢查條件約束|在中`Sales.SpecialDeals`, 相對複雜的檢查條件約束。 這可確保只會設定其中一個 DiscountAmount、DiscountPercentage 和單價。|
|UNIQUE 條件約束|已針對設定多對多的結構 (和唯一的`Warehouse.StockItemStockGroups`條件約束)。|
|資料表資料分割|(資料庫的完整版本)資料表`Sales.CustomerTransactions`和`Purchasing.SupplierTransactions`都會使用資料分割函數`PF_TransactionDate`和資料分割配置`PS_TransactionDate`, 依年份進行分割。 資料分割是用來改善大型資料表的管理能力。|
|列出處理|提供範例資料表類型`Website.OrderIDList` 。 範例程式會使用它`Website.InvoiceCustomerOrders`。 此程式使用通用資料表運算式 (Cte)、TRY/CATCH、JSON_MODIFY、XACT_ABORT、NOCOUNT、THROW 和 XACT_STATE, 示範處理訂單清單而不只是單一訂單的能力, 以將應用程式的來回行程降至最低資料庫引擎。|
|GZip 壓縮|在此`Warehouse.VehicleTemperature`視圖中, 其資料表會保存完整的感應器資料。 但當此資料超過幾個月時, 就會進行壓縮以節省空間。 壓縮函式會使用 GZip 壓縮。<br/><br/>當您`Website.VehicleTemperatures`抓取先前壓縮的資料時, 此視圖會使用解壓縮函數。|
|查詢存放區|已在資料庫上啟用查詢存放區。 執行幾個查詢之後, 請執行下列步驟:<br/><br/>1.在 Management Studio 中開啟資料庫。<br/>2.開啟 [節點查詢存放區], 這是在資料庫下。<br/>3.開啟 [報表] [*熱門資源取用查詢*]。 請參閱查詢執行, 並查看您剛才執行之查詢的計畫。|
|STRING_SPLIT|`DeliveryInstructions` 資料表`Sales.Invoices`中的資料行具有以逗號分隔的值, 可用於示範 STRING_SPLIT。|
|稽核|您可以在資料庫中執行下列語句, 以啟用此範例資料庫的 SQL Server Audit:<br/><br/>`EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>在 Azure SQL Database 中, 會透過[Azure 入口網站](https://portal.azure.com/)啟用審核。<br/><br/>有關登入、角色和許可權的安全性作業, 會記錄在已啟用 audit 的所有系統上 (包括 standard edition 系統)。 Audit 會導向至應用程式記錄檔, 因為這在所有系統上都有提供, 而且不需要其他許可權。 警告是為了提高安全性, 應將其重新導向至安全性記錄檔或安全資料夾中的檔案。 提供連結以描述所需的額外設定。<br/><br/>針對評估/developer/enterprise edition 系統, 會審核所有財務交易資料的存取權。|
| &nbsp; | &nbsp; |
