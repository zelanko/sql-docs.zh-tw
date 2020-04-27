---
title: Oracle 訂閱者 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- data types [SQL Server replication], non-SQL Server Subscribers
- Oracle Subscribers [SQL Server replication]
- non-SQL Server Subscribers, Oracle
- heterogeneous Subscribers, Oracle
- mapping data types [SQL Server replication]
ms.assetid: 591c0313-82ce-4689-9fc1-73752ff122cf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e38cc3a111eb68688fcc9c30ef01bb607349afcb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63022230"
---
# <a name="oracle-subscribers"></a>Oracle 訂閱者
  從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]開始， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 就會透過由 Oracle 提供的 Oracle OLE DB 提供者支援 Oracle 的發送訂閱。  
  
## <a name="configuring-an-oracle-subscriber"></a>設定 Oracle 訂閱者  
 若要設定「Oracle 訂閱者」，請遵循下列步驟：  
  
1.  在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」上安裝並設定 Oracle 用戶端網路軟體及 Oracle OLE DB 提供者，以便「散發者」可與「Oracle 訂閱者」建立連接。 Oracle 用戶端網路軟體應為最新的可用版本。 Oracle 建議使用者安裝最新版本的用戶端軟體。 因此用戶端軟體的版本通常比資料庫軟體的版本還要新。 安裝該軟體最直接的方法是使用 Oracle Client 磁碟上的 Oracle Universal Installer。 在 Oracle Universal Installer 中，您將提供下列資訊：  
  
    |資訊|描述|  
    |-----------------|-----------------|  
    |Oracle Home|這是到 Oracle 軟體之安裝目錄的路徑。 接受預設路徑 (C:\oracle\ora90 或類似路徑) 或輸入其他路徑。 如需有關 Oracle Home 的詳細資訊，請參閱本主題後面的「Oracle Home 的注意事項」。|  
    |Oracle Home 名稱|Oracle Home 路徑的別名。|  
    |安裝類型|在 Oracle 10g 中，選取 **[執行階段]** 或 **[管理員]** 安裝選項。|  
  
2.  為「訂閱者」建立 TNS 名稱。 TNS (Transparent Network Substrate) 是 Oracle 資料庫所使用的通訊層。 TNS Service Name 是 Oracle 資料庫執行個體在網路上使用的名稱。 您可以在為 Oracle 資料庫設定連接時，指派 TNS Service Name。 複寫使用「TNS 服務」名稱來識別「訂閱者」並建立連接。  
  
     Oracle Universal Installer 完成之後，請使用 Net Configuration Assistant 設定網路連接性。 您必須提供四項資訊來設定網路連接性。 Oracle 資料庫管理員會在設定資料庫與接聽程式時設定網路組態，如果您沒有此一資訊，管理員應該能夠提供。 您必須執行下列工作：  
  
    |動作|描述|  
    |------------|-----------------|  
    |識別資料庫|有兩種方法可以識別資料庫。 第一種方法使用 Oracle 系統識別碼 (SID)，每個 Oracle 版本都有。 第二種方法使用服務名稱，從 Oracle 8.0 版開始提供。 這兩種方法都使用在建立資料庫時設定的值，重要的是，用戶端網路組態必須使用相同於管理員在設定資料庫接聽程式時，所使用的命名方法。|  
    |識別資料庫的網路別名|您必須指定一個用於存取 Oracle 資料庫的網路別名。 網路別名實質上是指向在建立資料庫時設定之遠端 SID 或服務名稱的指標；不同的 Oracle 版本與產品中所使用的稱呼各有不同，包括網路服務名稱 (Net Service Name) 和 TNS 別名 (TNS Alias)。 您登入時，SQL*Plus 會提示以「Host String」參數輸入這個別名。|  
    |選取網路通訊協定|選取您要支援的適當通訊協定。 大多數應用程式使用 TCP。|  
    |指定識別資料庫接聽程式的主機資訊|主機是 Oracle 接聽程式所執行之電腦 (通常與資料庫所在的電腦相同) 的名稱或 DNS 別名。 針對某些通訊協定，您必須提供其他的資訊。 例如，您若是選取 TCP，就必須提供接聽程式接聽對目標資料庫之連接要求的通訊埠。 預設 TCP 組態使用通訊埠 1521。|  
  
