---
title: SQL Server 的最大容量規格 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [SQL Server]
- number capacity specifications [SQL Server]
- size [SQL Server], capacity specifications
- number of objects
- capacity specifications [SQL Server]
- maximum capacity specifications [SQL Server]
- size [SQL Server]
- replication capacity specifications [SQL Server]
- objects [SQL Server], capacity specifications
- Database Engine [SQL Server], capacity specifications
ms.assetid: 13e95046-0e76-4604-b561-d1a74dd824d7
caps.latest.revision: 76
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 08997fa0dd4fe66b4e3c22fd6447105d11991c29
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37296038"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>SQL Server 的最大容量規格
  下表指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件中已定義之各種物件的大小和數目上限。 若要導覽至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 技術的資料表，請按一下其連結：  
  
 [SQL Server Database Engine 物件](#Engine)  
  
 [SQL Server 公用程式物件](#Utility)  
  
 [SQL Server 資料層應用程式物件](#DAC)  
  
 [SQL Server 複寫物件](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] 物件  
 下表指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中已定義或 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式中所參考之各種物件的大小和數目上限。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 物件 (object)|大小/數目上限[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]（32 位元）|大小/數目上限 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 位元)|  
|---------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|批次大小<br /><br /> 注意： 網路封包大小是用來溝通應用程式與關聯式的表格式資料流 (TDS) 封包大小[!INCLUDE[ssDE](../includes/ssde-md.md)]。 預設封包大小是 4 KB，由 network packet size 組態選項所控制。|65,536 * 網路封包大小|65,536 * 網路封包大小|  
|每個短字串資料行的位元組數|8,000|8,000|  
|每個 GROUP BY、ORDER BY 的位元組數|8,060|8,060|  
|每個索引鍵的位元組數<br /><br /> 注意： 任何索引鍵中的位元組數目上限不能超過 900 中的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 假設這些資料行內從未插入超過 900 位元組的資料，則您可使用大小上限累加超過 900 的可變長度資料行定義索引鍵。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，您可以在非叢集索引中包含非索引鍵資料行，以避免達到最大索引鍵大小 900 個位元組。|900|900|  
|每個外部索引鍵的位元組數|900|900|  
|每個主索引鍵的位元組|900|900|  
|每個資料列的位元組數<br /><br /> 注意：<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援資料列溢位儲存，好讓可變長度資料行可以非資料列形式推送。 只有 24 位元組的根會儲存在從資料列發送之可變長度資料行的主要記錄中；因此，有效資料列限制高於舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》中的＜超過 8 KB 的資料列溢位資料＞主題。|8,060|8,060|  
|記憶體最佳化資料表中每個資料列的位元組數<br /><br /> 注意：<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 記憶體內部 OLTP 不支援資料列溢位儲存體。 可變長度資料行不是發送的資料列。 這會限制您可以在記憶體最佳化資料表中指定至最大資料列大小的可變長度資料行之最大寬度。 如需詳細資訊，請參閱 [記憶體最佳化資料表中的資料表和資料列大小](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)。|不支援|8,060|  
|預存程序之來源文字的位元組數|批次大小或 250 MB 當中較小者|批次大小或 250 MB 當中較小者|  
|每個 `varchar(max)`、`varbinary(max)`、`xml`、`text` 或 `image` 資料行的位元組數|2^31-1|2^31-1|  
|每個 `ntext` 或 `nvarchar(max)` 資料行的字元數|2^30-1|2^30-1|  
|每份資料表的叢集索引數|1|1|  
|GROUP BY、ORDER BY 的資料行|僅受限於位元組數|僅受限於位元組數|  
|GROUP BY WITH CUBE 或 WITH ROLLUP 陳述式中的資料行或運算式|10|10|  
|每個索引鍵的資料行數<br /><br /> 注意： 如果資料表包含一或多個 XML 索引，使用者資料表的叢集索引鍵是限制為 15 個資料行因為 XML 資料行會加入主要 XML 索引的叢集索引鍵。 在  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，您可以在以避免限制最多 16 個索引鍵資料行的非叢集索引包含非索引鍵資料行。 如需詳細資訊，請參閱 [建立內含資料行的索引](../relational-databases/indexes/create-indexes-with-included-columns.md)。|16|16|  
|每個外部索引鍵的資料行數|16|16|  
|每個主索引鍵的資料行數|16|16|  
|每個非寬型資料表的資料行數|1,024|1,024|  
|每個寬型資料表的資料行數|30,000|30,000|  
|每個 SELECT 陳述式的資料行數|4,096|4,096|  
|每個 INSERT 陳述式的資料行數|4096|4096|  
|每個用戶端的連接數目|已設定之連接的最大值|已設定之連接的最大值|  
|資料庫大小|524,272 TB|524,272 TB|  
|每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|32,767|32,767|  
|每個資料庫的檔案群組數|32,767|32,767|  
|記憶體最佳化資料的每個資料庫檔案群組|不支援|1|  
|每個資料庫的檔案數|32,767|32,767|  
|檔案大小 (資料)|16 TB|16 TB|  
|檔案大小 (記錄檔)|2 TB|2 TB|  
|每個資料庫之記憶體最佳化資料的資料檔案|不支援|4.096|  
|記憶體最佳化資料之每個資料檔案的差異檔案|不支援|1|  
|每個資料表的外部索引鍵資料表參考數<br /><br /> 注意： 雖然資料表可以包含無限的數量的 FOREIGN KEY 條件約束，建議的最大值為 253。 根據主控 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的硬體組態而定，指定額外的 FOREIGN KEY 條件約束對於查詢最佳化工具的處理可能會耗費極大成本。|253|253|  
|識別碼長度 (字元數)|128|128|  
|每部電腦的執行個體數|所有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本在獨立伺服器上可支援 50 個執行個體。<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 25 個執行個體在容錯移轉叢集為叢集安裝，使用共用的叢集磁碟做為預存選項時支援[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]支援 50 個執行個體在容錯移轉叢集，如果您選擇 SMB 檔案共用作為您的叢集安裝的儲存體選項如需詳細資訊，請參閱 <<c2> [ 硬體和軟體需求，安裝 SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md)。|單機伺服器為 50 個執行個體。<br /><br /> 當使用共用叢集磁碟做為叢集安裝的預存選項時，在容錯移轉叢集上可支援 25 個執行個體，若您選擇 SMB 檔案共用為叢集安裝的儲存選項， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 則可在容錯移轉叢集上支援 50 個執行個體。|  
|每個記憶體最佳化資料表的索引|不支援|8|  
|包含 SQL 陳述式的字串長度 (批次大小)<br /><br /> 注意： 網路封包大小是用來溝通應用程式與關聯式的表格式資料流 (TDS) 封包大小[!INCLUDE[ssDE](../includes/ssde-md.md)]。 預設封包大小是 4 KB，由 network packet size 組態選項所控制。|65,536 * 網路封包大小|65,536 * 網路封包大小|  
|每個連接的鎖定數|每部伺服器的最大鎖定數|每部伺服器的最大鎖定數|  
|每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]<br /><br /> 注意： 此值是針對靜態鎖定配置。 動態鎖定僅受限於記憶體。|最多為 2,147,483,647|僅受限於記憶體|  
|巢狀預存程序層級<br /><br /> 注意： 如果預存程序存取超過 64 個資料庫或以交錯方式超過 2 的資料庫，您會收到錯誤。|32|32|  
|巢狀子查詢|32|32|  
|巢狀觸發程序層級|32|32|  
|每份資料表的非叢集索引數|999|999|  
|當下列任何一個存在時，GROUP BY 子句內相異運算式的數目：CUBE、ROLLUP、GROUPING SETS、WITH CUBE、WITH ROLLUP|32|32|  
|GROUP BY 子句中由運算子產生的群組集合數目|4,096|4,096|  
|每個預存程序的參數數目|2,100|2,100|  
|每個使用者定義函數的參數數目|2,100|2,100|  
|每份資料表的 REFERENCES|253|253|  
|每份資料表的資料列數|受限於可用的儲存體|受限於可用的儲存體|  
|每個資料庫的資料表數<br /><br /> 注意： 資料庫物件包括資料表、 檢視、 預存程序、 使用者定義函數、 觸發程序、 規則、 預設值和條件約束等物件。 資料庫中所有物件數的總和不得超過 2,147,483,647。|受限於資料庫的物件數|受限於資料庫的物件數|  
|每份分割區資料表或索引的分割區數|1,000<br /><br /> **\*\* 重要\* \*** 建立超過 1,000 個分割區資料表或索引可以在 32 位元系統上，但不是支援。|15,000|  
|非索引資料行的統計資料|30,000|30,000|  
|每個 SELECT 陳述式的資料表數|僅受限於可用的資源|僅受限於可用的資源|  
|每份資料表的觸發程序數<br /><br /> 注意： 資料庫物件包括資料表、 檢視、 預存程序、 使用者定義函數、 觸發程序、 規則、 預設值和條件約束等物件。 資料庫中所有物件數的總和不得超過 2,147,483,647。|受限於資料庫的物件數|受限於資料庫的物件數|  
|每個 UPDATE 陳述式 (寬型資料表) 的資料行數|4096|4096|  
|使用者連線|32,767|32,767|  
|XML 索引|249|249|  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式物件  
 下表指定已經在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式中測試之各種物件的大小和數目上限。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式物件|大小/數目上限[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]（32 位元）|大小/數目上限 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 位元)|  
