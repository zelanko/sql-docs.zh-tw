---
title: "時態表使用案例 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b8fa2dd-1790-4289-8362-f11e6d63bb09
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 332787256518605b6f91dab6be012889c0b0aa93
ms.openlocfilehash: 007b40b36317a67c6b9714b89aac0d3324312f30
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="temporal-table-usage-scenarios"></a>時態表使用案例
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  時態表在需要追蹤資料變更歷程記錄的案例中通常很有用。    
建議您在下列使用案例中考慮使用時態表，以獲得卓越的生產力優勢。  
  
## <a name="data-audit"></a>資料稽核  
 在您儲存重要資訊，並隨時需要追蹤變更內容和變更時間，以及執行資料鑑識調查的資料表上使用暫時性系統版本設定。    
已 Temporal 系統版本設定的資料表可讓您在開發週期的早期階段針對資料稽核案例進行計畫，或視需要將資料稽核新增到現有應用程式或解決方案。  
  
 下圖顯示「員工」資料表案例，其中的資料樣本包括目前 (以藍色標示) 和歷程記錄的資料列版本 (以灰色標示)。   
圖表的右邊以視覺化的方式在時間軸上呈現資料列版本，以及透過時態表上不同的查詢類型 (不管包含或不包含 SYSTEM_TIME 子句) 來顯示您所選取的資料列。  
  
 ![TemporalUsageScenario1](../../relational-databases/tables/media/temporalusagescenario1.png "TemporalUsageScenario1")  
  
### <a name="enabling-system-versioning-on-a-new-table-for-data-audit"></a>在新的資料表上針對資料稽核啟用系統版本設定  
 如果您已識別出需要進行資料稽核的資訊，請將資料庫資料表建立為已 Temporal 系統版本設定。 下列簡易範例說明在假設性的 HR 資料庫中「員工」資訊的案例：  
  
```  
CREATE TABLE Employee   
(    
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED   
  , [Name] nvarchar(100) NOT NULL  
  , [Position] varchar(100) NOT NULL   
  , [Department] varchar(100) NOT NULL  
  , [Address] nvarchar(1024) NOT NULL  
  , [AnnualSalary] decimal (10,2) NOT NULL  
  , [ValidFrom] datetime2 (2) GENERATED ALWAYS AS ROW START  
  , [ValidTo] datetime2 (2) GENERATED ALWAYS AS ROW END  
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)  
 )    
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));  
```  
  
 如需建立系統設定版本之時態表的各種選項，請參閱 [建立系統設定版本的時態表](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)中的說明。  
  
