---
description: IBM DB2 訂閱者
title: IBM DB2 訂閱者 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- non-SQL Server Subscribers, IBM DB2
- data types [SQL Server replication], non-SQL Server Subscribers
- IBM DB2 Subscribers
- mapping data types [SQL Server replication]
- heterogeneous Subscribers, IBM DB2
ms.assetid: a1a27b1e-45dd-4d7d-b6c0-2b608ed175f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e044fa0e368893f0aaa1fe8175b306c2fc04c24b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88327064"
---
# <a name="ibm-db2-subscribers"></a>IBM DB2 訂閱者
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  透過[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Host Integration Server 所含的 OLE DB 提供者， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 支援向 IBM DB2/AS 400、DB2/MVS 和 DB2/Universal Database 的提取訂閱。  
  
## <a name="configuring-an-ibm-db2-subscriber"></a>設定 IBM DB2 訂閱者  
 若要設定「IBM DB2 訂閱者」，請遵循下列步驟：  
  
1.  在散發者上安裝 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for DB2 的最新版本：  
  
    -   如果您使用的是 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Enterprise Edition，請在 [SQL Server 下載](https://go.microsoft.com/fwlink/?LinkId=149256)網頁的 [Related Downloads] \(相關下載) 區段中，按一下最新版 Microsoft SQL Server 功能套件的連結。**** 在 **Microsoft SQL Server 功能套件**網頁上，搜尋 **Microsoft OLE DB Provider for DB2**。  
  
    -   如果您使用的是 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Standard Edition，請安裝 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] (HIS) 伺服器的最新版本，其中就包含此提供者。  
  
     除了安裝提供者外，建議您同時安裝「資料存取工具」，該工具將在下一步中用到 (根據預設，它會隨 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Enterprise Edition 的下載一起安裝)。 如需有關安裝和使用「資料存取工具」的詳細資料，請參閱提供者文件集或 HIS 文件集。  
  
2.  為「訂閱者」建立連接字串。 在任何文字編輯器中都可建立連接字串，但建議您使用「資料存取工具」。 若要在「資料存取工具」中建立字串：  
  
    1.  依序按一下 **[開始]**、 **[程式集]** 和 **[DB2 的 Microsoft OLE DB 提供者]**，然後再按 **[資料存取工具]**。  
  
    2.  遵循 **[資料存取工具]** 中的步驟提供有關 DB2 伺服器的資訊。 完成工具後，將建立通用資料連結 (UDL) 和相關聯的連接字串 (複寫實際不會使用 UDL，但會用到連接字串)。  
  
    3.  存取連接字串：以滑鼠右鍵按一下「資料存取工具」中的 UDL，然後選取 **[顯示連接字串]**。  
  
     連接字串類似於 (使用分行符號是為提高可讀性)：  
  
    ```  
    Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
    PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
    Default Schema=MY_SCHEMA;Process Binary as Character=False;Derive Parameters=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
    Persist Security Info=False;Connection Pooling=True;  
    ```  
  
     字串中的大多數選項都是您設定之 DB2 伺服器的專用選項，但 `Process Binary as Character` 和 `Derive Parameters` 選項應一律設定為 `False`。 需要為 `Initial Catalog` 選項指定值，以便識別訂閱資料庫。 在您建立訂閱時，將在「新增訂閱精靈」中輸入連接字串。  
  
3.  建立快照集或交易式發行集，並為非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者啟用，然後再為訂閱者建立發送訂閱。 如需相關資訊，請參閱 [為非 SQL Server 訂閱者建立訂閱](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)。  
  
4.  可以選擇為一或多個發行項指定自訂建立指令碼。 發行資料表時，將為該資料表建立一個 `CREATE TABLE` 指令碼。 對於非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者，指令碼將以 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 用語建立，然後在套用到訂閱者端之前，透過散發代理程式將其翻譯為比較一般的 SQL 用語。 若要指定自訂的建立指令碼，請修改現有的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼或建立使用 DB2 SQL 用語的完整指令碼；如果已建立 DB2 指令碼，請使用 **bypass_translation** 指示詞，好讓散發代理程式無需進行翻譯便可在訂閱者端套用指令碼。  
  
     有多種情況下會需要修改指令碼，但最常見的原因是改變資料類型對應。 如需詳細資訊，請參閱本主題中的＜資料類型對應考量＞一節。 如果您修改 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼，請將變更限制為資料類型對應變更 (且指令碼不應包含任何註解)。 如果需要作大量變更，請建立 DB2 指令碼。  
  
     **若要修改發行項指令碼並做為自訂建立指令碼提供**  
  
    1.  為發行集產生快照集後，瀏覽至發行集的快照集資料夾。  
  
    2.  找到與發行項名稱相同的 `.sch` 檔案，例如 `MyArticle.sch`。  
  
    3.  使用 [記事本] 或其他文字編輯器開啟此檔案。  
  
    4.  修改檔案並將其儲存至其他目錄。  
  
    5.  執行 `sp_changearticle`，並指定 *creation_script* 屬性的檔案路徑與名稱。 如需詳細資訊，請參閱 [sp_changearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)。  
  
     **若要建立發行項指令碼並做為自訂建立指令碼提供**  
  
    1.  使用 DB2 SQL 用語建立發行項指令碼。 確定檔案的第一行為 **bypass_translation**，且該行上除此之外無其他內容。  
  
    2.  執行 sp_changearticle，並指定 *creation_script* 屬性的檔案路徑與名稱。  
  
## <a name="considerations-for-ibm-db2-subscribers"></a>IBM DB2 訂閱者考量  
 複寫至「DB2 訂閱者」時，除了＜ [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)＞主題中涵蓋的考量外，還需考慮以下幾個問題：  
  
-   每個已複寫資料表的資料與索引將指定給 DB2 資料表空間。 DB2 資料表空間的頁面大小，控制資料表空間所屬資料表的最大資料行行數以及最大資料列大小。 根據複寫的資料行數與資料表的最大資料列大小，確定與複寫資料表相關聯的資料表空間是否適當。  
  
-   如果資料表中一或多個主索引鍵資料行的資料類型為 DECIMAL(32-38, 0-38) 或 NUMERIC(32-38, 0-38)，則不要使用異動複寫將資料表發行至「DB2 訂閱者」。 異動複寫使用主索引鍵識別資料列；這可能會導致失敗，因為這些資料類型對應至「訂閱者」端的 VARCHAR(41)。 含有可使用這些資料類型之主索引鍵的資料表可以使用快照式複寫加以發行。  
  
-   如果您要在「訂閱者」端預先建立資料表，請不要由複寫來建立，而是使用僅支援複寫選項。 如需詳細資訊，請參閱 [不使用快照集初始化交易式訂閱](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
-   相對於 DB2，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 允許使用更長的資料表名稱和資料行名稱：  
  
    -   如果發行集資料庫中的資料表名稱比「訂閱者」端 DB2 版本支援的資料表名稱長，請為 destination_table 發行項屬性指定替代名稱。 如需在建立發行集時設定屬性的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)和[定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    -   不可能指定替代資料行名稱。 您必須確定已發行資料表中的資料行名稱比「訂閱者」端 DB2 版本支援的那些資料行名稱短。  
  
## <a name="mapping-data-types-from-sql-server-to-ibm-db2"></a>從 SQL Server 到 IBM DB2 的資料類型對應  
 下表顯示了將資料複寫到執行 IBM DB2 的「訂閱者」時所使用的資料類型對應。  
  
|SQL Server 資料類型|IBM DB2 資料類型|  
|--------------------------|-----------------------|  
|**bigint**|DECIMAL(19,0)|  
|**binary(1-254)**|CHAR(1-254) FOR BIT DATA|  
|**binary(255-8000)**|VARCHAR(255-8000) FOR BIT DATA|  
|**bit**|SMALLINT|  
|**CHAR(1-254)**|CHAR(1-254)|  
|**char(255-8000)**|VARCHAR(255-8000)|  
|**date**|日期|  
|**datetime**|timestamp|  
|**datetime2(0-7)**|VARCHAR(27)|  
|**datetimeoffset(0-7)**|VARCHAR(34)|  
|**decimal(1-31, 0-31)**|DECIMAL(1-31, 0-31)|  
|**decimal(32-38, 0-38)**|VARCHAR(41)|  
|**float(53)**|DOUBLE|  
|**float**|FLOAT|  
|**地理位置**|IMAGE|  
|**幾何**|IMAGE|  
|**hierarchyid**|IMAGE|  
|**image**|VARCHAR(0) FOR BIT DATA*|  
|**into**|INT|  
|**money**|DECIMAL(19,4)|  
|**nchar(1-4000)**|VARCHAR(1-4000)|  
|**ntext**|VARCHAR(0)*|  
|**numeric(1-31, 0-31)**|DECIMAL(1-31,0-31)|  
|**numeric(32-38, 0-38)**|VARCHAR(41)|  
|**nvarchar(1-4000)**|VARCHAR(1-4000)|  
|**nvarchar(max)**|VARCHAR(0)*|  
|**real**|REAL|  
|**smalldatetime**|timestamp|  
|**smallint**|SMALLINT|  
|**smallmoney**|DECIMAL(10,4)|  
|**sql_variant**|N/A|  
|**sysname**|VARCHAR(128)|  
|**text**|VARCHAR(0)*|  
|**time(0-7)**|VARCHAR(16)|  
|**timestamp**|CHAR(8) FOR BIT DATA|  
|**tinyint**|SMALLINT|  
|**uniqueidentifier**|CHAR(38)|  
|**varbinary(1-8000)**|VARCHAR(1-8000) FOR BIT DATA|  
|**varchar(1-8000)**|VARCHAR(1-8000)|  
|**varbinary(max)**|VARCHAR(0) FOR BIT DATA*|  
|**varchar(max)**|VARCHAR(0)*|  
|**xml**|VARCHAR(0)*|  
  
* 如需與 VARCHAR(0) 之對應的詳細資訊，請參閱下節。  
  
### <a name="data-type-mapping-considerations"></a>資料類型對應考量  
 複寫至「DB2 訂閱者」時，請考慮下列資料類型對應問題：  
  
-   在將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**、**varchar**、**binary** 和 **varbinary** 分別對應至 DB2 CHAR、VARCHAR、CHAR FOR BIT DATA 及 VARCHAR FOR BIT DATA 時，複寫會將 DB2 資料類型長度設定為與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 類型的長度相同。  
  
     這可使產生的資料表在「訂閱者」端成功建立，只要 DB2 頁面大小條件約束足以容納資料列的大小上限。 確定用於存取 DB2 資料庫的登入，有權限存取擁有足夠大小以容納正複寫至 DB2 之資料表的資料表空間。  
  
-   DB2 可以支援最大 32 千位元組 (KB) 的 VARCHAR 資料行，因此可以將某些 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大型物件資料行正確對應至 DB2 VARCHAR 資料行。 但是，複寫用於 DB2 的 OLE DB 提供者不支援將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大型物件對應至 DB2 大型物件。 因此，在產生的建立指令碼中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **text**、**varchar(max)**、**ntext** 和 **nvarchar(max)** 資料行將對應至 VARCHAR(0)。 長度值 0 必須在將指令碼套用至「訂閱者」之前變更為適當值。 如果資料類型長度未變更，則嘗試在「DB2 訂閱者」端建立資料表時，DB2 將產生錯誤 604 (表示資料類型的有效位數或長度屬性無效)。  
  
     根據您對要複寫之來源資料表的了解，判斷是否適合將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大型物件對應至可變長度的 DB2 項目，並在自訂建立指令碼中指定適當的最大長度。 如需有關指定自訂建立指令碼的資訊，請參閱本主題中＜設定 IBM DB2 訂閱者＞一節中的步驟 5。  
  
    > [!NOTE]  
    >  指定的 DB2 類型長度與其他資料行長度的組合，不得超過由資料表資料指派到的 DB2 資料表空間確定之最大資料列大小。  
  
     如果大型物件資料行沒有適當的對應，請考慮在發行項上使用資料行篩選，以便不複寫資料行。 如需詳細資訊，請參閱[篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
-   在將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **nchar** 和 **nvarchar** 複寫至 DB2 CHAR 和 VARCHAR 時，複寫對 DB2 類型與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 類型使用相同的長度規範。 但是，資料類型長度對於產生的 DB2 資料表可能太小。  
  
     在某些 DB2 環境中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char** 資料項目未限制為單一位元組字元；CHAR 或 VARCHAR 項目的長度必須將此納入考量。 如果需要 *shift in* 和 *shift out* 字元，您還必須考慮到它們。 如果您要複寫含有 **nchar** 和 **nvarchar** 資料行的資料表，可能需要為自訂建立指令碼中的資料類型指定較大的最大長度。 如需有關指定自訂建立指令碼的資訊，請參閱本主題中＜設定 IBM DB2 訂閱者＞一節中的步驟 5。  
  
## <a name="see-also"></a>另請參閱  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
