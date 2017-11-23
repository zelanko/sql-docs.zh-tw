---
title: "sp_addlinkedserver (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addlinkedserver_TSQL
- sp_addlinkedserver
dev_langs: TSQL
helpviewer_keywords: sp_addlinkedserver
ms.assetid: fed3adb0-4c15-4a1a-8acd-1b184aff558f
caps.latest.revision: "70"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 35173890392c69d6ef6fe40c71b484ae9db3bee3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spaddlinkedserver-transact-sql"></a>sp_addlinkedserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立連結伺服器。 連結的伺服器可讓您對 OLE DB 資料來源存取分散式異質性查詢。 藉由建立連結的伺服器之後**sp_addlinkedserver**、 分散式查詢可對這部伺服器執行。 如果連結的伺服器定義為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體，就可以執行遠端預存程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addlinkedserver [ @server= ] 'server' [ , [ @srvproduct= ] 'product_name' ]   
     [ , [ @provider= ] 'provider_name' ]  
     [ , [ @datasrc= ] 'data_source' ]   
     [ , [ @location= ] 'location' ]   
     [ , [ @provstr= ] 'provider_string' ]   
     [ , [ @catalog= ] 'catalog' ]   
```  
  
## <a name="arguments"></a>引數  
 [  **@server=** ] **'***伺服器***'**  
 這是您要建立的連結伺服器名稱。 *server* 是 **sysname**，沒有預設值。  
  
 [  **@srvproduct=** ] **'***product_name***'**  
 這是要當做連結伺服器加入的 OLE DB 資料來源產品名稱。 *product_name*是**nvarchar (**128**)**，預設值是 NULL。 如果**SQL Server**， *provider_name*， *data_source*，*位置*， *provider_string*，和*目錄*不需要指定。  
  
 [  **@provider=** ] **'***provider_name***'**  
 這是對應於這個資料來源之 OLE DB 提供者的唯一程式化識別碼 (PROGID)。 *provider_name*必須是唯一的安裝目前電腦上指定的 OLE DB 提供者。 *provider_name*是**nvarchar (**128**)**，預設值是 NULL; 但是，如果*provider_name*已省略，就使用 SQLNCLI。 (使用 SQLNCLI 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會重新導向至最新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者)。OLE DB 提供者預期要登錄在登錄中的指定 PROGID。  
  
 [  **@datasrc=** ] **'***data_source***'**  
 這是資料來源的名稱，如 OLE DB 提供者所解譯。 *data_source*是**nvarchar (**4000**)**。 *data_source*被當做 DBPROP_INIT_DATASOURCE 屬性，以初始化 OLE DB 提供者。  
  
 [  **@location=** ] **'***位置***'**  
 這是 OLE DB 提供者解譯的資料庫位置。 *位置*是**nvarchar (**4000**)**，預設值是 NULL。 *位置*作為 DBPROP_INIT_LOCATION 屬性，以初始化 OLE DB 提供者傳遞。  
  
 [  **@provstr=** ] **'***provider_string***'**  
 這是 OLE DB 提供者特定的連接字串，用來識別唯一資料來源。 *provider_string*是**nvarchar (**4000**)**，預設值是 NULL。 *provstr*傳遞至 IDataInitialize，或設定為 DBPROP_INIT_PROVIDERSTRING 屬性以初始化 OLE DB 提供者。  
  
 針對建立連結的伺服器時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，可以使用 「 SERVER 關鍵字做為伺服器指定的執行個體 =*servername*\\*instancename*指定的特定執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 *servername*所在電腦的名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行，並*instancename*是特定執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者連接。  
  
> [!NOTE]  
>  若要存取鏡像資料庫，連接字串必須包含資料庫名稱。 這個名稱是讓資料存取提供者進行容錯移轉嘗試所需的名稱。 中可以指定資料庫 **@provstr** 或 **@catalog** 參數。 此外，連接字串也可以提供容錯移轉夥伴名稱。  
  
 [  **@catalog=** ] **'***目錄***'**  
 這是連接 OLE DB 提供者時所用的目錄。 *目錄*是**sysname**，預設值是 NULL。 *目錄*被當做 DBPROP_INIT_CATALOG 屬性，以初始化 OLE DB 提供者。 當您對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體定義連結伺服器時，目錄會參考連結伺服器所對應的預設資料庫。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 下表所顯示的，是針對可以透過 OLE DB 來存取的資料來源，設定連結伺服器的方法。 您可以對一個特定的資料來源，用一個以上的方法來設定連結伺服器；一個資料來源類型可以有一個以上的資料列。 此資料表也會顯示**sp_addlinkedserver**參數值來設定連結的伺服器。  
  
|遠端 OLE DB 資料來源|OLE DB 提供者|product_name|provider_name|data_source|location|provider_string|catalog|  
|-------------------------------|---------------------|-------------------|--------------------|------------------|--------------|----------------------|-------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<sup>1</sup> （預設值）||||||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者||**SQLNCLI**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的網路名稱 (適用於預設執行個體)|||資料庫名稱 (選擇性)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者||**SQLNCLI**|*servername*\\*instancename* （適用於特定的執行個體）|||資料庫名稱 (選擇性)|  
|Oracle 第 8 版和更新的版本|Oracle OLE DB 提供者|任意|**（oraoledb.oracle)**|Oracle 資料庫的別名||||  
|Access/Jet|Microsoft OLE DB Provider for Jet|任意|**Microsoft.Jet.OLEDB.4.0**|Jet 資料庫檔案的完整路徑||||  
|ODBC 資料來源|Microsoft OLE DB Provider for ODBC|任意|**MSDASQL**|ODBC 資料來源的系統 DSN||||  
|ODBC 資料來源|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for ODBC|任意|**MSDASQL**|||ODBC 連接字串||  
|檔案系統|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Indexing Service|任意|**MSIDXS**|索引服務目錄名稱||||  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 試算表|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet|任意|**Microsoft.Jet.OLEDB.4.0**|Excel 檔的完整路徑||Excel 5.0||  
|IBM DB2 資料庫|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for DB2|任意|**DB2OLEDB**|||請參閱[!INCLUDE[msCoName](../../includes/msconame-md.md)]OLE DB Provider for DB2 文件。|DB2 資料庫的目錄名稱|  
  
 <sup>1</sup>設定連結伺服器的這種方式強制連結伺服器的遠端執行個體的網路名稱相同的名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 使用*data_source*以指定的伺服器。  
  
 <sup>2</sup> 「 任何 」 表示產品名稱可以是任何項目。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者是與搭配使用的提供者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果沒有指定任何提供者名稱，或如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定為產品名稱。 即使您指定較早的提供者名稱 SQLOLEDB，它也會在保存到目錄時，改為 SQLNCLI。  
  
 *Data_source*，*位置*， *provider_string*，和*目錄*參數會識別資料庫或資料庫的連結伺服器所指向。 如果這些參數有任何一個是 NULL，就不會設定對應的 OLE DB 初始化屬性。  
  
 在群集環境中，當您指定讓檔名指向 OLE DB 資料來源時，請使用通用命名慣例名稱 (UNC) 或共用磁碟機來指定位置。  
  
 **sp_addlinkedserver**無法在使用者自訂交易內執行。  
  
> [!IMPORTANT]  
>  藉由建立連結的伺服器時**sp_addlinkedserver**，預設的自我對應加入所有本機登入。 如果是非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入也許可以利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶，取得該提供者的存取權。 管理員應該考慮使用 `sp_droplinkedsrvlogin <linkedserver_name>, NULL` 來移除全域對應。  
  
## <a name="permissions"></a>Permissions  
 `sp_addlinkedserver`陳述式需要`ALTER ANY LINKED SERVER`權限。 (SSMS**新增連結的伺服器**對話方塊需要的成員資格的方式實作`sysadmin`固定的伺服器角色。)  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-microsoft-sql-server-native-client-ole-db-provider"></a>A. 使用 Microsoft SQL Server Native Client OLE DB Provider  
 下列範例會建立一個名為 `SEATTLESales` 的連結伺服器。 產品名稱是 `SQL Server`，另外，不使用任何提供者名稱。  
  
```  
USE master;  
GO  
EXEC sp_addlinkedserver   
   N'SEATTLESales',  
   N'SQL Server';  