### <a name="enabling-system-versioning-on-an-existing-table-for-data-audit"></a>在現有的資料表上針對資料稽核啟用系統版本設定  
 如果您需要在現有資料庫中執行資料稽核，請使用 ALTER TABLE 來延伸非時態表以使它成為已系統版本設定。 為了避免中斷您應用程式中的變更，請將期間資料行新增為 HIDDEN，如 [Alter Non-Temporal Table to be System-Versioned Temporal Table](https://msdn.microsoft.com/library/mt590957.aspx#Anchor_3)(將非時態表變更為系統設定版本的時態表) 中所述。 下列範例說明在假設性的 HR 資料庫中於現有「員工」資料表上啟用系統版本設定：  
  
```  
/*   
Turn ON system versioning in Employee table in two steps   
(1) add new period columns (HIDDEN)   
(2) create default history table   
*/   
ALTER TABLE Employee   
ADD   
    ValidFrom datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , ValidTo datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);   
  
ALTER TABLE Employee    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Employee_History));  
```  
  
 在執行上述指令碼之後，所有資料變更將會在記錄資料表中明確地進行收集。    
在一般的資料稽核案例中，您會對在感興趣時間週期內套用到個別資料列的所有資料變更進行查詢。 預設的記錄資料表是以叢集資料列存放區 B 型樹狀結構建立，以有效地處理這個使用案例。  
  
### <a name="performing-data-analysis"></a>執行資料分析  
 使用上述的任何一個方式啟用系統版本設定之後，您只需再執行一次查詢，便能開始資料稽核。 下列查詢會搜尋「員工」記錄的資料列版本，搜尋條件為 EmployeeID = 1000，且在 2014 年 1 月 1 日和 2015 年 1 月 1 日之間 (包括上限) 至少有在一段時間為作用中。  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME    
        BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'   
            WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 將 [FOR SYSTEM_TIME BETWEEN...AND] 以 [FOR SYSTEM_TIME ALL] 取代，以分析該特定員工的整體資料變更歷程記錄。  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME ALL WHERE    
        EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 若要搜尋僅在特定期間內 (且沒有在該期間之外) 作用的資料列版本，請使用 CONTAINED IN。 這個查詢非常有效率，因為它只會查詢記錄資料表：  
  
```  
SELECT * FROM Employee FOR SYSTEM_TIME    
    CONTAINED IN ('2014-01-01 00:00:00.0000000', '2015-01-01 00:00:00.0000000')   
        WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 最後，針對某些稽核案例，您可能會想要查看整體資料表在過去任何一個時間點的模樣。  
  
```  
SELECT * FROM Employee FOR SYSTEM_TIME AS OF '2014-01-01 00:00:00.0000000' ;  
```  
  
 已系統版本設定的時態表會以 UTC 時區來存放期間資料行的值，不過在進行篩選資料和顯示結果的工作時，使用本地時區總是會比較方便。 下列程式碼範例示範如何套用原本在本地時區中指定，並使用 SQL Server 2016 所導入之 AT TIME ZONE 轉換成 UTC 的篩選條件。  
  
```  
/*Add offset of the local time zone to current time*/  
DECLARE @asOf DATETIMEOFFSET = GETDATE() AT TIME ZONE 'Pacific Standard Time'  
/*Convert AS OF filter to UTC*/  
SET @asOf = DATEADD (MONTH, -9, @asOf) AT TIME ZONE 'UTC';  
  
SELECT   
    EmployeeID  
    , Name  
    , Position  
    , Department  
    , [Address]  
    , [AnnualSalary]  
    , ValidFrom AT TIME ZONE 'Pacific Standard Time' AS ValidFromPT   
    , ValidTo AT TIME ZONE 'Pacific Standard Time' AS ValidToPT  
FROM Employee   
    FOR SYSTEM_TIME AS OF @asOf where EmployeeId = 1000  
  
```  
  
 對於所有其他使用已系統版本設定資料表的案例，使用 AT TIME ZONE 會很有幫助。  
  
> [!TIP]  
>  以 FOR SYSTEM_TIME 在 Temporal 子句中指定的篩選條件可進行 SARG (也就是說， SQL Server 可以利用基礎叢集索引來執行搜尋作業，而非掃描作業)。   
> 如果您直接查詢記錄資料表，請以 \<期間資料行>  {< | > | =, …} date_condition AT TIME ZONE ‘UTC’ 的格式指定篩選，來確保您的篩選條件也是可進行 SARG 的。  
> 如果您將 AT TIME ZONE 套用到期間資料行，SQL Server 將會執行資料表/索引掃描，這可能會耗費相當多的資源。 請在查詢中避免這類條件：  
> \<期間資料行>  AT TIME ZONE ‘\<您的時區>’  >  {< | > | =, …} date_condition。  
  
 另請參閱： [查詢系統設定版本時態表中的資料](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)。  
  
## <a name="point-in-time-analysis-time-travel"></a>時間點分析 (時間移動)  
 資料稽核的焦點通常是在個別記錄所發生的變更上，而對於時間移動案例來說，使用者想要看的是整體資料集經過一段時間的變更方式。 時間移動有時候會包含數個您想要分析的相關時態表，每個時態表皆會以獨立的方式進行變更：  
  
-   歷程記錄和目前資料中之重要指標的趨勢  
  
-   「位於」過去任何時間點 (昨天、一個月前等) 之整體資料的確切快照集  
  
-   感興趣的兩個時間點之間的差異 (例如一個月前 vs. 三個月前)  
  
 有許多實際的案例都會需要進行時間移動分析。 為了說明此使用案例，我們將參考具有自動產生歷程記錄的 OLTP。  
  
### <a name="oltp-with-auto-generated-data-history"></a>具有自動產生資料歷程記錄的 OLTP  
 在交易處理系統中，對重要衡量標準在經過一段時間之後的變更方式進行分析，是一件很常見的事。 在理想情況下，分析歷程記錄並不應該影響 OLTP 應用程式的效能，因為該應用程式必須在最低延遲和最少資料鎖定的情況下存取資料的最新狀態。  已系統版本設定的時態表已設計成允許使用者明確地保存完整的變更歷程記錄，來和目前的資料分開並於稍後進行分析，以將對主要 OLTP 工作負載所造成的影響降到最低。  
針對大量交易處理的工作負載，我們建議您使用 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)，這能允許您以符合成本效益的方式將目前的資料儲存在記憶體中，並將完整的變更記錄儲存在磁碟上。  
  
 針對記錄資料表，我們建議您使用叢集資料行存放區索引，原因如下：  
  
-   典型的趨勢分析受惠於叢集資料行存放區索引所提供的查詢效能。  
  
-   搭配記憶體最佳化資料表的資料清除工作，在記錄資料表擁有叢集資料行存放區索引時，於 OLTP 工作負載較重之下的表現最佳。  
  
-   叢集資料行存放區索引能提供絕佳的壓縮，特別是在並非所有資料行皆同時受到變更的情況下。  
  
 搭配記憶體內部 OLTP 使用時態表，能減少將整個資料集保持在記憶體內部的需求，並能讓您輕鬆地分辨熱門和冷門資料。  
幾個符合此類別的實際案例範例，為庫存管理或貨幣交易。  
  
 下圖顯示用於庫存管理的簡化資料模型：  
  
 ![TemporalUsageInMemory](../../relational-databases/tables/media/temporalusageinmemory.png "TemporalUsageInMemory")  
  
 下列程式碼範例將 ProductInventory 建立為記憶體內已系統版本設定時態表，並在記錄資料表上具有叢集資料行存放區索引 (根據預設，這會取代資料列存放區索引)：  
  
> [!NOTE]  
>  請確定您的資料庫允許建立記憶體最佳化資料表。 請參閱 [建立記憶體最佳化資料表和原生編譯的預存程序](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)。  
  
```  
USE TemporalProductInventory  
GO  
  
BEGIN  
    --If table is system-versioned, SYSTEM_VERSIONING must be set to OFF first   
    IF ((SELECT temporal_type FROM SYS.TABLES WHERE object_id = OBJECT_ID('dbo.ProductInventory', 'U')) = 2)  
    BEGIN  
        ALTER TABLE [dbo].[ProductInventory] SET (SYSTEM_VERSIONING = OFF)  
    END  
    DROP TABLE IF EXISTS [dbo].[ProductInventory]  
       DROP TABLE IF EXISTS [dbo].[ProductInventoryHistory]  
END  
GO  
  
CREATE TABLE [dbo].[ProductInventory]  
(  
    ProductId int NOT NULL,  
    LocationID INT NOT NULL,  
    Quantity int NOT NULL CHECK (Quantity >=0),  
  
    SysStartTime datetime2(0) GENERATED ALWAYS AS ROW START  NOT NULL ,  
    SysEndTime datetime2(0) GENERATED ALWAYS AS ROW END  NOT NULL ,  
    PERIOD FOR SYSTEM_TIME(SysStartTime,SysEndTime),  
  
    --Primary key definition  
    CONSTRAINT PK_ProductInventory PRIMARY KEY NONCLUSTERED (ProductId, LocationId)  
)  
WITH  
(  
    MEMORY_OPTIMIZED=ON,      
    SYSTEM_VERSIONING = ON   
    (          
        HISTORY_TABLE = [dbo].[ProductInventoryHistory],          
        DATA_CONSISTENCY_CHECK = ON  
    )  
)  
  
CREATE CLUSTERED COLUMNSTORE INDEX IX_ProductInventoryHistory ON [ProductInventoryHistory]  
WITH (DROP_EXISTING = ON);  
```  
  
 針對上述模型，以下是維護庫存之程序可能的模樣：  
  
```  
CREATE PROCEDURE [dbo].[spUpdateInventory]  
@productId int,  
@locationId int,  
@quantityIncrement int  
  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')  
    UPDATE dbo.ProductInventory  
        SET Quantity = Quantity + @quantityIncrement   
            WHERE ProductId = @productId AND LocationId = @locationId  
  
/*If zero rows were updated than this is insert of the new product for a given location*/  
    IF @@rowcount = 0  
        BEGIN  
            IF @quantityIncrement < 0  
                SET @quantityIncrement = 0  
            INSERT INTO [dbo].[ProductInventory]  
                (  
                    [ProductId]  
                    ,[LocationID]  
                    ,[Quantity]  
                )  
                VALUES  
                   (  
                        @productId  
                       ,@locationId  
                       ,@quantityIncrement  
        END  
END;  
```  
  
 spUpdateInventory 預存程序可能會在庫存中插入新產品，或更新特定位置的產品數量。 商務邏輯非常簡單，且專注在持續維持最新狀態的準確度之上。它會透過資料表更新對 [數量] 欄位進行遞增 / 遞減，同時已系統版本設定的資料表會明確地將歷程記錄的維度新增到資料中，如下列圖表所示  
  
 ![TemporalUsageInMemory2b](../../relational-databases/tables/media/temporalusageinmemory2b.png "TemporalUsageInMemory2b")  
  
 現在，對最新狀態的查詢工作將可以從原生編譯的模組上有效地執行：  
  
```  
CREATE PROCEDURE [dbo].[spQueryInventoryLatestState]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')  
    SELECT ProductId, LocationID, Quantity, SysStartTime  
      FROM dbo.ProductInventory  
    ORDER BY ProductId, LocationId  
END;  
GO  
EXEC [dbo].[spQueryInventoryLatestState];  
```  
  
 對經過一段時間之資料變更所進行的分析，在使用 FOR SYSTEM_TIME ALL 子句的情況下會變得非常簡單，如下列範例所示：  
  
```  
DROP VIEW IF EXISTS vw_GetProductInventoryHistory;  
GO  
CREATE VIEW vw_GetProductInventoryHistory  
AS  
   SELECT ProductId, LocationId, Quantity, SysStartTime, SysEndTime   
   FROM [dbo].[ProductInventory]  
   FOR SYSTEM_TIME ALL;  
GO  
SELECT * FROM vw_GetProductInventoryHistory   
    WHERE ProductId = 2;  
```  
  
 下圖顯示單一產品的資料歷程記錄，這可以透過在 Power Query、Power BI 或類似的商務智慧工具中匯入上述檢視，來輕鬆地進行轉譯。  
  
 ![ProductHistoryOverTime](../../relational-databases/tables/media/producthistoryovertime.png "ProductHistoryOverTime")  
  
 時態表可以在此案例中用來執行其他類型的時間移動分析，例如重新建構「位於 (AS OF)」過去任何時間點的庫存狀態，或比較屬於不同時間的快照集。  
  
 針對這個使用案例，您也可以延伸「產品」和「位置」資料表來使它們成為時態表，以便稍後進行 UnitPrice 和 NumberOfEmployee 之變更歷程記錄的分析。  
  
```  
ALTER TABLE Product   
ADD   
    SysStartTime datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , SysEndTime datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);   
  
ALTER TABLE Product    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProductHistory));  
  
