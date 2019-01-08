---
title: 建立 FILESTREAM 資料的用戶端應用程式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32
ms.assetid: 8a02aff6-e54c-40c6-a066-2083e9b090aa
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 017762b9897af951020793fdd02fc34d3209da2d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363650"
---
# <a name="create-client-applications-for-filestream-data"></a>建立 FILESTREAM 資料的用戶端應用程式
  您可以使用 Win32 來讀取及寫入資料至 FILESTREAM BLOB。 下面是必要的步驟：  
  
-   讀取 FILESTREAM 檔案路徑。  
  
-   讀取目前交易內容。  
  
-   取得 Win32 控制代碼，並且使用此控制代碼來讀取及寫入資料至 FILESTREAM BLOB。  
  
> [!NOTE]  
>  此主題中的範例需要使用在 [建立啟用 FILESTREAM 的資料庫](create-a-filestream-enabled-database.md) 和 [建立儲存 FILESTREAM 資料的資料表](create-a-table-for-storing-filestream-data.md)中建立之啟用 FILESTREAM 的資料庫和資料表。  
  
##  <a name="func"></a> 使用 FILESTREAM 資料的功能  
 當您使用 FILESTREAM 來儲存二進位大型物件 (BLOB) 資料時，可以使用 Win32 API 來處理檔案。 為了支援在 Win32 應用程式中使用 FILESTREAM BLOB 資料， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了下列函數和 API：  
  
-   [PathName](/sql/relational-databases/system-functions/pathname-transact-sql) 會將路徑當做 Token 傳給 BLOB。 應用程式會使用此 Token 來取得 Win32 控制代碼，並在 BLOB 資料上運作。  
  
     當包含 FILESTREAM 資料的資料庫屬於 AlwaysOn 可用性群組時，PathName 函數就會傳回虛擬網路名稱 (VNN) 而非電腦名稱。  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT()](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) 會傳回代表工作階段之目前交易的 Token。 應用程式會使用此 Token 將 FILESTREAM 檔案系統資料流作業繫結至此交易。  
  
-   [OpenSqlFilestream API](access-filestream-data-with-opensqlfilestream.md) 會取得 Win32 檔案控制代碼。 應用程式寫入資料流 FILESTREAM 資料，會使用控制代碼，並可以再將控制代碼傳遞給下列 Win32 Api:[ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)， [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423)， [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424)， [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425)， [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)，或[FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)。 如果應用程式使用此控制代碼呼叫任何其他 API，就會傳回 ERROR_ACCESS_DENIED 錯誤。 應用程式應該使用 [CloseHandle](https://go.microsoft.com/fwlink/?LinkId=86428)來關閉此控制代碼。  
  
 所有 FILESTREAM 資料容器存取都是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易中執行。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可以在相同的交易中執行，以維護 SQL 資料與 FILESTREAM 資料之間的一致性。  
  
##  <a name="steps"></a> 存取 FILESTREAM 資料的步驟  
  
###  <a name="path"></a> 讀取 FILESTREAM 檔案路徑  
 FILESTREAM 資料表中的每個資料格都具有與它相關聯的檔案路徑。 若要讀取此路徑，請在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中使用 `PathName` 資料行的 `varbinary(max)` 屬性。 下列範例將示範如何讀取 `varbinary(max)` 資料行的檔案路徑。  
  
 [!code-sql[FILESTREAM#FS_PathName](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_pathname)]  
  
###  <a name="trx"></a> 讀取交易內容  
 若要取得目前的交易內容，請使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] [GET_FILESTREAM_TRANSACTION_CONTEXT()](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) 函數。 下列範例將示範如何開始交易並讀取目前交易內容。  
  
 [!code-sql[FILESTREAM#FS_GET_TRANSACTION_CONTEXT](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_get_transaction_context)]  
  
###  <a name="handle"></a> 取得 Win32 檔案控制代碼  
 若要取得 Win32 檔案控制代碼，請呼叫 OpenSqlFilestream API。 這個 API 是從 sqlncli.dll 檔案中匯出。 傳回的控制代碼可傳遞至任何下列的 Win32 Api:[ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)， [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423)， [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424)， [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425)， [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)，或[FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)。 下列範例將示範如何取得 Win32 檔案控制代碼，並用它來讀取及寫入資料至 FILESTREAM BLOB。  
  
 [!code-csharp[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cs/filestream.cs#fs_cs_readandwriteblob)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/vb/filestream.vb#fs_vb_readandwriteblob)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_writeblob)]  
  
##  <a name="best"></a> 應用程式設計和實作的最佳作法  
  
-   當您要設計和實作使用 FILESTREAM 的應用程式時，請考慮下列指導方針：  
  
-   使用 NULL (而非 0x) 來表示未初始化的 FILESTREAM 資料行。 0x 值會導致系統建立檔案，而 NULL 則不會。  
  
-   避免在包含非 Null FILESTREAM 資料行的資料表中進行插入和刪除作業。 插入和刪除作業可能會修改用於記憶體回收的 FILESTREAM 資料表。 這可能會導致應用程式的效能隨著時間降低。  
  
-   在使用複寫的應用程式中，使用 NEWSEQUENTIALID() 來取代 NEWID()。 就這些應用程式的 GUID 產生而言，NEWSEQUENTIALID() 的執行效能高於 NEWID()。  
  
-   FILESTREAM API 是針對資料的 Win32 資料流存取所設計。 請避免使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來讀取或寫入超過 2 MB 的 FILESTREAM 二進位大型物件 (BLOB)。 如果您必須從 [!INCLUDE[tsql](../../includes/tsql-md.md)]讀取或寫入 BLOB，請在嘗試從 Win32 開啟 FILESTREAM BLOB 之前，確定已取用所有 BLOB 資料。 如果無法取用所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料，可能會導致任何後續的 FILESTREAM 開啟或關閉作業失敗。  
  
-   避免使用更新、附加或預先附加資料至 FILESTREAM BLOB 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 這會導致 BLOB 資料多工緩衝處理到 tempdb 資料庫中，然後送回新的實體檔案。  
  
-   避免將小型 BLOB 更新附加至 FILESTREAM BLOB。 每次附加都會導致系統複製基礎 FILESTREAM 檔案。 如果應用程式必須附加小型 BLOB，請將這些 BLOB 寫入 `varbinary(max)` 資料行，然後在 BLOB 的數目到達預先決定的限制時，針對 FILESTREAM BLOB 執行單一寫入作業。  
  
-   避免在應用程式中擷取大量 BLOB 檔案的資料長度。 這是一項耗時的作業，因為大小不會儲存在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中。 如果您必須判斷 BLOB 檔案的長度，請使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DATALENGTH() 函數來判斷 BLOB 的大小 (如果它已關閉的話)。 DATALENGTH() 不會開啟 BLOB 檔案來判斷其大小。  
  
-   如果應用程式使用 Message Block1 (SMB1) 通訊協定，您就應該以 60-KB 的倍數來讀取 FILESTREAM BLOB 資料，以便發揮最佳效能。  
  
## <a name="see-also"></a>另請參閱  
 [避免與 FILESTREAM 應用程式中的資料庫作業相衝突](avoid-conflicts-with-database-operations-in-filestream-applications.md)   
 [使用 OpenSqlFilestream 存取 FILESTREAM 資料](access-filestream-data-with-opensqlfilestream.md)   
 [二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)   
 [對 FILESTREAM 資料進行部分更新](make-partial-updates-to-filestream-data.md)  
  
  
