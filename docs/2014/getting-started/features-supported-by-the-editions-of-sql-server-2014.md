---
title: SQL Server 2014 版本所支援的功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caae4212e2182ae6afde29b0fed1aaee4f05645a
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2020
ms.locfileid: "78339288"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>SQL Server 2014 各版本所支援的功能


  本主題提供不同 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]版本所支援功能的詳細資料。 

 > **注意：** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在評估版中，有180天的試用期間可供使用。 如需詳細資訊，請[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]參閱[試用軟體網站](https://go.microsoft.com/fwlink/?LinkId=190955)。  
> 
> **注意：** 如需評估和開發人員版本所支援的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能，請參閱企業功能集。  
  
 若要導覽至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 技術的資料表，請按一下其連結：  
  
 [跨主機殼縮放限制](#CrossBoxScale)  
  
 [高可用性](#High_availability)  
  
 [延展性和效能](#Scalability)  
  
 [安全性](#Enterprise_security)  
  
 [複寫](#Replication)  
  
 [管理工具](#Mgmt_Tools)  
  
 [RDBMS 管理能力](#RDBMS_mgmt)  
  
 [開發工具](#Dev_tools)  
  
 [序](#Programmability)  
  
 [Integration Services](#SSIS)  
  
 [Integration Services – 進階配接器](#SSIS_AA)  
  
 [Integration Services – 進階轉換](#SSIS_AT)  
  
 [Master Data Services](#MDS)  
  
 [資料倉儲 (data warehouse)](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [BI 語意模型 (多維度)](#BISemModel_multi)  
  
 [BI 語義模型（表格式）](#BISemModel_tabular)  
  
 [PowerPivot for SharePoint](#PowerPivot)  
  
 [資料採礦](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [商業智慧用戶端](#BIClients)  
  
 [空間和位置服務](#Spatial)  
  
 [其他資料庫服務](#Add_DBServices)  
  
 [其他元件](#Other_Components)  
  
##  <a name="CrossBoxScale"></a>跨主機殼縮放限制  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|單一實例所使用的計算容量上限（[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]資料庫引擎）<sup>1</sup>|作業系統最大值|限制為 4 個插槽或 16 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|  
|單一實例所使用的計算容量上限（Analysis Services、Reporting Services） <sup>1</sup>|作業系統最大值|作業系統最大值|限制為 4 個插槽或 16 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|  
|使用的記憶體上限 ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Database Engine 的每個執行個體)|作業系統最大值|128 GB|128 GB|64 GB|1 GB|1 GB|1 GB|  
|使用的記憶體上限 ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的每個執行個體)|作業系統最大值|作業系統最大值|64 GB|N/A|N/A|N/A|N/A|  
|使用的記憶體上限 ( [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]的每個執行個體)|作業系統最大值|作業系統最大值|64 GB|64 GB|4 GB|N/A|N/A|  
|關聯式資料庫大小上限|524 PB|524 PB|524 PB|524 PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup> Enterprise Edition （含伺服器 + 用戶端存取許可證（CAL））型授權（不適用於新合約）僅限每個[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]實例最多20個核心。 核心伺服器授權模式之下沒有任何限制。 如需詳細資訊，請參閱[依版本 SQL Server 的計算容量限制](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
##  <a name="High_availability"></a>高可用性  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Server Core 支援<sup>1</sup>|是|是|是|是|是|是|是|  
|記錄傳送|是|是|是|是||||  
|資料庫鏡像|是|是 (僅限 Safety Full)|是 (僅限 Safety Full)|僅限見證|僅限見證|僅限見證|僅限見證|  
|備份壓縮|是|是|是|||||  
|資料庫快照集|是|||||||  
|AlwaysOn 容錯移轉叢集執行個體|是 (節點支援：作業系統最大值)|是 (節點支援：2)|是 (節點支援：2)|||||  
|AlwaysOn 可用性群組|是 (最多 8 個次要複本，包括 2 個同步次要複本)|||||||  
|連接導向器|是|||||||  
|線上頁面和檔案還原|是|||||||  
|線上檢索索引|是|||||||  
|線上結構描述變更|是|||||||  
|快速復原|是|||||||  
|鏡像備份|是|||||||  
|熱新增記憶體和 CPU<sup>2</sup>|是|||||||  
|Database Recovery Advisor|是|是|是|是|是|是|是|  
|加密的備份|是|是|是|||||  
|智慧型備份|是|是|是|否||||  
  
 <sup>1</sup>如需有關在 Server [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] core 上安裝的詳細資訊，請參閱[在 Server core 上安裝 SQL Server 2014](../database-engine/install-windows/install-sql-server-on-server-core.md)。  
  
 <sup>2</sup>這項功能僅適用于64位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
##  <a name="Scalability"></a>擴充性和效能  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|多個執行個體支援|50|50|50|50|50|50|50|  
|資料表和索引分割區|是|||||||  
|資料壓縮|是|||||||  
|資源管理員|是|||||||  
|分割區資料表平行處理原則|是|||||||  
|多個檔案資料流容器|是|||||||  
|NUMA 感知大型分頁記憶體和緩衝區陣列配置|是|||||||  
|緩衝集區延伸模組<sup>1</sup>|是|是|是|||||  
|IO 資源管理|是|||||||  
|記憶體內部 OLTP <sup>1</sup>|是|||||||  
|延遲持久性|是|是|是|是|是|是|是|  
  
 <sup>1</sup>此功能僅適用于64位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
##  <a name="Enterprise_security"></a> Security  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|基本稽核|是|是|是|是|是|是|是|  
|細部稽核|是|||||||  
|透明資料庫加密|是|||||||  
|可延伸金鑰管理|是|||||||  
|使用者定義角色|是|是|是|是|是|是|是|  
|自主資料庫|是|是|是|是|是|是|是|  
|備份的加密|是|是|是|||||  
  
##  <a name="Replication"></a> 複寫  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]變更追蹤|是|是|是|是|是|是|是|  
|合併式複寫|是|是|是|是 (僅限訂閱者)|是 (僅限訂閱者)|是 (僅限訂閱者)|是 (僅限訂閱者)|  
|異動複寫|是|是|是|是 (僅限訂閱者)|是 (僅限訂閱者)|是 (僅限訂閱者)|是 (僅限訂閱者)|  
|快照式複寫|是|是|是|是 (僅限訂閱者)|是 (僅限訂閱者)|是 (僅限訂閱者)|是 (僅限訂閱者)|  
|異質性訂閱者|是|是|是|||||  
|Oracle 發行|是|||||||  
|點對點異動複寫|是|||||||  
  
##  <a name="Mgmt_Tools"></a>管理工具  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|SQL 管理物件 (SMO)|是|是|是|是|是|是|是|  
|SQL 組態管理員|是|是|是|是|是|是|是|  
|SQL CMD (命令提示字元工具)|是|是|是|是|是|是|是|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Management Studio|是|是|是|是|是|是||  
|Distributed Replay - 管理工具|是|是|是|是|是|是||  
|Distributed Replay - Client|是|否|是|是||||  
|Distributed Replay - Controller|Yes (Enterprise 最多支援 16 個用戶端，Developer 僅支援 1 個用戶端)|否|Yes (僅支援 1 個用戶端)|Yes (僅支援 1 個用戶端)||||  
|SQL Profiler|是|是|是|否<sup>2</sup>|否<sup>2</sup>|否<sup>2</sup>|否<sup>2</sup>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent|是|是|是|是||||  
|Microsoft System Center Operations Manager 管理組件|是|是|是|是||||  
|Database Tuning Advisor (DTA)|是|是|是<sup>3</sup>|是<sup>3</sup>||||  
|將[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]資料庫部署至 Azure VM Wizard|是|是|是|是|是|是|是|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Azure 中的資料檔案|是|是|是|是|是|是|是|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Web、 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]、 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Tools 和[!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services 可以使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard 和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 版本進行分析。  
  
 <sup>3</sup>僅針對 Standard edition 功能啟用微調。  
  
##  <a name="RDBMS_mgmt"></a>RDBMS 管理能力  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|使用者執行個體|||||是|是|是|  
|LocalDB|||||是|是||  
|專用管理員連接|是|是|是|是|是 (在追蹤旗標下方)|是 (在追蹤旗標下方)|是 (在追蹤旗標下方)|  
|PowerShell 指令碼支援|是|是|是|是|是|是|是|  
|SysPrep 支援<sup>1</sup>|是|是|是|是|是|是|是|  
|資料層應用程式元件作業的支援-解壓縮、部署、升級、刪除|是|是|是|是|是|是|是|  
|原則自動化 (依排程和變更檢查)|是|是|是|是||||  
|效能資料收集器|是|是|是|是||||  
|能夠在多重執行個體管理中註冊為受管理的執行個體|是|是|是|是||||  
|標準效能報告|是|是|是|是||||  
|計畫指南和計畫指南的計畫凍結|是|是|是|是||||  
|索引檢視表的直接查詢 (使用 NOEXPAND 提示)|是|是|是|是||||  
|自動索引檢視表維護|是|是|是|是||||  
|分散式分割區檢視|是|部分。 分散式分割區檢視無法更新|部分。 分散式分割區檢視無法更新|部分。 分散式分割區檢視無法更新|部分。 分散式分割區檢視無法更新|部分。 分散式分割區檢視無法更新|部分。 分散式分割區檢視無法更新|  
|平行索引作業|是|||||||  
|查詢最佳化工具自動使用索引檢視表|是|||||||  
|平行一致性檢查|是|||||||  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式控制點|是|||||||  
|自主資料庫|是|是|是|是|是|是|是|  
|緩衝集區延伸模組<sup>2</sup>|是|是|是|||||  
  
 <sup>1</sup>如需詳細資訊，請參閱[使用 SysPrep 安裝 SQL Server 的考慮](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)。  
  
 <sup>2</sup>這項功能僅適用于64位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
##  <a name="Dev_tools"></a>開發工具  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[msCoName](../includes/msconame-md.md)]Visual Studio 整合|是|是|是|是|是|是|是|  
|Intellisense ([!INCLUDE[tsql](../includes/tsql-md.md)] 和 MDX)|是|是|是|是|是|是|是|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|是|是|是|是|是|||  
|SQL 查詢編輯和設計工具<sup>1</sup>|是|是|是|||||  
|版本控制支援<sup>1</sup>|是|是|是|||||  
|MDX 編輯、debug 和設計工具<sup>1</sup>|是|是|是|||||  
  
 <sup>1</sup>這項功能不適用於64位版本的 Standard edition。  
  
##  <a name="Programmability"></a> Programmability  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Common Language Runtime (CLR) 整合|是|是|是|是|是|是|是|  
|原生 XML 支援|是|是|是|是|是|是|是|  
|XML 索引|是|是|是|是|是|是|是|  
|MERGE & UPSERT 功能|是|是|是|是|是|是|是|  
|FILESTREAM 支援|是|是|是|是|是|是|是|  
|FileTable|是|是|是|是|是|是|是|  
|日期和時間資料類型|是|是|是|是|是|是|是|  
|國際化支援|是|是|是|是|是|是|是|  
|全文檢索和語意搜尋|是|是|是|是|是|||  
|查詢中的語言規格|是|是|是|是|是|||  
|Service Broker (訊息)|是|是|是|否 (僅限用戶端)|否 (僅限用戶端)|否 (僅限用戶端)|否 (僅限用戶端)|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]終點|是|是|是|是||||  
  
##  <a name="SSIS"></a> Integration Services  
  
|功能|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 匯入和匯出精靈|是|是|是|是|是|是|是|  
|內建的資料來源連接器|是|是|是|是|是|是|是|  
|SSIS 設計師和執行階段|是|是|是|||||  
|基本轉換|是|是|是|||||  
|基本資料分析工具|是|是|是|||||  
|Attunity Oracle 異動資料擷取服務|是|||||||  
|Attunity Oracle 異動資料擷取設計工具|是|||||||  
  
###  <a name="SSIS_AA"></a>Integration Services-Advanced 介面卡  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|高效能 Oracle 目的地|是|||||||  
|高效能 Teradata 目的地|是|||||||  
|SAP BW 來源和目的地|是|||||||  
|資料採礦模型定型目的地配接器|是|||||||  
|維度處理目的地配接器|是|||||||  
|分割區處理目的地配接器|是|||||||  
|Attunity 異動資料擷取元件|是|||||||  
|Attunity 開放式資料庫連接 (ODBC) 連接器|是|||||||  
  
###  <a name="SSIS_AT"></a>Integration Services-Advanced 轉換  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|持續的 (高效能) 查閱|是|||||||  
|資料採礦查詢轉換|是|||||||  
|模糊群組和查閱轉換|是|||||||  
|詞彙擷取與查閱轉換|是|||||||  
  
##  <a name="MDS"></a>Master Data Services  
  
> [!NOTE]  
>  -   
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 只能在 64 位元版本的 Business Intelligence 和 Enterprise 上使用。  
  
|功能|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]資料|是|是||||||  
|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]web 應用程式|是|是||||||  
  
##  <a name="Data_warehouse"></a>資料倉儲  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|建立不含資料庫的 Cube|是|是|是|||||  
|自動產生暫存和資料倉儲結構描述|是|是|是|||||  
|變更資料擷取|是|||||||  
|星型聯結查詢最佳化|是|||||||  
|可擴充的唯讀 Analysis Services 組態|是|||||||  
|分割區資料表和索引上的查詢平行處理|是|||||||  
|xVelocity 記憶體最佳化的資料行存放區索引|是|||||||  
|全域批次彙總|是|||||||  
  
##  <a name="SSAS"></a>Analysis Services  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|可擴充共用資料庫 (附加/卸離唯讀資料庫)|是|是||||||  
|備份/還原、附加/卸離資料庫|是|是|是|||||  
|同步處理資料庫|是|是||||||  
|高可用性|是|是|是|||||  
|可程式性 (AMO、ADOMD.Net、OLEDB、XML/A、ASSL)|是|是|是|||||  
  
###  <a name="BISemModel_multi"></a>BI 語義模型（多維度）  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|局部加總量值|是|是|否<sup>1</sup>|||||  
|階層|是|是|是|||||  
|KPI|是|是|是|||||  
|檢視方塊|是|是||||||  
|動作|是|是|是|||||  
|帳戶智慧|是|是|是|||||  
|時間智慧|是|是|是|||||  
|自訂積存|是|是|是|||||  
|回寫 Cube|是|是|是|||||  
|回寫維度|是|是||||||  
|回寫資料格|是|是|是|||||  
|鑽研|是|是|是|||||  
|進階階層類型 (父子式、不完全階層)|是|是|是|||||  
|進階維度 (參考維度、多對多維度)|是|是|是|||||  
|連結量值和維度|是|是||||||  
|翻譯|是|是|是|||||  
|彙總|是|是|是|||||  
|多個分割區|是|是|是，最多 3 個|||||  
|主動式快取|是|是||||||  
|自訂組件 (預存程序)|是|是|是|||||  
|MDX 查詢和指令碼|是|是|是|||||  
|DAX 查詢|是|是||||||  
|以角色為基礎的安全性模型|是|是|是|||||  
|維度和資料格層級安全性|是|是|是|||||  
|可擴充字串儲存體|是|是|是|||||  
|MOLAP、ROLAP、HOLAP 儲存模式|是|是|是|||||  
|二進位和壓縮 XML 傳輸|是|是|是|||||  
|發送模式處理|是|是||||||  
|直接回寫|是|是||||||  
|量值運算式|是|是||||||  
  
 <sup>1</sup>LastChild 局部加總量值在 standard edition 中有受到支援，但是其他局部加總量值（例如 None、FirstChild、FirstNonEmpty、LastNonEmpty、AverageOfChildren 和 ByAccount）則不是。 所有的版本都支援加總量值 (例如 Sum、Count、Min、Max) 和非加總量值 (DistinctCount)。  
  
###  <a name="BISemModel_tabular"></a>BI 語義模型（表格式）  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|階層|是|是||||||  
|KPI|是|是||||||  
|檢視方塊|是|是||||||  
|翻譯|是|是||||||  
|DAX 計算、DAX 查詢、MDX 查詢|是|是||||||  
|資料列層級安全性|是|是||||||  
|資料分割|是|是||||||  
|InMemory 和 DirectQuery 儲存模式 (僅限表格式)|是|是||||||  
  
###  <a name="PowerPivot"></a>PowerPivot for SharePoint  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|以共用服務架構為基礎的 SharePoint 伺服器陣列整合|是|是||||||  
|使用量回報|是|是||||||  
|健全狀況監視規則|是|是||||||  
|PowerPivot 圖庫|是|是||||||  
|PowerPivot 資料重新整理|是|是||||||  
|PowerPivot 資料摘要|是|是||||||  
  
###  <a name="DataMining"></a>資料採礦  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|標準演算法|是|是|是|||||  
|資料採礦工具 (精靈、編輯器、查詢產生器)|是|是|是|||||  
|交叉驗證|是|是||||||  
|已篩選之採礦結構資料子集的模型|是|是||||||  
|時間序列：ARTXP 和 ARIMA 方法之間的自訂混合|是|是||||||  
|時間序列：以新的資料預測|是|是||||||  
|無限制的並行 DM 查詢|是|是||||||  
|適用于資料採礦演算法的 Advanced Configuration & 微調選項|是|是||||||  
|支援外掛程式演算法|是|是||||||  
|平行模型處理|是|是||||||  
|時間序列：跨序列預測|是|是||||||  
|無限制的關聯規則屬性|是|是||||||  
|順序預測|是|是||||||  
|貝氏機率、類神經網路和羅吉斯迴歸的多個預測目標|是|是||||||  
  
##  <a name="Reporting"></a>Reporting Services  
  
###  <a name="Reporting_features"></a>Reporting Services 功能  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|支援的目錄 DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Standard 或更高版本|Standard 或更高版本|Standard 或更高版本|Web|Express|||  
|支援的資料來源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所有版本|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所有版本|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所有版本|Web|Express|||  
|報表伺服器|是|是|是|是|是|||  
|報表設計師|是|是|是|是|是|||  
|報表管理員|是|是|是|是|是|||  
|以角色為基礎的安全性|是|是|是|是|是|||  
|Word 匯出和 RTF 支援|是|是|是|是|是|||  
|增強的量測計和圖表|是|是|是|是|是|||  
|匯出至 Excel、PDF 和影像|是|是|是|是|是|||  
|自訂驗證|是|是|是|是|是|||  
|報告成資料摘要|是|是|是|是|是|||  
|模型支援|是|是|是|是||||  
|針對以角色為基礎的安全性建立自訂角色|是|是|是|||||  
|模型項目安全性|是|是|是|||||  
|無限點選連結|是|是|是|||||  
|共用元件程式庫|是|是|是|||||  
|電子郵件和檔案共用訂閱與排程|是|是|是|||||  
|報表記錄、執行快照集和快取|是|是|是|||||  
|SharePoint 整合|是|是|是|||||  
|遠端及非 SQL 資料來源支援<sup>1</sup>|是|是|是|||||  
|資料來源、傳遞和轉譯、RDCE 擴充性|是|是|是|||||  
|資料驅動報表訂閱|是|是||||||  
|向外延展部署 (Web 伺服器陣列)|是|是||||||  
|警示<sup>2</sup>|是|是||||||  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]<sup>2</sup>|是|是||||||  
  
 <sup>1</sup>如需有關中[!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]支援之資料來源的詳細資訊，請參閱[Reporting Services &#40;SSRS&#41;支援的資料來源](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
 <sup>2</sup>需要[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式的。 如需詳細資訊，請參閱[Reporting Services Sharepoint 模式安裝 &#40;sharepoint 2010 和 sharepoint 2013&#41;](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
### <a name="report-server-database-server-edition-requirements"></a>報表伺服器資料庫伺服器版本需求  
 建立報表伺服器資料庫時，並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本都可以用來主控資料庫。 下表顯示哪些 [!INCLUDE[ssDE](../includes/ssde-md.md)] 版本可用於特定的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]版本。  
  
|對於這一版的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|使用這一版的 Database Engine 執行個體來主控資料庫|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Standard、Business Intelligence Enterprise 版 (本機或遠端)|  
|商業智慧|Standard、Business Intelligence Enterprise 版 (本機或遠端)|  
|標準|Standard、Enterprise Edition (本機或遠端)|  
|Web|Web Edition (僅限本機)|  
|Express with Advanced Services|Express with Advanced Services (僅限本機)。|  
|評估|評估|  
  
##  <a name="BIClients"></a>商業智慧用戶端  
 您可以透過 Microsoft 下載中心取得下列軟體用戶端應用程式，這些應用程式是提供來協助您建立可在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上執行的商業智慧文件。 當您在伺服器環境中裝載這些文件時，請使用支援該文件類型的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 下表將識別哪些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本包含裝載在這些用戶端應用程式中建立之文件所需的伺服器功能。  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|是|是|是|||||  
|適用於 Excel 及 Visio 2010 的資料採礦增益集|是|是|是|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)]2010|是|是||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|是|是||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)]是 Excel 增益集，不依賴[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 不過，若要在 SharePoint 中共用 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 活頁簿並進行共同作業，則需要使用 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] ，而且這項功能是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 和 Business Intelligence Edition 的一部分。  
> 2.  上表識別啟用這些用戶端工具所需的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。不過，這些功能可以存取任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本上裝載的資料。  
  
##  <a name="Spatial"></a>空間和位置服務  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|空間索引|是|是|是|是|是|是|是|  
|平面與 Geodetic 資料類型|是|是|是|是|是|是|是|  
|進階空間程式庫|是|是|是|是|是|是|是|  
|匯入/匯出業界標準空間資料格式|是|是|是|是|是|是|是|  
  
##  <a name="Add_DBServices"></a>其他資料庫服務  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|是|是|是|是|是|是|是|  
|Database Mail|是|是|是|是||||  
  
##  <a name="Other_Components"></a>其他元件  
  
|功能名稱|Enterprise|商業智慧|標準|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Data Quality Services|是|是||||||  
|StreamInsight|StreamInsight Premium 版|StreamInsight Standard 版|StreamInsight Standard 版|StreamInsight Standard 版||||  
|StreamInsight HA|StreamInsight Premium 版|||||||  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 的產品規格](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [SQL Server 2014 的安裝](../database-engine/install-windows/installation-for-sql-server.md)   
 [SQL Server 2014 快速入門安裝](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