ALTER TABLE [Location]  
ADD   
    SysStartTime datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DFValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , SysEndTime datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DFValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);  
  
ALTER TABLE [Location]    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.LocationHistory));  
```  
  
 由於資料模組現已牽涉到多個時態表，AS OF 分析的最佳做法為建立可從相關資料表擷取必要資料的檢視，並將 FOR SYSTEM_TIME AS OF 套用到檢視上，這將能大幅簡化對整體檔案模組狀態的重新建構：  
  
```  
DROP VIEW IF EXISTS vw_ProductInventoryDetails;  
GO  
  
CREATE VIEW vw_ProductInventoryDetails  
AS  
    SELECT PrInv.ProductId ,PrInv.LocationId, P.ProductName, L.LocationName, PrInv.Quantity  
    , P.UnitPrice, L.NumberOfEmployees  
    , P.SysStartTime AS ProductStartTime, P.SysEndTime AS ProductEndTime  
    , L.SysStartTime AS LocationStartTime, L.SysEndTime AS LocationEndTime  
    , PrInv.SysStartTime AS InventoryStartTime, PrInv.SysEndTime AS InventoryEndTime  
FROM dbo.ProductInventory as PrInv  
JOIN dbo.Product AS P ON PrInv.ProductId = P.ProductID  
JOIN dbo.Location AS L ON PrInv.LocationId = L.LocationID;  
GO  
SELECT * FROM vw_ProductInventoryDetails  
    FOR SYSTEM_TIME AS OF '2015.01.01';   
