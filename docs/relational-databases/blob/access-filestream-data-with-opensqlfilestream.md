---
title: 使用 OpenSqlFilestream 存取 FILESTREAM 資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
apiname:
- OpenSqlFilestream
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 826e0a047e119b186905f9d3f2d56170aa7b9249
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68041245"
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>使用 OpenSqlFilestream 存取 FILESTREAM 資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  OpenSqlFilestream API 會為儲存在檔案系統中的 FILESTREAM 二進位大型物件 (BLOB)，取得與 Win32 相容的檔案控制代碼。 此控制代碼可傳遞給下列任何 Win32 API： [ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)、 [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423)、 [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424)、 [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425)、 [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)或 [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)。 如果您將此控制代碼傳遞給其他任何 Win32 API，將會傳回錯誤 ERROR_ACCESS_DENIED。 在認可或回復交易之前，必須將此控制代碼傳遞給 Win32 的 [CloseHandle API](https://go.microsoft.com/fwlink/?LinkId=86428) 來關閉此控制代碼。 如果無法關閉此控制代碼，將會導致伺服器端資源洩露。  
  
 您必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易中執行所有的 FILESTREAM 資料容器存取。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式也可在同一交易中執行。 以維護 SQL 資料與 FILESTREAM 資料之間的一致性。  
  
 若要使用 Win32 存取 FILESTREAM BLOB，必須啟用 [Windows 授權](../../relational-databases/security/choose-an-authentication-mode.md) 。  
  
> [!IMPORTANT]  
>  當檔案已針對寫入存取開啟時，FILESTREAM 代理程式就會擁有此交易。 在釋放交易之前，僅允許 Win32 檔案 I/O。 若要釋放該異動，您必須關閉寫入控制代碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
HANDLE OpenSqlFilestream (  
    LPCWSTR FilestreamPath,  
    SQL_FILESTREAM_DESIRED_ACCESS DesiredAccess,  
    ULONG OpenOptions,  
    LPBYTE FilestreamTransactionContext,  
    SIZE_T FilestreamTransactionContextLength,  
    PLARGE_INTEGER AllocationSize);  
```  
  
#### <a name="parameters"></a>參數  
 *FilestreamPath*  
 [in] 這是 **PathName** 函式傳回的 [nvarchar(max)](../../relational-databases/system-functions/pathname-transact-sql.md) 路徑。 PathName 必須從具有 FILESTREAM 資料表與資料行之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT 或 UPDATE 權限的帳戶內容中呼叫。  
  
 *DesiredAccess*  
 [in] 設定用來存取 FILESTREAM BLOB 資料的模式。 此值會傳遞給 [DeviceIoControl 函式](https://go.microsoft.com/fwlink/?LinkId=105527)。  
  
|名稱|值|意義|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_READ|0|資料可以從檔案讀取。|  
|SQL_FILESTREAM_WRITE|1|資料可以寫入檔案。|  
|SQL_FILESTREAM_READWRITE|2|資料可以寫入檔案和從檔案讀取。|  
  
> [!NOTE]  
>  這些值會定義在 sqlncli.h 中的 SQL_FILESTREAM_DESIRED_ACCESS 列舉內。  
  
 *OpenOptions*  
 [in] 檔案屬性和旗標。 這個參數也可以包含下列旗標的任意組合。  
  
|旗標|值|意義|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_OPEN_NONE|0x00000000:|開啟或建立這個檔案時，不搭配任何特殊選項。|  
|SQL_FILESTREAM_OPEN_FLAG_ASYNC|0x00000001L|開啟或建立這個檔案是為了非同步 I/O。|  
|SQL_FILESTREAM_OPEN_FLAG_NO_BUFFERING|0x00000002L|系統藉由不使用任何系統快取來開啟檔案。|  
|SQL_FILESTREAM_OPEN_FLAG_NO_WRITE_THROUGH|0x00000004L|系統不會透過中繼快取來寫入。 會直接寫入磁碟。|  
|SQL_FILESTREAM_OPEN_FLAG_SEQUENTIAL_SCAN|0x00000008L|按順序從開頭至結尾存取檔案。 系統可使用這個做為最佳化檔案快取的提示。 如果應用程式藉移動檔案指標來進行隨機存取，則可能不會發生最佳快取。|  
|SQL_FILESTREAM_OPEN_FLAG_RANDOM_ACCESS|0x00000010L|隨機存取檔案。 系統可使用這個做為最佳化檔案快取的提示。|  
  
 *FilestreamTransactionContext*  
 [in] 此值由 [GET_FILESTREAM_TRANSACTION_CONTEXT](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) 函式傳回。  
  
 *FilestreamTransactionContextLength*  
 [in] GET_FILESTREAM_TRANSACTION_CONTEXT 函式傳回之 **varbinary(max)** 資料的位元組數。 此函數會傳回 N 個位元組的陣列。 N 是由此函數所決定，而且是所傳回之位元組陣列的屬性。  
  
 *AllocationSize*  
 [in] 指定資料檔的初始配置大小 (以位元組為單位)。 在讀取模式下將會被忽略。 這個參數可以是 NULL，此時會使用預設檔案系統行為。  
  
## <a name="return-value"></a>傳回值  
 如果此函數成功，傳回值就是指定之檔案的開啟控制代碼。 如果此函數失敗，傳回值就是 INVALID_HANDLE_VALUE。 如需更多的錯誤資訊，可呼叫 GetLastError()。  
  
## <a name="examples"></a>範例  
 下列範例將示範如何使用 `OpenSqlFilestream` API 來取得 Win32 控制代碼。  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/access-filestream-data-w_0_1.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/access-filestream-data-w_0_2.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/access-filestream-data-w_0_3.cpp)]  
  
## <a name="remarks"></a>備註  
 必須安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，才能使用此 API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會隨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端工具一起安裝。 如需詳細資訊，請參閱 [安裝 SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)。  
  
## <a name="see-also"></a>另請參閱  
 [二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [對 FILESTREAM 資料進行部分更新](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)   
 [避免與 FILESTREAM 應用程式中的資料庫作業相衝突](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
