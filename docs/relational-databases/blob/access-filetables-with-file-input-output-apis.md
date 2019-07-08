---
title: 使用檔案輸入輸出 API 存取 FileTable | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with file APIs
ms.assetid: fa504c5a-f131-4781-9a90-46e6c2de27bb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: abcbeb3cd6abfd1712217ed5577f2fafd4d5b4a3
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2019
ms.locfileid: "67582256"
---
# <a name="access-filetables-with-file-input-output-apis"></a>使用檔案輸入輸出 API 存取 FileTable
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  描述檔案系統 I/O 如何在 FileTable 上運作。  
  
##  <a name="accessing"></a> 開始使用 FileTable 檔案的 I/O API  
 FileTable 的主要用法是透過 Windows 檔案系統和檔案 I/O API。 FileTable 支援透過一系列可用檔案 I/O API 的非交易式存取。  
  
1.  檔案 I/O API 存取通常一開始會先取得檔案或目錄的邏輯 UNC 路徑。 應用程式可以搭配 [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) 函數使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以取得檔案或目錄的邏輯路徑。 如需詳細資訊，請參閱 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)。  
  
2.  然後應用程式會使用此邏輯路徑以取得檔案或目錄控制代碼，並對物件進行操作。 該路徑可傳遞至任何支援的檔案系統 API 函數，例如 CreateFile() 或 CreateDirectory()，以建立或開啟檔案並取得控制代碼。 控制代碼隨後便可用於以資料流形式處理資料、列舉或組織目錄、取得或設定檔案屬性、刪除檔案或目錄等。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="create"></a> 在 FileTable 中建立檔案和目錄  
 透過呼叫檔案 I/O API (例如 CreateFile 或 CreateDirectory) 在 FileTable 中建立檔案或目錄。  
  
-   支援所有建立配置旗標、共用模式及存取模式。 其中包括檔案建立、刪除及就地修改。 另外也支援檔案命名空間更新，例如目錄建立/刪除、重新命名和移動作業。  
  
-   新檔案或目錄的建立會對應到基礎 FileTable 中新資料列的建立。  
  
-   若為檔案，資料流資料會儲存在 **file_stream** 資料行中；若為目錄，此資料行為 null。  
  
-   若為檔案， **is_directory** 資料行內含 **false**。 若為目錄，此資料行內含 **true**。  
  
-   當多個並行的檔案 I/O 作業或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業在階層中影響同一個檔案或目錄時，會強制執行共用存取及並行存取。  
  
##  <a name="read"></a> 讀取 FileTable 中的檔案和目錄  
 若為所有資料流及屬性資料的檔案 I/O 存取作業， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會強制執行讀取認可隔離語意。  
  
##  <a name="write"></a> 寫入及更新 FileTable 中的檔案和目錄  
  
-   所有 FileTable 上的檔案 I/O 寫入或更新作業都是非交易式的。 也就是說，不會有任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易繫結至這些作業，而且不會提供任何 ACID 保證。  
  
-   FileTable 支援所有檔案 I/O 資料流/就地更新。  
  
-   透過檔案 I/O API 進行的 FILESTREAM 資料或屬性更新都將更新 FileTable 中對應的 **file_stream** 及對應的檔案屬性資料行。  
  
##  <a name="delete"></a> 刪除 FileTable 中的檔案和目錄  
 當您刪除檔案或目錄時會強制執行所有 Windows 檔案 I/O API 語意。  
  
-   如果目錄中包含任何檔案或子目錄，將無法刪除目錄。  
  
-   刪除檔案或目錄將會從 FileTable 中移除對應的資料列。 這相當於透過 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業刪除該資料列。  
  
##  <a name="supported"></a> 支援的檔案系統作業  
 FileTable 支援與下列檔案系統作業相關的檔案系統 API：  
  
-   目錄管理  
  
-   檔案管理  
  
 FileTable 不支援下列作業：  
  
-   磁碟管理  
  
-   磁碟區管理  
  
-   交易式 NTFS  
  
##  <a name="considerations"></a> FileTable 之檔案 I/O 存取的其他考量  
  