```  
  
 下圖顯示針對 SELECT 查詢產生的執行計畫。 下列說明處理 Temporal 關係所包含的所有複雜度，都會由 SQL Server 引擎負責處理：  
  
 ![ASOFExecutionPlan](../../relational-databases/tables/media/asofexecutionplan.png "ASOFExecutionPlan")  
  
 使用下列程式碼來比較兩個時間點 (一天前和一個月前) 的產品庫存狀況：  
  
```  
DECLARE @dayAgo datetime2 (0) = DATEADD (day, -1, SYSUTCDATETIME());  
DECLARE @monthAgo datetime2 (0) = DATEADD (month, -1, SYSUTCDATETIME());  
  
SELECT   
    inventoryDayAgo.ProductId  
    , inventoryDayAgo.ProductName  
    , inventoryDayAgo.LocationName  
    , inventoryDayAgo.Quantity AS QuantityDayAgo,inventoryMonthAgo.Quantity AS QuantityMonthAgo  
    , inventoryDayAgo.UnitPrice AS UnitPriceDayAgo, inventoryMonthAgo.UnitPrice AS UnitPriceMonthAgo  
FROM vw_ProductInventoryDetails  
FOR SYSTEM_TIME AS OF @dayAgo AS inventoryDayAgo  
JOIN vw_ProductInventoryDetails FOR SYSTEM_TIME AS OF @monthAgo AS inventoryMonthAgo  
    ON inventoryDayAgo.ProductId = inventoryMonthAgo.ProductId AND inventoryDayAgo.LocationId = inventoryMonthAgo.LocationID;  
