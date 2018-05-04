---
title: sys.sp_rda_reauthorize_db (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e8e68eef4e198ab55a6fa465abd07afa16918a21
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdareauthorizedb-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  還原啟用 「 延展 」 與遠端資料庫的本機資料庫之間已驗證的連接。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>引數  
 @credential = *@credential*  
 是與本機已啟用 Stretch 的資料庫相關聯的資料庫範圍認證。  
  
 @with_copy = *@with_copy*  
 指定是否要建立一份遠端資料，並連接到複本 （建議選項）。 *@with_copy* 位元。  
  
 @azure_servername = *@azure_servername*  
 指定包含遠端資料的 Azure 伺服器的名稱。 *@azure_servername* 是 sysname。  
  
 @azure_databasename = *@azure_databasename*  
 指定包含遠端資料的 Azure 資料庫的名稱。 *@azure_databasename* 是 sysname。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 >0 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 權限。  
  
## <a name="remarks"></a>備註  
 當您執行[sys.sp_rda_reauthorize_db (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新連線到遠端 Azure 資料庫，這項作業會自動重設的查詢模式 LOCAL_AND_REMOTE，這是預設行為，以使用 Stretch Database。 也就是說，查詢會傳回結果，從本機和遠端資料。  
  
## <a name="example"></a>範例  
 下列範例會還原啟用 「 延展 」 與遠端資料庫的本機資料庫之間已驗證的連接。 它會建立一份遠端資料 （建議），並連接到新的複本。  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_rda_deauthorize_db &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
