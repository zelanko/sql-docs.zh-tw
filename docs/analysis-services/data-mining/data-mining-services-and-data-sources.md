---
title: "資料採礦服務與資料來源 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b26fd6e3-7d87-4f66-ab47-5303b51b87da
caps.latest.revision: 19
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 19
---
# 資料採礦服務與資料來源
  資料採礦會要求建立與 SQL Server Analysis Services 執行個體的連接。 資料採礦不需要 Cube 中的資料，而且建議您使用關聯式來源；但是資料採礦會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎所提供的元件。  
  
 此主題將提供一些在您連接至 SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體來建立、處理、部署或查詢資料採礦模型時所需要了解的資訊。  
  
## 資料採礦服務  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的伺服器元件是 msmdsrv.exe 應用程式，這個應用程式通常是當做 Windows 服務來執行。 這個應用程式是由安全性元件、XML for Analysis (XMLA) 接聽程式元件、查詢處理器元件及執行下列功能的許多其他內部元件所組成：  
  
-   剖析從用戶端收到的陳述式  
  
-   管理中繼資料  
  
-   處理交易  
  
-   處理計算  
  
-   儲存維度和資料格資料  
  
-   建立彙總  
  
-   排程查詢  
  
-   快取物件  
  
-   管理伺服器資源  
  
### XMLA 接聽程式  
 XMLA 接聽程式元件會處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 及其用戶端之間的所有 XMLA 通訊。 msmdsrv.ini 檔中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [通訊埠] 組態設定可用來指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體所接聽的通訊埠。 這個檔案中 0 的值表示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會接聽預設通訊埠。 除非另有指定，否則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用下列預設 TCP 通訊埠：  
  