```  
  
## <a name="anomaly-detection"></a>異常偵測  
 異常偵測 (或極端值偵測) 為針對不符合預期模式或資料集中其他項目之項目所進行的識別。   
您可以使用已系統版本設定的時態表來偵測定期發生或不規則發生的異常，因為您可以利用 Temporal 查詢來快速找出特定模式。  
異常的定義，取決於您所收集的資料類型，以及您的商務邏輯。  
  
 下列範例顯示偵測銷售數字「峰值」的簡化邏輯。 我們假設您是使用收集已購買產品之歷程記錄的時態表：  
  
```  
CREATE TABLE [dbo].[Product]  
                (  
            [ProdID] [int] NOT NULL PRIMARY KEY CLUSTERED  
        , [ProductName] [varchar](100) NOT NULL  
        , [DailySales] INT NOT NULL  
        , [ValidFrom] [datetime2](7) GENERATED ALWAYS AS ROW START NOT NULL  
        , [ValidTo] [datetime2](7) GENERATED ALWAYS AS ROW END NOT NULL  
        , PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])  
    )  
    WITH( SYSTEM_VERSIONING = ON (HISTORY_TABLE = [dbo].[ProductHistory]   
        , DATA_CONSISTENCY_CHECK = ON ))  
  
```  
  
 下圖顯示經過一段時間的購買情況：  
  
 ![TemporalAnomalyDetection](../../relational-databases/tables/media/temporalanomalydetection.png "TemporalAnomalyDetection")  
  
 假設平日的已購買產品數目擁有較小的差異，下列查詢將會識別單一的極端值 - 這些樣本與其最近的樣本之間有著顯著差異 (2 倍)，同時位於周圍的樣本差異並不顯著 (低於 20%)：  
  
```  
WITH CTE (ProdId, PrevValue, CurrentValue, NextValue, ValidFrom, ValidTo)  
AS  
    (  
        SELECT   
            ProdId, LAG (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as PrevValue  
            , DailySales, LEAD (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as NextValue   
             , ValidFrom, ValidTo from Product  
        FOR SYSTEM_TIME ALL  
)  
  
SELECT   
    ProdId  
    , PrevValue  
    , CurrentValue  
    , NextValue  
    , ValidFrom  
    , ValidTo  
    , ABS (PrevValue - NextValue) / convert (float, (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END)) as PrevToNextDiff  
    , ABS (CurrentValue - PrevValue) / convert (float, (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END)) as CurrentToPrevDiff  
    , ABS (CurrentValue - NextValue) / convert (float, (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END)) as CurrentToNextDiff  
FROM CTE   
    WHERE   
        ABS (PrevValue - NextValue) / (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END) < 0.2  
            AND ABS (CurrentValue - PrevValue) / (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END) > 2  
            AND ABS (CurrentValue - NextValue) / (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END) > 2;  
```  
  
> [!NOTE]  
>  這個範例已刻意簡化。 在生產案例中，您很有可能會使用進階的統計方法來識別沒有遵循一般模式的樣本。  
  
## <a name="slowly-changing-dimensions"></a>緩時變維度  
 資料倉儲中的維度通常會包含關於實體的相對靜態資料，例如地理位置、客戶或產品。 不過，某些案例也會需要您追蹤維度資料表中的資料變更。 由於維度中發生修改的機率較低、發生方式較無法預期，且不會發生在適用於事實資料表的定期更新排程之內，使這類維度資料表被稱為緩時變維度 (SCD)。  
  
 根據變更歷程記錄保留方式的不同，緩時變維度有數個不同的類別：  
  
-   類型 0：不保留歷程記錄。 維度屬性會反映原始值。  
  
-   類型 1：維度屬性會反應最新的值 (先前的值會被覆寫)  
  
-   類型 2：維度成員的每個版本都會在資料表中以個別資料列呈現，並通常以資料行代表有效期間  
  
-   類型 3：透過在相同的資料列中使用額外的資料行，來針對選取屬性保留有限的歷程記錄  
  
-   類型 4：在個別的資料表中保留歷程記錄，同時在原始的維度資料表上保留最新 (目前) 的維度成員版本  
  
 當您選擇 SCD 策略時，ETL 層 (擷取-轉換-載入) 將負責維持維度資料表的準確性，這通常需要大量程式碼和複雜的維護工作。  
  
 SQL Server 2016 中已系統版本設定的時態表可以用來大幅降低程式碼的複雜度，因為資料歷程記錄會自動保留。 由於 SQL Server 2016 中的時態表是使用兩個資料表進行實作，因此它和類別 4 的 SCD 最為相似。 不過，由於 Temporal 查詢允許您僅參照目前的資料表，您也可以在計畫使用類別 2 SCD 的環境中考慮使用時態表。  
  
 若要將一般維度轉換成 SCD，請建立新的資料表，或將現有資料表更改為已系統版本設定的時態表。 如果現有維度資料表內含歷程記錄資料，請建立個別資料表並將歷程記錄資料移至該處，並將目前 (實際) 的維度版本保留在原始的維度資料表中。 然後使用 ALTER TABLE 語法將您的維度資料表轉換成具有預先定義記錄資料表的已系統版本設定時態表。  
  
 下列範例將說明該程序，並假設 DimLocation 維度資料表已擁有 ValidFrom 和 ValidTo 做為 datetime2 不可為 Null 資料行，並由 ETL 程序所填入：  
  
```  
/*Move “closed” row versions into newly created history table*/  
SELECT * INTO  DimLocationHistory  
    FROM DimLocation  
        WHERE ValidTo < '9999-12-31 23:59:59.99';  
GO  
/*Create clustered columnstore index which is a very good choice in DW scenarios*/  
CREATE CLUSTERED COLUMNSTORE INDEX IX_DimLocationHistory ON DimLocationHistory  
/*Delete previous versions from DimLocation which will become current table in temporal-system-versioning configuration*/  
DELETE FROM DimLocation  
    WHERE ValidTo < '9999-12-31 23:59:59.99';  
/*Add period definition*/  
ALTER TABLE DimLocation ADD PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);  
/*Enable system-versioning and bind histiory table to the DimLocation*/  
ALTER TABLE DimLocation SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DimLocationHistory));  
```  
  
 請注意，當您建立 SCD 之後，在資料倉儲載入程序期間，維持 SCD 並不需要額外的程式碼。  
  
 下列說明顯示在涉及 2 個 SCD (DimLocation 和 DimProduct) 和一個事實資料表的簡單案例中使用時態表的方式。  
  
 ![TemporalSCD](../../relational-databases/tables/media/temporalscd.png "TemporalSCD")  
  
 若要在報表中使用上述 SCD，您必須有效地調整查詢。 例如，您可能會想要計算過去六個月中的總銷售量，以及每個資本的平均銷售產品數目。  請注意，上述兩個衡量標準都需要關聯來自事實資料表和維度的資料，這些資料可能會變更其對於分析相當重要的屬性 (DimLocation.NumOfCustomers、DimProduct.UnitPrice)。  下列查詢將能正確地計算所需的衡量標準：  
  
```  
DECLARE @now datetime2 = SYSUTCDATETIME()  
DECLARE @sixMonthsAgo datetime2 SET   
    @sixMonthsAgo = DATEADD (month, -12, SYSUTCDATETIME())   
  