3.  建立快照集或交易式發行集，並為非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者啟用，然後再為訂閱者建立發送訂閱。 如需相關資訊，請參閱 [為非 SQL Server 訂閱者建立訂閱](../create-a-subscription-for-a-non-sql-server-subscriber.md)。  
  
### <a name="setting-directory-permissions"></a>設定目錄權限  
 必須授與「散發者」端執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務所用之帳戶，對安裝 Oracle 用戶端網路軟體之目錄 (以及所有子目錄) 的讀取和執行權限。  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>測試 SQL Server 散發者與 Oracle 發行者之間的連接性  
 Net Configuration Assistant 執行即將結束時，可能會有一個用於測試到「Oracle 訂閱者」連接的選項。 在您測試連接之前，請確定 Oracle 資料庫執行個體有上線，而且 Oracle 接聽程式正在執行。 如果測試不成功，請連絡負責您想要連接之資料庫的 Oracle DBA (Oracle 資料庫管理員)。  
  
 成功連接到「Oracle 發行者」後，請嘗試使用與設定訂閱之「散發代理程式」時相同的帳戶與密碼登入資料庫。  
  
1.  按一下 **[開始]** ，然後按一下 **[執行]** 。  
  
2.  輸入 `cmd` ，然後按一下 **[確定]** 。  
  
