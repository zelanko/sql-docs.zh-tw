---
title: sys. sp_rda_reauthorize_db (Transact-sql) |Microsoft Docs
description: 瞭解如何使用 sys. sp_rda_reauthorize_db 來還原本機已啟用 Stretch 的資料庫與遠端資料庫之間的已驗證連接。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5f23c30ea481659bc1ce2366d674cea7fc753251
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540436"
---
# <a name="syssp_rda_reauthorize_db-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  還原已啟用 Stretch 和遠端資料庫之本機資料庫之間的已驗證連接。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>引數  
 @credential= * \@ 認證*  
 這是與本機已啟用 Stretch 的資料庫相關聯的資料庫範圍認證。  
  
 @with_copy= * \@ with_copy*  
 指定是否要建立遠端資料的複本，並連接到 (建議) 的複製。 * \@ with_copy*是 bit。  
  
 @azure_servername= * \@ azure_servername*  
 指定包含遠端資料的 Azure 伺服器名稱。 * \@ azure_servername*為 sysname。  
  
 @azure_databasename= * \@ azure_databasename*  
 指定包含遠端資料之 Azure 資料庫的名稱。 * \@ azure_databasename*為 sysname。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 >0 (失敗)   
  
## <a name="permissions"></a>權限  
 需要 db_owner 許可權。  
  
## <a name="remarks"></a>備註  
 當您執行 [sys. sp_rda_reauthorize_db (transact-sql) ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 重新連接到遠端 Azure 資料庫時，這項作業會自動將查詢模式重設為 LOCAL_AND_REMOTE，這是 Stretch Database 的預設行為。 也就是說，查詢會傳回本機和遠端資料的結果。  
  
## <a name="example"></a>範例  
 下列範例會還原已啟用延展的本機資料庫與遠端資料庫之間的已驗證連接。 它會複製遠端資料 (建議) ，並連接到新的複本。  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys. sp_rda_deauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