SELECT DimProduct_History.ProductId  
   , DimLocation_History.LocationId  
    , SUM(F.Quantity * DimProduct_History.UnitPrice) AS TotalAmount  
    , AVG (F.Quantity/DimLocation_History.NumOfCustomers) AS AverageProductsPerCapita   
FROM FactProductSales F   
/* find corresponding record in SCD history in last 6 months, based on matching fact */  
JOIN DimLocation FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimLocation_History   
    ON DimLocation_History.LocationId = F.LocationId   
        AND F.FactDate BETWEEN DimLocation_History.ValidFrom AND DimLocation_History.ValidTo   
/* find corresponding record in SCD history in last 6 months, based on matching fact */  
JOIN DimProduct FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimProduct_History   
    ON DimProduct_History.ProductId = F.ProductId  
        AND F.FactDate BETWEEN DimProduct_History.ValidFrom AND DimProduct_History.ValidTo   
    WHERE F.FactDate BETWEEN @sixMonthsAgo AND @now   
GROUP BY DimProduct_History.ProductId, DimLocation_History.LocationId ;  
```  
  
 **考量因素：**  
  
-   如果根據資料庫交易時間所計算的有效期限適用於您的商務邏輯，便可以針對 SCD 使用已系統版本設定的時態表。 如果您載入資料有明顯的延遲，則交易時間可能無法使用。  
  
-   根據預設，已系統版本設定的時態表並不允許於載入後變更歷程記錄資料 (您可以在將 [SYSTEM_VERSIONING] 設定為 [OFF] 之後修改歷程記錄)。 針對時常發生歷程記錄資料變更的案例，這可能會是個限制。  
  
-   已 Temporal 系統版本設定的資料表會針對任何資料行變更產生資料列版本。 如果您想要針對特定資料行變更隱藏新版本，便需要將該限制併入 ETL 邏輯之中。  
  
-   如果您預期 SCD 資料表中會有大量的歷程記錄資料列，請考慮使用叢集資料行存放區索引做為歷程記錄資料表的主要存放區選項。 那將會減少歷程記錄資料表的使用量，並加快您的分析查詢。  
  
## <a name="repairing-row-level-data-corruption"></a>修復資料列層級資料損毀  
 您可以依靠已系統版本設定時態表中的歷程記錄資料，來快速將個別資料列修復為先前所擷取的任何狀態。 時態表的這個屬性，在您可以找出受影響資料列和/或在您知道發生不想要變更之時間的情況下相當有用，並讓您可以非常有效地執行修復，而不必處理備份。  
  
 這個方法有多項優點：  
  
-   您可以精準地控制修復的範圍。 沒有受到影響的記錄必須保持在最新的狀態，這通常是相當重要的需求。  
  
-   作業非常有效率，且資料庫能針對所有使用該資料的工作負載持續保持連線。  
  
-   修復作業本身已進行版本設定。 您擁有修復作業本身的稽核線索，因此如有必要，您可以於稍後針對發生的情況進行分析。  
  
 修復動作可以相對輕鬆地進行自動化。 下列為針對於資料稽核案例中所使用之「員工」資料表進行資料修復之預存程序的程式碼範例。  
  
```  
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecord;  
GO  
  
