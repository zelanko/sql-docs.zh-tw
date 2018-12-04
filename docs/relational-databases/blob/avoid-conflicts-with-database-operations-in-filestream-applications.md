---
title: 避免與 FILESTREAM 應用程式中的資料庫作業相衝突 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32 and Transact-SQL Conflicts
ms.assetid: 8b1ee196-69af-4f9b-9bf5-63d8ac2bc39b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b5967b38a0bcc648bf02a5b3c6fa404b31eaaccf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540634"
---
# <a name="avoid-conflicts-with-database-operations-in-filestream-applications"></a>避免與 FILESTREAM 應用程式中的資料庫作業相衝突
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 SqlOpenFilestream() 來開啟 Win32 檔案控制代碼以便讀取或寫入 FILESTREAM BLOB 資料的應用程式可能會與在一般交易中管理的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式發生衝突錯誤。 這包括需要很長時間才能執行完成的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 MARS 查詢。 若要有效避免這些衝突類型，您必須仔細地設計應用程式。  
  
 當 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 或應用程式嘗試開啟 FILESTREAM BLOB 時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會檢查相關聯的交易內容。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會根據開啟作業是使用 DDL 陳述式、DML 陳述式、擷取資料或管理交易，允許或拒絕此要求。 下表將顯示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 根據交易所開啟的檔案類型來判斷允許或拒絕 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
|Transact-SQL 陳述式|開啟以便讀取|開啟以便寫入|  
|------------------------------|---------------------|----------------------|  
|使用資料庫中繼資料的 DDL 陳述式，例如 CREATE TABLE、CREATE INDEX、DROP TABLE 和 ALTER TABLE。|Allowed|封鎖並且因逾時而失敗。|  
|使用資料庫所儲存之資料的 DML 陳述式，例如 UPDATE、DELETE 和 INSERT。|Allowed|拒絕|  
|SELECT|Allowed|Allowed|  
|COMMIT TRANSACTION|拒絕*|拒絕*|  
|SAVE TRANSACTION|拒絕*|拒絕*|  
|ROLLBACK|允許*|允許*|  
  
 \* 取消交易，而且交易內容的開啟控制代碼會失效。 應用程式必須關閉所有開啟控制代碼。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式和 FILESTREAM Win32 存取如何造成衝突。  
  
### <a name="a-opening-a-filestream-blob-for-write-access"></a>A. 開啟 FILESTREAM BLOB 進行寫入存取  
 下列範例會顯示開啟檔案進行唯寫存取的作用。  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//Write some date to the FILESTREAM BLOB.  
WriteFile(dstHandle, updateData, ...);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed. The FILESTREAM BLOB is  
//returned without the modifications that are made by  
//WriteFile(dstHandle, updateData, ...).  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed. The FILESTREAM BLOB  
//is returned with the updateData applied.  
```  
  
### <a name="b-opening-a-filestream-blob-for-read-access"></a>B. 開啟 FILESTREAM BLOB 進行讀取存取  
 下列範例會顯示開啟檔案進行唯讀存取的作用。  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed. Any changes that are  
//made to the FILESTREAM BLOB will not be returned until  
//the dstHandle is closed.  
//SELECT statements will be allowed.  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="c-opening-and-closing-multiple-filestream-blob-files"></a>C. 開啟並關閉多個 FILESTREAM BLOB 檔案  
 如果已開啟多個檔案，就會使用限制最嚴格的規則。 下列範例會開啟兩個檔案。 第一個檔案會開啟以便讀取，而第二個檔案會開啟以便寫入。 在開啟第二個檔案之前，系統會拒絕 DML 陳述式。  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
  
dstHandle1 =  OpenSqlFilestream(dstFilePath1, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
//Close the read handle. The write handle is still open.  
CloseHandle(dstHandle);  
//DML statements are still denied because the write handle is open.  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
CloseHandle(dstHandle1);  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="d-failing-to-close-a-cursor"></a>D. 無法關閉資料指標  
 下列範例會顯示未關閉的陳述式資料指標如何讓 `OpenSqlFilestream()` 無法開啟 BLOB 進行寫入存取。  
  
```  
TCHAR *sqlDBQuery =  
TEXT("SELECT GET_FILESTREAM_TRANSACTION_CONTEXT(),")  
TEXT("Chart.PathName() FROM Archive.dbo.Records");  
  
//Execute a long-running Transact-SQL statement. Do not allow  
//the statement to complete before trying to  
//open the file.  
  
SQLExecDirect(hstmt, sqlDBQuery, SQL_NTS);  
  
//Before you call OpenSqlFilestream() any open files  
//that the Cursor the Transact-SQL statement is using  
// must be closed. In this example,  
//SQLCloseCursor(hstmt) is not called so that  
//the transaction will indicate that there is a file  
//open for reading. This will cause the call to  
//OpenSqlFilestream() to fail because the file is  
//still open.  
  
HANDLE srcHandle =  OpenSqlFilestream(srcFilePath,  
     Write, 0,  transactionToken,  cbTransactionToken,  0);  
  
//srcHandle will == INVALID_HANDLE_VALUE because the  
//cursor is still open.  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 OpenSqlFilestream 存取 FILESTREAM 資料](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [使用 Multiple Active Result Set &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
  
  
