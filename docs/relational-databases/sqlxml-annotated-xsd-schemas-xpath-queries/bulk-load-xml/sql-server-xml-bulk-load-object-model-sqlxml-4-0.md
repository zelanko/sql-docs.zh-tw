---
title: 'SQL Server XML 大量載入物件模型 (SQLXML) '
description: 瞭解 Sqlxmlbulkload.sqlxmlbulkload.4.0 物件的方法和屬性，此物件是用來在 SQLXML 4.0 中大量載入 XML。
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], object model
- ErrorLogFile property
- SGDropTables property
- SGUseID property
- KeepNulls property
- ConnectionCommand property
- SchemaGen property
- XMLFragment property
- SQLXMLBulkLoad object
- ForceTableLock property
- CheckConstraints property
- BulkLoad property
- TempFilePath property
- IgnoreDuplicateKeys property
- Transaction property
- KeepIdentity property
- ConnectionString property
- FireTriggers property
- Execute method
- XML Bulk Load [SQLXML], object model
ms.assetid: a9efbbde-ed2b-4929-acc1-261acaaed19d
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bc5414ba64ec7a801cf279a4735a2f8e85cd3731
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461729"
---
# <a name="sql-server-xml-bulk-load-object-model-sqlxml-40"></a>SQL Server XML 大量載入物件模型 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 大量載入物件模型包含 sqlxmlbulkload.sqlxmlbulkload.4.0 物件。 這個物件支援下列方法和屬性。  
  
## <a name="methods"></a>方法  
 執行  
 使用當做參數提供的結構描述檔案和資料檔案 (或資料流) 大量載入資料。  
  
## <a name="properties"></a>屬性  
 大量載入  
 指定是否應該執行大量載入。 如果您只想要產生架構 (查看遵循) 且不執行大量載入的 SchemaGen、SGDropTables 和 SGUseID 屬性，此屬性會很有用。 這是布林屬性。 當屬性設定為 TRUE 時，XML 大量載入會執行。 設定為 FALSE 時，XML 大量載入則不會執行。  
  
 預設值為 TRUE。  
  
 CheckConstraints  
 指定當 XML 大量載入將資料插入資料行時，是否要檢查在資料行上指定的條件約束 (例如，由於資料行間之主索引鍵/外部索引鍵關聯性緣故的條件約束)。 這是布林屬性。  
  
 當屬性設定為 TRUE 時，XML 大量載入會檢查插入之每個值的條件約束 (也就是說，條件約束違規會導致錯誤)。  
  
> [!NOTE]  
>  若要將此屬性保留為 FALSE，您必須擁有目標資料表的 **ALTER TABLE** 許可權。 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)。  
  
 預設值為 FALSE。 設定為 FALSE 時，XML 大量載入會在插入作業期間忽略條件約束。 在目前的實作中，您必須以對應結構描述中，主索引鍵和外部索引鍵關聯性的順序定義資料表。 也就是說，具有主索引鍵的資料表必須在具有外部索引鍵的對應資料表之前定義，否則，XML 大量載入會失敗。  
  
 請注意，如果識別碼擴展即將完成，則此選項不會套用，而且條件約束檢查將會保持開啟。 如果 `KeepIdentity=False`，而且有定義一個關聯性，其中父系是識別欄位，並在產生值時將其提供給子系，則會發生這個狀況。  
  
 ConnectionCommand  
 識別現有的連線物件 (例如，XML 大量載入應使用的 ADO 或 ICommand 命令物件) 。 您可以使用 ConnectionCommand 屬性，而不是使用 ConnectionString 屬性指定連接字串。 如果您使用 ConnectionCommand，則 Transaction 屬性必須設定為 TRUE。  
  
 如果您同時使用 ConnectionString 和 ConnectionCommand 屬性，XML 大量載入會使用最後指定的屬性。  
  
 預設值是 NULL。  
  
 ConnectionString  
 識別 OLE DB 連接字串，提供必要的資訊來建立資料庫執行個體的連接。 如果您同時使用 ConnectionString 和 ConnectionCommand 屬性，XML 大量載入會使用最後指定的屬性。  
  
 預設值是 NULL。  
  
 ErrorLogFile  
 指定 XML 大量載入記錄錯誤和訊息所在的檔案名稱。 預設為空字串，在此情況下，沒有做任何記錄。  
  
 FireTriggers  
 指定在目標資料表上定義的觸發程序是否應該在大量載入作業期間引發。 預設值為 FALSE。  
  
 設定為 TRUE 時，觸發程序一般將會在插入作業期間引發。  
  