|----------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式的電腦數 (實體電腦或虛擬機器)|100|100|  
|每部電腦的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體數|5|5|  
|每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體總數|200*|200*|  
|每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的使用者資料庫數，包括資料層應用程式|50|50|  
|每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式的使用者資料庫總數|1,000|1,000|  
|每個資料庫的檔案群組數|1|1|  
|每個檔案群組的資料檔案數|1|1|  
|每個資料庫的記錄檔案數|1|1|  
|每部電腦的磁碟區數|3|3|  
  
 * 的 managed 執行個體的數目上限[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]受到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]公用程式可能會根據伺服器的硬體組態而有所不同。 如需入門資訊，請參閱 [SQL Server 公用程式的功能與工作](../relational-databases/manage/sql-server-utility-features-and-tasks.md)。 並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本都提供 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 公用程式控制點。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
##  <a name="DAC"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料層應用程式物件  
 下表指定已經在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料層應用程式 (DAC) 中測試之各種物件的大小和數目上限。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC 物件|大小/數目上限[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]（32 位元）|大小/數目上限 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 位元)|  
|------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|每個 DAC 的資料庫數|1|1|  
|每個 DAC 的物件數*|受限於資料庫的物件數或可用的記憶體。|受限於資料庫的物件數或可用的記憶體。|  
  
 *此限制所包括的物件類型為使用者、資料表、檢視表、預存程序、使用者定義函數、使用者定義資料類型、資料庫角色、結構描述和使用者定義資料表類型。  
  