GO  
```  
  
 下列範例會建立連結的伺服器`S1_instance1`的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。  
  
```  
EXEC sp_addlinkedserver     
   @server=N'S1_instance1',   
   @srvproduct=N'',  
   @provider=N'SQLNCLI',   
   @datasrc=N'S1\instance1';  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-microsoft-access"></a>B. 使用 Microsoft OLE DB Provider for Microsoft Access  
 Microsoft.Jet.OLEDB.4.0 提供者會連接到使用 2002-2003 格式的 Microsoft Access 資料庫。 下列範例會建立一個名為 `SEATTLE Mktg` 的連結伺服器。  
  
> [!NOTE]  
>  這個範例假設這兩個[!INCLUDE[msCoName](../../includes/msconame-md.md)]Access 和範例**Northwind**資料庫皆已安裝且**Northwind**資料庫位於 C:\Msoffice\Access\Samples。  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.Jet.OLEDB.4.0',   
   @srvproduct = N'OLE DB Provider for Jet',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.mdb';  
GO  
```  
  
 Microsoft.ACE.OLEDB.12.0 提供者會連接到使用 2007 格式的 Microsoft Access 資料庫。 下列範例會建立一個名為 `SEATTLE Mktg` 的連結伺服器。  
  
> [!NOTE]  
>  這個範例假設這兩個[!INCLUDE[msCoName](../../includes/msconame-md.md)]Access 和範例**Northwind**資料庫皆已安裝且**Northwind**資料庫位於 C:\Msoffice\Access\Samples。  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.ACE.OLEDB.12.0',   
   @srvproduct = N'OLE DB Provider for ACE',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.accdb';  
GO  
```  
  