> [!NOTE]  
>  若要將此屬性保留為 FALSE，您必須擁有目標資料表的 **ALTER TABLE** 許可權。 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)。  
  
 請注意，如果識別碼擴展即將完成，則此選項不會套用，而且觸發條件將會保持開啟。 如果 `KeepIdentity=False`，而且有定義一個關聯性，其中父系是識別欄位，並在產生值時將其提供給子系，則會發生這個狀況。  
  
 ForceTableLock  
 指定 XML 大量載入複製資料的目標資料表是否應該在大量載入期間鎖定。 這是布林屬性。 當屬性設定為 TRUE 時，XML 大量載入會取得大量載入期間的資料表鎖定。 設定為 FALSE 時，XML 大量載入會在每次將記錄插入資料表時取得資料表鎖定。  
  
 預設值為 FALSE。  
  
 IgnoreDuplicateKeys  
 指定嘗試在索引鍵資料行中插入重複的值時該怎麼辦。 如果此屬性設定為 TRUE，而且嘗試在索引鍵資料行中插入具有重複值的記錄，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會插入該記錄。 但是它會插入後續的記錄，因此，大量載入作業不會失敗。 如果此屬性設定為 FALSE，嘗試在索引鍵資料行中插入重複的值時，大量載入會失敗。  
  
 當 IgnoreDuplicateKeys 屬性設定為 TRUE 時，會針對資料表中插入的每個記錄發出 COMMIT 語句。 這會讓效能減慢。 只有當 Transaction 屬性設為 FALSE 時，才可以將屬性設定為 TRUE，因為交易行為是使用檔案來執行。  
  
 預設值為 FALSE。  
  
 KeepIdentity  
 指定如何處理來源檔案中識別類型資料行的值。 這是布林屬性。 當屬性設定為 TRUE 時，XML 大量載入會將來源檔案中指定的值指派給識別資料行。 當屬性設定為 FALSE 時，大量載入作業會忽略來源檔案中指定的識別資料行值。 在此情況下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會指派值給識別資料行。  
  
 如果大量載入包含的資料行是參考儲存 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 產生之值所在識別資料行的外部索引鍵，大量載入就會將這些識別值適當地擴展到外部索引鍵資料行。  
  
 此屬性的值會套用到大量載入包含的所有資料行。 預設值為 TRUE。  
  
> [!NOTE]  
>  若要將此屬性保留為 TRUE，您必須擁有目標資料表的 **ALTER TABLE** 許可權。 否則，它必須設定為值 FALSE。 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)。  
  
 KeepNulls  
 指定在 XML 文件中，用於缺少對應屬性或子元素之資料行的值。 這是布林屬性。 當屬性設定為 TRUE 時，XML 大量載入會將 Null 值指派給資料行。 它不會將資料行的預設值指派為伺服器上的值 (如果有的話)。 此屬性的值會套用到大量載入包含的所有資料行。  
  
 預設值為 FALSE。  
  
 SchemaGen  
 指定是否要在執行大量載入作業前，建立所需的資料表。 這是布林屬性。 如果此屬性設定為 TRUE，會建立對應結構描述中所識別的資料表 (資料庫必須存在)。 如果有一或多個資料表已經存在於資料庫中，SGDropTables 屬性會決定是否要卸載和重新建立這些預先存在的資料表。  
  
 SchemaGen 屬性的預設值為 FALSE。 SchemaGen 不會在新建立的資料表上建立 PRIMARY KEY 條件約束。 不過，SchemaGen 會在資料庫中建立外鍵條件約束，如果它可以在對應架構中找到相符的 **sql： relationship** 和 **sql：索引鍵欄位** 注釋，而且索引鍵欄位是由單一資料行組成。  
  
 請注意，如果您將 SchemaGen 屬性設定為 TRUE，XML 大量載入會執行下列動作：  
  
-   從元素和屬性名稱建立所需的資料表。 因此，您最好不要將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 保留字用於結構描述中的元素和屬性名稱。  
  
-   以[xml 資料類型](../../../t-sql/xml/xml-transact-sql.md)格式，傳回任何使用[sql：溢位欄位](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)指定之資料行的溢位資料。  
  
 SGDropTables  
 指定應該卸除或重新建立現有的資料表。 當 SchemaGen 屬性設定為 TRUE 時，您可以使用這個屬性。 如果 SGDropTables 為 FALSE，則會保留現有的資料表。 當此屬性為 TRUE 時，會刪除並重新建立現有的資料表。  
  
 預設值為 FALSE。  
  
 SGUseID  
 指定當建立資料表時，是否可以在建立 PRIMARY KEY 條件約束時，使用識別為 **識別碼** 類型之對應架構中的屬性。 當 SchemaGen 屬性設定為 TRUE 時，請使用此屬性。 如果 SGUseID 為 TRUE，SchemaGen 公用程式會使用屬性，其 **dt： type = "id"** 已指定為 primary key 資料行，並在建立資料表時加入適當的 primary key 條件約束。  
  
 預設值為 FALSE。  
  
 TempFilePath  
 針對交易的大量載入，指定 XML 大量載入建立暫存檔案所在的檔案路徑   (此屬性只有在 Transaction 屬性設定為 TRUE 時才有用。 ) 您必須確定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用於 XML 大量載入的帳戶可以存取此路徑。 如果未設定此屬性，XML 大量載入會將暫存檔案儲存在 TEMP 環境變數中所指定的位置。  
  
 交易  
 指定大量載入是否應該當做交易完成，在此情況下，保證會在大量載入失敗時回復。 這是布林屬性。 如果屬性設定為 TRUE，大量載入會在交易內容中發生。 只有當交易設定為 TRUE 時，TempFilePath 屬性才有用。  
  
> [!NOTE]  
>  如果您要將二進位資料 (例如，將 bin. hex、bin、base64 XML 資料類型載入二進位檔、影像 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型) ，則 Transaction 屬性必須設定為 FALSE。  
  
 預設值為 FALSE。  
  
 XMLFragment  
 指定來源資料是否為 XML 片段。 XML 片段是沒有單一、最上層 (根) 元素的 XML 文件。 這是布林屬性。 如果來源檔案由 XML 片段所組成，此屬性必須設定為 TRUE。  
  
 預設值為 FALSE。  
  
  