|通訊埠|說明|  
|----------|-----------------|  
|2383|預設的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。|  
|2382|其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的重新導向程式。|  
|在伺服器啟動時動態指派|具名的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。|  
  
 如需控制此服務使用之通訊埠的詳細資訊，請參閱[設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
## 連接到資料來源  
 每當您建立或更新資料採礦結構或模型時，就會使用資料來源所定義的資料。 此資料來源不包含資料，資料可能包含 Excel 活頁簿、文字檔和 SQL Server 資料庫；資料來源只會定義連接資訊。  資料來源檢視 (DSV) 會當做該來源上方的抽象層，修改或對應從來源取得的資料。  
  
 它超出本主題的範圍 (本主題會描述每一個來源的連接需求)。 如需詳細資訊，請參閱提供者的文件集。 但是一般而言，當您與提供者互動時，應該留意以下的 Analysis Services 需求：  
  
-   因為資料採礦是伺服器所提供的服務，所以必須將資料來源的存取權提供給 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  存取有兩個層面：位置和識別。  
  
     **位置**：表示如果您只使用電腦上所儲存的資料，然後將模型部署至伺服器來建立模型，此模型將無法處理，因為找不到資料來源。 若要解決此問題，您可能必須將資料移轉到執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的相同 SQL Server 執行個體，或是將檔案移到共用位置。  
  
     **識別**：表示 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 上的服務必須能夠使用適當的認證開啟資料檔或資料來源。 例如，當您建立模型時，您可能擁有檢視資料的無限權限，但是在伺服器上處理及更新模型的使用者可能擁有資料的有限存取權或無任何存取權，這樣可能會導致處理失敗或影響模型的內容。 用來連接遠端資料來源的帳戶至少必須擁有資料的讀取權限。  
  
-   當您移動模型時，也會有相同的需求：您必須設定適當的權限來存取舊的資料來源的位置、複製資料來源，或設定新的資料來源。 此外，您也必須移轉登入和角色，或是設定權限來允許在新的位置中處理和更新資料採礦物件。  
  
## 設定權限和伺服器屬性  
 資料採礦需要 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的額外權限。 您可以使用 [Analysis Server 屬性對話方塊 &#40;Analysis Services&#41;](../Topic/Analysis%20Server%20Properties%20Dialog%20Box%20\(Analysis%20Services\).md) 來設定大部分的資料採礦屬性。  
  
 如需您可以設定之屬性的詳細資訊，請參閱 [Analysis Services 的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 下列伺服器屬性與資料採礦特別相關：  
  
-   **AllowAdHocOpenRowsetQueries**：控制直接載入伺服器記憶體空間之 OLE DB 提供者的特定存取。  
  
    > [!IMPORTANT]  
    >  若要改善安全性，我們建議您將這個屬性設定為 **false**。 預設值是 **false**秒。 不過，即使這個屬性設定為 **false**，使用者仍然可以繼續建立單一查詢，而且可以針對允許的資料來源使用 OPENQUERY。  
  
-   **AllowedProvidersInOpenRowset**：指定提供者 (如果已啟用特定存取的話)。 您可以透過輸入逗號分隔的 ProgID 清單，指定多個提供者。  
  
-   **MaxConcurrentPredictionQueries**：控制預測所造成的伺服器負載。 預設值 0 允許無限制的查詢 (適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise)，而最大值是五個並行查詢 (適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard)。 超過此限制的查詢會進行序列化而且可能會逾時。  
  
 此伺服器會提供可控制哪些資料採礦演算法可用的其他屬性，包括演算法的任何相關限制，以及所有資料採礦服務的預設值。 不過，目前沒有任何設定可讓您特別控制資料採礦預存程序的存取權。 如需詳細資訊，請參閱[資料採礦屬性](../../analysis-services/server-properties/data-mining-properties.md)。  
  
 您也可以設定屬性，以便微調伺服器以及控制用戶端使用量的安全性。 如需詳細資訊，請參閱[功能屬性](../../analysis-services/server-properties/feature-properties.md)。  
  
> [!NOTE]  
>  如需支援外掛程式演算法之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的詳細資訊，請參閱 [SQL Server 2012 版本支援的功能](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473)。  
  
## 以程式設計方式存取資料採礦物件  
 您可以使用下列物件模型來建立 Analysis Services 資料庫的連接以及使用資料採礦物件：  
  
 **ADO**：使用 OLE DB 來連接至 Analysis Services 伺服器。 當您使用 ADO 時，用戶端就會限制為結構描述資料列集查詢和 DMX 陳述式。  
  
 **ADO.NET**：與 SQL Server 提供者互動的效果比其他提供者較佳。 使用資料配接器來儲存動態資料列集。 使用資料集物件，而這是儲存成可當做 XML 進行更新或儲存之資料表的伺服器資料快取。  
  
 **ADOMD.NET**：針對使用資料採礦和 OLAP 最佳化的 Managed 資料提供者。 相較於 ADO.NET 而言，ADOMD.NET 的速度較快而且記憶體效率較高。 ADOMD.NET 也可以讓您擷取有關伺服器物件的中繼資料。 建議用戶端應用程式採用 (.NET 無法使用時除外)。  
  
 **Server ADOMD**：直接在伺服器上存取 Analysis Services 物件的物件模型。 由 Analysis Services 預存程序使用，但不適合用戶端使用。  
  
 **AMO**：取代決策支援物件 (DSO) 的 Analysis Services 管理介面。 反覆運算物件等作業在使用 AMO 時會比使用其他介面需要更高的權限。 這是因為 AMO 會直接存取中繼資料，而 ADOMD.NET 和其他介面只會存取資料庫結構描述。  
  
### 伺服器的瀏覽和查詢存取  
 您可以使用 OLAP/資料採礦模式中的 Analysis Services 執行個體來執行所有種類的預測，但是有下列限制：  
  
-   如果您使用伺服器 ADOMD，就可以使用 DMX 來存取伺服器，而不需要建立連接。 然後，您可以將結果直接複製到資料表中。 不過，您無法使用 Server ADOMD 搭配遠端執行個體。您只能查詢本機伺服器。  
  
-   ADO.NET 不支援適用於資料採礦的具名參數。 您必須使用 ADOMD.NET。  
  
-   ADOMD.NET 可讓您傳遞整個資料表，以便當做參數使用。因此，您可以使用用戶端的資料，或是伺服器無法使用的資料。 您也可以將已成形的資料表當做預測輸入使用。  
  
### 使用資料採礦預存程序  
 預存程序的常見用法是封裝查詢，以便重複使用。 用戶端可以使用 CALL 來執行預存程序，包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 系統預存程序。  
  
 如果此程序傳回資料集，用戶端將會收到資料集或資料表，其中具有包含資料列的巢狀資料表。 例如，如果您針對模型內容建立查詢，此查詢會傳回整個模型。 若要避免傳回太多資料列，您可以使用 ADOMD+ 物件模型來撰寫預存程序。  
  
 若要撰寫伺服器預存程序，您必須參考 Microsoft.AnalysisServices.AdomdServer 命名空間。 如需如何建立和使用預存程序的詳細資訊，請參閱[使用者定義函數和預存程序](../../analysis-services/multidimensional-models-adomd-net-server/user-defined-functions-and-stored-procedures.md)。  
  
> [!NOTE]  
>  預存程序無法用來變更資料伺服器物件的安全性。 當您執行某個預存程序時，使用者的目前內容就會用來決定所有伺服器物件的存取權。 因此，使用者必須針對他們所存取的任何資料庫物件擁有適當的權限。  
  
## 請參閱＜  
 [實體架構 &#40;Analysis Services - 多維度資料&#41;](../Topic/Physical%20Architecture%20\(Analysis%20Services%20-%20Multidimensional%20Data\).md)   
 [實體架構 &#40;Analysis Services – 資料採礦&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [資料採礦方案與物件的管理](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)  
  
  