### <a name="c-using-the-microsoft-ole-db-provider-for-odbc-with-the-datasource-parameter"></a>C. 搭配 data_source 參數來使用 Microsoft OLE DB Provider for ODBC  
 下列範例會建立名為的連結的伺服器`SEATTLE Payroll`使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]OLE DB Provider for ODBC (`MSDASQL`) 和*data_source*參數。  
  
> [!NOTE]  
>  您必須先在伺服器中，將指定的 ODBC 資料來源名稱定義為系統 DSN，才可以使用該連結伺服器。  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Payroll',   
   @srvproduct = N'',  
   @provider = N'MSDASQL',   
   @datasrc = N'LocalServer';  
GO  
```  
  
### <a name="d-using-the-microsoft-ole-db-provider-for-excel-spreadsheet"></a>D. 使用適用於 Excel 試算表的 Microsoft OLE DB Provider  
 若要建立連結的伺服器定義使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]OLE DB Provider for Jet 來存取 1997年-2003年格式的 Excel 試算表第一次的具名的範圍在 Excel 中建立指定資料行和資料列，以選取的 Excel 工作表。 然後才能在分散式查詢中，將該範圍的名稱參考為資料表名稱。  
  
```  
EXEC sp_addlinkedserver 'ExcelSource',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   'c:\MyData\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
GO  
```  
  
 若要存取 Excel 試算表中的資料，請建立資料格範圍與某個名稱的關聯性。 您可以利用先前設定的連結伺服器，以下列查詢存取當做資料表使用的指定具名範圍 `SalesData`。  
  
```  
SELECT *  
   FROM ExcelSource...SalesData;  
GO  
```  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是以一個有權存取遠端共用區的網域帳戶來執行，即可改用 UNC 路徑來取代對應的磁碟機。  
  
```  
EXEC sp_addlinkedserver 'ExcelShare',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   '\\MyServer\MyShare\Spreadsheets\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
```  
  
 若要連接到 Excel 2007 格式的 Excel 試算表，請使用 ACE 提供者。  
  
```  
EXEC sp_addlinkedserver @server = N'ExcelDataSource',   
@srvproduct=N'ExcelData', @provider=N'Microsoft.ACE.OLEDB.12.0',   
@datasrc=N'C:\DataFolder\People.xlsx',  
@provstr=N'EXCEL 12.0' ;  
  
```  
  
### <a name="e-using-the-microsoft-ole-db-provider-for-jet-to-access-a-text-file"></a>E. 使用 Microsoft OLE DB Provider for Jet 來存取文字檔  
 下列範例會建立一個連結伺服器，直接存取文字檔，而不將這些檔案當做 Access .mdb 檔中的資料表加以連結。 提供者是 `Microsoft.Jet.OLEDB.4.0`，而提供者字串是 `Text`。  
  
 資料來源是包含這些文字檔之目錄的完整路徑。 描述文字檔結構的 schema.ini 檔，必須與文字檔置於同一個目錄下。 如需有關如何建立 Schema.ini 檔的詳細資訊，請參閱 Jet Database Engine 文件集。  
  
```  
--Create a linked server.  
EXEC sp_addlinkedserver txtsrv, N'Jet 4.0',   
   N'Microsoft.Jet.OLEDB.4.0',  
   N'c:\data\distqry',  
   NULL,  
   N'Text';  