##  <a name="Replication"></a> 複寫物件  
 下表指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 複寫中已定義之各種物件的大小和數目上限。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 複寫物件|SQL Server 大小/數目上限 (32 位元)|SQL Server 大小/數目上限 (64 位元)|  
|--------------------------------------------------|---------------------------------------------------|---------------------------------------------------|  
|發行項 (合併式發行集)|256|256|  
|發行項 (快照式或交易式發行集)|32,767|32,767|  
|資料表中的資料行* (合併式發行集)|246|246|  
|資料表中的資料行** ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 快照式或交易式發行集)|1,000|1,000|  
|資料表中的資料行** (Oracle 快照式或交易式發行集)|995|995|  
|用於資料列篩選之資料行的位元組數 (合併式發行集)|1,024|1,024|  
|用於資料列篩選之資料行的位元組數 (快照式或交易式發行集)|8,000|8,000|  
  
 *如果使用資料列追蹤來進行衝突偵測 (預設值)，則基底資料表可包括的資料行行數上限為 1,024，不過，因為必須從發行項篩選資料行，所以發行的資料行行數上限為 246。 如果使用資料行追蹤，則基底資料表可包括的資料行數上限為 246。  
  
 **基底資料表可包含發行集資料庫中允許的最大資料行數 (如果是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，則為 1,024 個)，但如果資料行超出對發行集類型指定的最大值，則必須篩選發行項的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [硬體和 Software Requirements for Installing SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [檢查 System Configuration Checker 的參數](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [SQL Server 公用程式的功能與工作](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
