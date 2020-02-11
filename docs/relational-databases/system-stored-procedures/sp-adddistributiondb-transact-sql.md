---
title: sp_adddistributiondb （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 04/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistributiondb_TSQL
- sp_adddistributiondb
helpviewer_keywords:
- sp_adddistributiondb
ms.assetid: e9bad56c-d2b3-44ba-a4d7-ff2fd842e32d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ef595adcf3772dcac92c58764d99bca4374aeb0a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771347"
---
# <a name="sp_adddistributiondb-transact-sql"></a>sp_adddistributiondb (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  建立新的散發資料庫並安裝散發者結構描述。 散發資料庫會儲存複寫所用的預存程序、結構描述和中繼資料。 這個預存程序執行於 master 資料庫的散發者端，以便建立散發資料庫，它會安裝必要的資料表以及啟用複寫散發時所需要的預存程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_adddistributiondb [ @database= ] 'database'   
    [ , [ @data_folder= ] 'data_folder' ]   
    [ , [ @data_file= ] 'data_file' ]   
    [ , [ @data_file_size= ] data_file_size ]   
    [ , [ @log_folder= ] 'log_folder' ]   
    [ , [ @log_file= ] 'log_file' ]   
    [ , [ @log_file_size= ] log_file_size ]   
    [ , [ @min_distretention= ] min_distretention ]   
    [ , [ @max_distretention= ] max_distretention ]   
    [ , [ @history_retention= ] history_retention ]   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @createmode= ] createmode ]  
    [ , [ @from_scripting = ] from_scripting ] 
    [ , [ @deletebatchsize_xact = ] deletebatchsize_xact ] 
    [ , [ @deletebatchsize_cmd = ] deletebatchsize_cmd ] 
```  
  
## <a name="arguments"></a>引數  
`[ @database = ] database'`這是要建立的散發資料庫名稱。 *資料庫*是**sysname**，沒有預設值。 如果指定的資料庫已經存在，且尚未標示為散發資料庫，便會安裝啟用散發所需要的物件，且會將資料庫標示為散發資料庫。 如果指定的資料庫已啟用為散發資料庫，就會傳回錯誤。  
  
`[ @data_folder = ] 'data_folder'_`這是用來儲存散發資料庫資料檔案的目錄名稱。 *data_folder*是**Nvarchar （255）**，預設值是 Null。 如果[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是 Null，就會使用該實例的資料目錄，例如`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`。  
  
`[ @data_file = ] 'data_file'`這是資料庫檔案的名稱。 *data_file*是**Nvarchar （255）**，預設值是**database**。 如果是 NULL，這個預存程序會利用資料庫名稱來建構檔案名稱。  
  
`[ @data_file_size = ] data_file_size`這是初始資料檔案大小（以 mb 為單位）。 *data_file_size i*s **int**，預設值是5mb。  
  
`[ @log_folder = ] 'log_folder'`這是資料庫記錄檔的目錄名稱。 *log_folder*是**Nvarchar （255）**，預設值是 Null。 如果是 NULL，就會使用該 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料目錄 (例如 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`)。  
  
`[ @log_file = ] 'log_file'`這是記錄檔的名稱。 *log_file*是**Nvarchar （255）**，預設值是 Null。 如果是 NULL，這個預存程序會利用資料庫名稱來建構檔案名稱。  
  
`[ @log_file_size = ] log_file_size`這是初始記錄檔大小（以 mb 為單位）。 *log_file_size*是**int**，預設值是 0 MB，表示檔案大小是使用所允許的最小記錄檔大小所建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
`[ @min_distretention = ] min_distretention`這是從散發資料庫中刪除交易之前的最小保留期限（以小時為單位）。 *min_distretention*是**int**，預設值是0小時。  
  
`[ @max_distretention = ] max_distretention`這是在刪除交易之前的最大保留期限（以小時為單位）。 *max_distretention*是**int**，預設值是72小時。 未收到超過最大散發保留期限之複寫命令的訂閱，會被標示為非使用中，必須重新初始化。 針對每個非使用中的訂閱，系統會發出 RAISERROR 21011。 值為**0**表示複寫的交易不會儲存在散發資料庫中。  
  
`[ @history_retention = ] history_retention`這是要保留記錄的時數。 *history_retention*是**int**，預設值是48小時。  
  
`[ @security_mode = ] security_mode`這是連接到散發者時所要使用的安全性模式。 *security_mode*是**int**，預設值是1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證;**1**指定 Windows 整合式驗證。  
  
`[ @login = ] 'login'`這是連接到散發者時所使用的登入名稱，用來建立散發資料庫。 如果*security_mode*設定為**0**，這就是必要的。 *login*是**sysname**，預設值是 Null。  
  
`[ @password = ] 'password'`這是連接到散發者時所使用的密碼。 如果*security_mode*設定為**0**，這就是必要的。 *password*是**sysname**，預設值是 Null。  
  
`[ @createmode = ] createmode`*createmode*是**int**，預設值是1，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**1** （預設值）|建立資料庫或使用現有的資料庫，然後套用**instdist** ，以在散發資料庫中建立複寫物件。|  
|**2**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
 
`[ @deletebatchsize_xact = ] deletebatchsize_xact`指定從 MSRepl_Transactions 資料表清除過期的交易時，要使用的批次大小。 *deletebatchsize_xact*是**int**，預設值是5000。 這個參數最初是在 SQL Server 2017 中引進，後面接著 SQL Server 2012 SP4 和 SQL Server 2016 SP2 中的版本。  

`[ @deletebatchsize_cmd = ] deletebatchsize_cmd`指定在清除 MSRepl_Commands 資料表過期的命令期間，要使用的批次大小。 *deletebatchsize_cmd*是**int**，預設值是2000。 這個參數最初是在 SQL Server 2017 中引進，後面接著 SQL Server 2012 SP4 和 SQL Server 2016 SP2 中的版本。 
 
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_adddistributiondb**用於所有類型的複寫中。 不過，這個預存程序在散發者端執行。  
  
 您必須先執行[sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)來設定散發者，才能執行**sp_adddistributiondb**。  
  
 執行**sp_adddistributiondb**之前，請先執行**sp_adddistributor** 。  
  
## <a name="example"></a>範例  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
-- Specify the replication working directory.  
SET @directory = N'\\' + $(DistPubServer) + '\repldata';  
-- Specify the publication database.  
SET @publicationDB = N'AdventureWorks2012';   
  
-- Install the server MYDISTPUB as a Distributor using the defaults,  
-- including autogenerating the distributor password.  
USE master  
EXEC sp_adddistributor @distributor = @distributor;  
  
-- Create a new distribution database using the defaults, including  
-- using Windows Authentication.  
USE master  
EXEC sp_adddistributiondb @database = @distributionDB,   
    @security_mode = 1;  
GO  
  
-- Create a Publisher and enable AdventureWorks2012 for replication.  
-- Add MYDISTPUB as a publisher with MYDISTPUB as a local distributor  
-- and use Windows Authentication.  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
USE [distribution]  
EXEC sp_adddistpublisher @publisher=@publisher,   
    @distribution_db=@distributionDB,   
    @security_mode = 1;  
GO  
  
```  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_adddistributiondb**。  
  
## <a name="see-also"></a>另請參閱  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributiondb &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)  
  
  