3.  在命令提示字元中，輸入：  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     例如： `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  如果網路組態成功，登入將會成功，您也會看到 `SQL` 提示字元。  
  
### <a name="considerations-for-oracle-home"></a>Oracle Home 的注意事項  
 Oracle 支援應用程式二進位編碼檔案的並存安裝，但是複寫時，一次只能使用一組二進位編碼檔案。 每一個二進位編碼檔案與一個 Oracle Home 相關聯；二進位編碼檔案是在 %ORACLE_HOME%\bin 目錄下。 如果複寫連接到「Oracle 訂閱者」，則您必須確定使用正確的一組二進位編碼檔案 (特別對於最新版本的用戶端網路軟體)。  
  
 利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務使用的帳戶登入散發者，並設定適當的環境變數。 %ORACLE_HOME% 變數應設定為參考您安裝用戶端網路軟體時指定的安裝點。 %PATH% 必須包含 %ORACLE_HOME% \bin 目錄，做為遇到的第一個 Oracle 項目。 如需有關設定環境變數的資訊，請參閱 Windows 文件集。  
  
> [!NOTE]  
>  如果您在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」上有多個 Oracle 首頁，請確定「散發代理程式」使用的是最新版本的 Oracle OLE DB 提供者。 在某些情況下，更新「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」上的用戶端元件時，依預設，Oracle 不會更新 OLE DB 提供者。 請解除安裝舊的 OLE DB 提供者，並安裝最新版本的 OLE DB 提供者。 如需安裝與解除安裝該提供者的詳細資訊，請參閱 Oracle 文件集。  
  
## <a name="considerations-for-oracle-subscribers"></a>Oracle 訂閱者之考量  
 複寫至「Oracle 訂閱者」時，除了要考慮主題＜ [Non-SQL Server Subscribers](non-sql-server-subscribers.md)＞中涵蓋的內容外，還需考慮以下幾個問題：  
  
-   Oracle 將空白字串和 NULL 值均視為 NULL。 您將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料行定義為 NOT NULL，並要將此資料行複寫至「Oracle 訂閱者」時，這一點相當重要。 若要避免將變更套用到「Oracle 訂閱者」時發生錯誤，您必須執行以下操作之一：  
  
    -   請確定空白字串尚未做為資料行值插入已發行的資料表中。  
  
    -   如果通知「散發代理程式」記錄中的錯誤並繼續處理是可接受的，則請使用「散發代理程式」的 **-SkipErrors** 參數。 指定 Oracle 錯誤碼 1400 ( **-SkipErrors1400**)。  
  
    -   修改已產生的建立資料表指令碼，同時從可能包含了與空白字串相關聯的任何字元資料行中移除 NOT NULL 屬性，並且使用 @creation_script sp_addarticle [的](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)參數為發行項提供做為自訂建立指令碼的已修改指令碼。  
  
-   Oracle 訂閱者支援 0x4071 的結構描述選項。 如需結構描述選項的詳細資訊，請參閱 [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。  
  
## <a name="mapping-data-types-from-sql-server-to-oracle"></a>從 SQL Server 到 Oracle 的資料類型對應  
 下表顯示了將資料複寫到執行 Oracle 的「訂閱者」時所使用之資料類型對應。  
  
|SQL Server 資料類型|Oracle 資料類型|  
|--------------------------|----------------------|  
|`bigint`|NUMBER(19,0)|  
|`binary(1-2000)`|RAW(1-2000)|  
|`binary(2001-8000)`|BLOB|  
|`bit`|NUMBER(1)|  
|`char(1-2000)`|CHAR(1-2000)|  
|`char(2001-4000)`|VARCHAR2(2001-4000)|  
|`char(4001-8000)`|CLOB|  
|`date`|日期|  
|`datetime`|日期|  
|`datetime2(0-7)`|適用於 Oracle 9 和 Oracle 10 的 TIMESTAMP(7)；適用於 Oracle 8 的 VARCHAR(27)|  
|`datetimeoffset(0-7)`|適用於 Oracle 9 和 Oracle 10 的 TIMESTAMP(7) WITH TIME ZONE；適用於 Oracle 8 的 VARCHAR(34)|  
|`decimal(1-38, 0-38)`|NUMBER(1-38, 0-38)|  
|`float(53)`|FLOAT|  
|`float`|FLOAT|  
|`geography`|BLOB|  
|`geometry`|BLOB|  
|`hierarchyid`|BLOB|  
|`image`|BLOB|  
|`int`|NUMBER(10,0)|  
|`money`|NUMBER(19,4)|  
|`nchar(1-1000)`|CHAR(1-1000)|  
|`nchar(1001-4000)`|NCLOB|  
|`ntext`|NCLOB|  
|`numeric(1-38, 0-38)`|NUMBER(1-38, 0-38)|  
|`nvarchar(1-1000)`|VARCHAR2(1-2000)|  
|`nvarchar(1001-4000)`|NCLOB|  
|`nvarchar(max)`|NCLOB|  
|`real`|real|  
|`smalldatetime`|日期|  
|`smallint`|NUMBER(5,0)|  
|`smallmoney`|NUMBER(10,4)|  
|`sql_variant`|不適用|  
|`sysname`|VARCHAR2(128)|  
|`text`|CLOB|  
|`time(0-7)`|VARCHAR(16)|  
|`timestamp`|RAW (8)|  
|`tinyint`|NUMBER(3,0)|  
|`uniqueidentifier`|CHAR(38)|  
|`varbinary(1-2000)`|RAW(1-2000)|  
|`varbinary(2001-8000)`|BLOB|  
|`varchar(1-4000)`|VARCHAR2(1-4000)|  
|`varchar(4001-8000)`|CLOB|  
|`varbinary(max)`|BLOB|  
|`varchar(max)`|CLOB|  
|`xml`|NCLOB|  
  
## <a name="see-also"></a>另請參閱  
 [Non-SQL Server Subscribers](non-sql-server-subscribers.md)   
 [Subscribe to Publications](../subscribe-to-publications.md)  
  
  