CREATE PROCEDURE sp_RepairEmployeeRecord   
    @EmployeeID INT,  
    @versionNumber INT = 1  
AS  
  
;WITH History  
AS  
(  
        /* Order historical rows by tehir age in DESC order*/  
        SELECT ROW_NUMBER () OVER (PARTITION BY EmployeeID ORDER BY [ValidTo] DESC) AS RN, *  
        FROM Employee FOR SYSTEM_TIME ALL WHERE YEAR (ValidTo) < 9999 AND Employee.EmployeeID = @EmployeeID  
)  
  
/*Update current row by using N-th row version from history (default is 1 - i.e. last version)*/  
UPDATE Employee   
    SET [Position] = H.[Position], [Department] = H.Department, [Address] = H.[Address], AnnualSalary = H.AnnualSalary  
    FROM Employee E JOIN History H ON E.EmployeeID = H.EmployeeID AND RN = @versionNumber  
    WHERE E.EmployeeID = @EmployeeID  
  
```  
  
 此預存程序會採用 @EmployeeID 和 @versionNumber 作為輸入參數。 這個程序根據預設會將資料列狀態還原到歷程記錄的最新版本 (@versionNumber = 1)。  
  
 下圖顯示程序引動過程之前和之後的資料列狀態。 紅色矩形標示目前不正確的資料列版本，而綠色矩形則從歷程記錄標示正確的版本。  
  
 ![TemporalUsageRepair1](../../relational-databases/tables/media/temporalusagerepair1.png "TemporalUsageRepair1")  
  
```  
EXEC sp_RepairEmployeeRecord @EmployeeID = 1, @versionNumber = 1  
```  
  
 ![TemporalUsageRepair2](../../relational-databases/tables/media/temporalusagerepair2.png "TemporalUsageRepair2")  
  
 這個修復預存程序可以定義為接受確切時間戳記，而非資料列版本。 它會把資料列還原為於提供之時間點作用的任何版本 (例如 AS OF 時間點)。  
  
```  
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecordAsOf;  
GO  
  