GO  
  
--Set up login mappings.  
EXEC sp_addlinkedsrvlogin txtsrv, FALSE, Admin, NULL;  
GO  
  
--List the tables in the linked server.  
EXEC sp_tables_ex txtsrv;  
GO  
  
--Query one of the tables: file1#txt  
--using a four-part name.   
SELECT *   
FROM txtsrv...[file1#txt];  
```  
  
### <a name="f-using-the-microsoft-ole-db-provider-for-db2"></a>F. 使用 Microsoft OLE DB Provider for DB2  
 下列範例會建立一個名叫 `DB2` 的連結伺服器，該連結伺服器是使用 `Microsoft OLE DB Provider for DB2`。  
  
```  
EXEC sp_addlinkedserver  
   @server=N'DB2',  
   @srvproduct=N'Microsoft OLE DB Provider for DB2',  
   @catalog=N'DB2',  
   @provider=N'DB2OLEDB',  
   @provstr=N'Initial Catalog=PUBS;  
       Data Source=DB2;  
       HostCCSID=1252;  
       Network Address=XYZ;  
       Network Port=50000;  
       Package Collection=admin;  
       Default Schema=admin;';  
```  
  
### <a name="g-add-a-includesssdsfullincludessssdsfull-mdmd-as-a-linked-server-for-use-with-distributed-queries-on-cloud-and-on-premise-databases"></a>G. 加入 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]成為連結伺服器以搭配跨雲端和內部部署資料庫的分散式查詢使用  
 您可以加入 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]成為連結伺服器，再將其搭配跨內部部署和雲端資料庫的分散式查詢使用。 這是跨內部部署企業網路和 Windows Azure 雲端的資料庫混合式方案的一項元件。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 盒裝產品包含分散式查詢功能，可讓您撰寫查詢將本機資料來源的資料與遠端資料來源的資料 (包括非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的資料) 結合，定義成連結伺服器。 您將能加入每個 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (虛擬 master 除外) 成為個別的連結伺服器，然後直接供您的資料庫應用程式使用，與任何其他資料庫無異。  
  
 使用 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]的好處包括管理能力、高可用性、延展性、有您熟悉的開發模型和關聯式資料模型。 您的資料庫應用程式的需求決定了該如何在雲端使用 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 您可以一次將所有資料移到 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，或是逐漸搬移部分資料並將其餘資料留在內部部署環境。 藉著這類混合式資料庫應用程式，如今您可以加入 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]成為連結伺服器，而且資料庫應用程式可以發出分散式查詢，將 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]與內部部署資料來源的資料結合。  
  
 以下是說明如何使用分散式查詢連接到 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]的簡單範例：  
  
```  
------ Configure the linked server  
-- Add one Windows Azure SQL DB as Linked Server  
EXEC sp_addlinkedserver  
@server='myLinkedServer', -- here you can specify the name of the linked server  
@srvproduct='',       
@provider='sqlncli', -- using SQL Server Native Client  
@datasrc='myServer.database.windows.net',   -- add here your server name  
@location='',  
@provstr='',  
@catalog='myDatabase'  -- add here your database name as initial catalog (you cannot connect to the master database)  
-- Add credentials and options to this linked server  
EXEC sp_addlinkedsrvlogin  
@rmtsrvname = 'myLinkedServer',  
@useself = 'false',  
@rmtuser = 'myLogin',             -- add here your login on Azure DB  
@rmtpassword = 'myPassword' -- add here your password on Azure DB  
EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;  
------ Now you can use the linked server to execute 4-part queries  
-- You can create a new table in the Azure DB  
exec ('CREATE TABLE t1tutut2(col1 int not null CONSTRAINT PK_col1 PRIMARY KEY CLUSTERED (col1) )') at myLinkedServer  
-- Insert data from your local SQL Server  
exec ('INSERT INTO t1tutut2 VALUES(1),(2),(3)') at myLinkedServer  
  
-- Query the data using 4-part names  
select * from myLinkedServer.myDatabase.dbo.myTable  
```  
  
## <a name="see-also"></a>請參閱＜  
 [分散式的查詢預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropserver &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_serveroption &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [sp_setnetname &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setnetname-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [系統資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
