---
title: 使用 Transact-SQL 存取 FILESTREAM 資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Transact-SQL
ms.assetid: a6bf0ce7-7e5e-4a07-8917-ee526c9d0a05
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 067f14e857addc5f43a0b17d81d554997adbc09f
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010436"
---
# <a name="access-filestream-data-with-transact-sql"></a>使用 Transact-SQL 存取 FILESTREAM 資料
  本主題描述如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT、UPDATE 及 DELETE 陳述式來管理 FILESTREAM 資料。  
  
> [!NOTE]  
>  本主題中的範例需要使用在 [建立啟用 FILESTREAM 的資料庫](create-a-filestream-enabled-database.md) 和 [建立儲存 FILESTREAM 資料的資料表](create-a-table-for-storing-filestream-data.md)中建立之啟用 FILESTREAM 的資料庫和資料表。  
  
##  <a name="ins"></a> 插入包含 FILESTREAM 資料的資料列  
 若要將資料列加入至支援 FILESTREAM 資料的資料表，請使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 陳述式。 當您將資料插入 FILESTREAM 資料行時，可以插入 NULL 或 `varbinary(max)` 值。  
  
### <a name="inserting-null"></a>插入 NULL  
 下列範例將示範如何插入 `NULL`。 當 FILESTREAM 值為 `NULL`時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 就不會在檔案系統中建立檔案。  
  
 [!code-sql[FILESTREAM#FS_InsertNULL](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertnull)]  
  
### <a name="inserting-a-zero-length-record"></a>插入長度為零的記錄  
 下列範例將示範如何使用 `INSERT` 來建立長度為零的記錄。 當您想要取得檔案控制代碼，但是將要使用 Win32 API 操作檔案時，這會很有用。  
  
 [!code-sql[FILESTREAM#FS_InsertZero](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertzero)]  
  
### <a name="creating-a-data-file"></a>建立資料檔  
 下列範例將示範如何使用 `INSERT` 來建立包含資料的檔案。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將 `Seismic Data` 字串轉換成 `varbinary(max)` 值。 FILESTREAM 會建立此 Windows 檔案 (如果不存在的話)，然後資料會加入到此資料檔中。  
  
 [!code-sql[FILESTREAM#FS_InsertData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertdata)]  
  
 當您從 `Archive`.`dbo.Records` 資料表中選取所有資料時，其結果與下表所顯示的結果很相似。 不過， `Id` 資料行將包含不同的 GUID。  
  
|Id|SerialNumber|繼續|  
|--------|------------------|------------|  
|`C871B90F-D25E-47B3-A560-7CC0CA405DAC`|`1`|`NULL`|  
|`F8F5C314-0559-4927-8FA9-1535EE0BDF50`|`2`|`0x`|  
|`7F680840-B7A4-45D4-8CD5-527C44D35B3F`|`3`|`0x536569736D69632044617461`|  
  
##  <a name="upd"></a> 更新 FILESTREAM 資料  
 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來更新檔案系統檔案中的資料。不過，當您必須將大量資料串流處理至檔案時，可能不會想要這樣做。  
  
 下列範例會以文字 `Xray 1`來取代檔案記錄中的所有文字。  
  
 [!code-sql[FILESTREAM#FS_UpdateData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_updatedata)]  
  
##  <a name="del"></a> 刪除 FILESTREAM 資料  
 當您刪除包含 FILESTREAM 欄位的資料列時，您也會刪除其基礎檔案系統的檔案。 因此，刪除資料列與檔案的唯一方法，是使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE 陳述式。  
  
 下列範例將示範如何刪除資料列及相關聯的檔案系統檔案。  
  
 [!code-sql[FILESTREAM#FS_DeleteData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_deletedata)]  
  
 當您從 `dbo.Archive` 資料表中選取所有資料時，此資料列就會消失。 您無法再使用相關聯的檔案。  
  
> [!NOTE]  
>  基礎檔案會由 FILESTREAM 記憶體回收行程所移除。  
  
## <a name="see-also"></a>另請參閱  
 [啟用及設定 FILESTREAM](enable-and-configure-filestream.md)   
 [避免與 FILESTREAM 應用程式中的資料庫作業相衝突](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