CREATE PROCEDURE sp_RepairEmployeeRecordAsOf   
    @EmployeeID INT,  
    @asOf datetime2  
AS  
  
/*Update current row to the state that was actual AS OF provided date*/  
UPDATE Employee   
    SET [Position] = History.[Position], [Department] = History.Department, [Address] = History.[Address], AnnualSalary = History.AnnualSalary  
    FROM Employee AS E JOIN Employee FOR SYSTEM_TIME AS OF @asOf AS History  ON E.EmployeeID = History.EmployeeID  
    WHERE E.EmployeeID = @EmployeeID  
  
```  
  
 針對相同的資料範例，下圖說明具有時間條件的修復案例。 醒目提示的項目為 @asOf 參數、在歷程記錄中於提供之時間點作用的選取資料列，以及修復作業後在目前資料表中的新資料列版本：  
  
 ![TemporalUsageRepair3](../../relational-databases/tables/media/temporalusagerepair3.png "TemporalUsageRepair3")  
  
 資料更正可以成為資料倉儲和報告系統中自動資料載入的一部分。  
如果剛更新的值並不正確，在許多情況下，從歷程記錄還原為先前的版本已是可接受的移轉。 下圖顯示對此程序進行自動化的方式：  
  
 ![TemporalUsageRepair4](../../relational-databases/tables/media/temporalusagerepair4.png "TemporalUsageRepair4")  
  
## <a name="see-also"></a>另請參閱  
 [時態表](../../relational-databases/tables/temporal-tables.md)   
 [開始使用系統建立版本的時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [對時態表進行資料分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [時態表考量與限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [時態表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

