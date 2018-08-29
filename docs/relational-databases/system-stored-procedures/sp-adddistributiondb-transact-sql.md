---
title: sp_adddistributiondb & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 04/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_adddistributiondb_TSQL
- sp_adddistributiondb
helpviewer_keywords:
- sp_adddistributiondb
ms.assetid: e9bad56c-d2b3-44ba-a4d7-ff2fd842e32d
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: db1cc4feb71c3b7c7bdc09e1c62f5fa1237a3d0d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029173"
---
# <a name="spadddistributiondb-transact-sql"></a>sp_adddistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [  **@database=**]*資料庫 '*  
 這是要建立的散發資料庫名稱。 *資料庫*已**sysname**，沒有預設值。 如果指定的資料庫已經存在，且尚未標示為散發資料庫，便會安裝啟用散發所需要的物件，且會將資料庫標示為散發資料庫。 如果指定的資料庫已啟用為散發資料庫，就會傳回錯誤。  
  
 [  **@data_folder=**] **' * * * data_folder'*  
 這是用於儲存散發資料庫資料檔案的目錄名稱。 *data_folder*已**nvarchar(255)**，預設值是 NULL。 如果是 NULL，就會使用該 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料目錄，例如 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`。  
  
 [  **@data_file=**] **'***data_file***'**  
 這是資料庫檔案的名稱。 *data_file*已**nvarchar(255)**，預設值是**資料庫**。 如果是 NULL，這個預存程序會利用資料庫名稱來建構檔案名稱。  
  
 [  **@data_file_size=**] *data_file_size*  
 這是初始資料檔案大小 (以 MB 為單位)。 *data_file_size 我*s **int**，預設值是 5 MB。  
  
 [  **@log_folder=**] **'***log_folder***'**  
 這是資料庫記錄檔的目錄名稱。 *log_folder*已**nvarchar(255)**，預設值是 NULL。 如果是 NULL，就會使用該 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料目錄 (例如 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`)。  
  
 [  **@log_file=**] **'***log_file***'**  
 這是記錄檔的名稱。 *log_file*已**nvarchar(255)**，預設值是 NULL。 如果是 NULL，這個預存程序會利用資料庫名稱來建構檔案名稱。  
  
 [  **@log_file_size=**] *log_file_size*  
 這是初始記錄檔案大小 (以 MB 為單位)。 *log_file_size*已**int**，預設值是 0 MB，的表示檔案大小會建立使用的最小記錄檔案所允許的大小[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 [  **@min_distretention=**] *min_distretention*  
 這是從散發資料庫中刪除交易之前的最小保留期限 (以小時為單位)。 *min_distretention*已**int**，預設值是 0 小時。  
  
 [  **@max_distretention=**] *max_distretention*  
 這是在刪除交易之前的最大保留期限 (以小時為單位)。 *max_distretention*已**int**，預設值為 72 小時。 未收到超過最大散發保留期限之複寫命令的訂閱，會被標示為非使用中，必須重新初始化。 針對每個非使用中的訂閱，系統會發出 RAISERROR 21011。 值為**0**表示複寫的交易不會儲存在散發資料庫。  
  
 [  **@history_retention=**] *history_retention*  
 這是保留記錄的時數。 *history_retention*已**int**，預設值是 48 小時。  
  
 [  **@security_mode=**] *security_mode*  
 這是用於連接散發者的安全性模式。 *security_mode*已**int**，預設值是 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證;**1**指定 Windows 整合式驗證。  
  
 [  **@login=**] **'***登入***'**  
 這是連接到散發者來建立散發資料庫時，所用的登入名稱。 這是必要的如果*security_mode*設為**0**。 *login* 是預設值為 NULL 的 **sysname**。  
  
 [  **@password=**] **'***密碼***'**  
 這是連接到散發者時所用的密碼。 這是必要的如果*security_mode*設為**0**。 *密碼*已**sysname**，預設值是 NULL。  
  
 [  **@createmode=**] *createmode*  
 *createmode*已**int**，預設值是 1，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**1** (預設值)|CREATE DATABASE 或使用現有資料庫，再套用**instdist.sql**檔案以建立散發資料庫中的複寫物件。|  
|**2**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 [  **@from_scripting =** ] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
 
 [  **@deletebatchsize_xact=**] *deletebatchsize_xact*  
 指定要在過期的交易從 MSRepl_Transactions 資料表的清除作業期間使用的批次大小。 *deletebatchsize_xact*已**int**，預設值是 5000。 SQL Server 2017，後面接著 SQL Server 2012 SP4 和 SQL Server 2016 SP2 中的版本中引進這個參數。  

 [  **@deletebatchsize_cmd=**] *deletebatchsize_cmd*  
 指定批次大小來清理過期的命令，從 MSRepl_Commands 資料表的期間。 *deletebatchsize_cmd*已**int**，預設值是 2000年。 SQL Server 2017，後面接著 SQL Server 2012 SP4 和 SQL Server 2016 SP2 中的版本中引進這個參數。 
 
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_adddistributiondb**用於所有類型的複寫。 不過，這個預存程序在散發者端執行。  
  
 您必須設定 「 散發者 」，藉由執行[sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)執行之前，先**sp_adddistributiondb**。  
  
 執行**sp_adddistributor**在執行之前**sp_adddistributiondb**。  
  
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
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_adddistributiondb**。  
  
## <a name="see-also"></a>另請參閱  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributiondb &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)  
  
  