###  <a name="vnn"></a> 使用虛擬網路名稱 (VNN) 搭配 AlwaysOn 可用性群組  
 當包含 FILESTREAM 或 FileTable 資料的資料庫屬於 AlwaysOn 可用性群組時，透過檔案系統 API 對 FILESTREAM 或 FileTable 資料進行的所有存取都應該使用 VNN 而非電腦名稱。 如需詳細資訊，請參閱 [FILESTREAM 和 FileTable 與 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)。  
  
###  <a name="partial"></a> 部分更新  
 使用 [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) 函數在 FileTable 中取得的 FILESTREAM 資料可寫入控制代碼，可用於執行 FILESTREAM 內容的就地、部分更新。 此行為與交易 FILESTREAM 存取不同，它是透過呼叫 **OpenSQLFILESTREAM()** 及傳遞明確交易內容所取得的控制代碼來進行。  
  
###  <a name="trans"></a> 交易式語意  
 當您使用檔案 I/O API 於 FileTable 中存取檔案時，這些作業不會與任何使用者交易有關聯，並且具有下列其他特性：  
  
-   FileTable 中 FILESTREAM 資料的非交易式存取與任何交易無關，因此不會有任何特定的隔離語意。 但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會使用內部交易，針對 FileTable 資料強制執行鎖定或並行語意。 此類型的任何內部交易都已完成讀取認可隔離。  
  
-   這些 FILESTREAM 資料上的非交易作業沒有任何 ACID 保證。 一致性保證類似於檔案系統上應用程式所建立的檔案更新。  
  
-   這些變更無法回復。  
  
 但是，FileTable 中的 FILESTREAM 資料行也可以透過呼叫 **OpenSqlFileStream()** ，與交易式 FILESTREAM 存取一同進行存取。 這種存取可以完全為交易式，而且會接受目前一致支援的所有交易式層級。  
  
###  <a name="concurrency"></a> 並行存取控制  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在檔案系統應用程式之間以及檔案系統應用程式和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 應用程式之間強制執行 FileTable 存取的並行存取控制。 達成此並行存取控制的方式是針對 FileTable 資料列採取適當的鎖定。  
  
###  <a name="triggers"></a> 觸發程序  
 透過檔案系統建立、修改、或刪除檔案或目錄或其屬性，將會導致 FileTable 中對應的插入、更新或刪除作業。 任何關聯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] DML 觸發程序都會當做這些作業的一部分引發。  
  
##  <a name="funclist"></a> FileTable 中支援的檔案系統功能  
  
|功能|Supported|註解|  
|----------------|---------------|--------------|  
|**Oplock**|是|支援層級 2、層級 1、批次和篩選器 oplock。|  
|**擴充屬性**|否||  
|**重新剖析點**|否||  
|**持續的 ACL**|否||  
|**具名資料流**|否||  
|**疏鬆檔案**|是|疏鬆性只能在檔案上設定，而且會影響資料流的儲存方式。 FILESTREAM 資料儲存在 NTFS 磁碟區上，因此 FileTable 功能會將要求轉送至 NTFS 檔案系統以支援疏鬆檔案。|  
|**壓縮**|是||  
|**加密**|是||  
|**TxF**|否||  
|**檔案識別碼**|否||  
|**物件識別碼**|否||  
|**符號連結**|否||  
|**永久連結**|否||  
|**簡短名稱**|否||  
|**目錄變更通知**|否||  
|**位元組範圍鎖定**|是|位元組範圍鎖定的要求會傳遞到 NTFS 檔案系統。|  
|**記憶體對應檔案**|否||  
|**取消 I/O**|是||  
|**安全性**|否|系統會強制執行 Windows 共用層級安全性和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表與資料行層級安全性。|  
|**USN 日誌**|否|FileTable 和 DML 作業中檔案和目錄的中繼資料變更為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫上的 DML 作業。 因此，這些會記錄在對應的資料庫記錄檔中。 但是，並不會記錄在 NTFS USN 日誌中 (除非大小有變更)。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 變更追蹤功能可用於取得類似的資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [載入檔案至 FileTable](../../relational-databases/blob/load-files-into-filetables.md)   
 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [利用 Transact-SQL 存取 FileTable](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [FileTable DDL、函數、預存程序及檢視](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
