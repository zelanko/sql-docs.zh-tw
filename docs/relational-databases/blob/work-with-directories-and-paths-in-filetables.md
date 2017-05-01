---
title: "使用 FileTables 中的目錄與路徑 | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], directories
ms.assetid: f1e45900-bea0-4f6f-924e-c11e1f98ab62
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d41410b3da1f823a29da0c5b7bd706dff4ce4584
ms.lasthandoff: 04/11/2017

---
# <a name="work-with-directories-and-paths-in-filetables"></a>使用 FileTables 中的目錄與路徑
  描述在 FileTable 中儲存檔案的目錄結構。  
  
##  <a name="HowToDirectories"></a> 如何：使用 FileTables 中的目錄與路徑  
 您可使用下列三項函數在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中使用 FileTable 目錄：  
  
|為得到此結果|使用此函數|  
|------------------------|-----------------------|  
|取得特定 FileTable 或目前資料庫的根層級 UNC 路徑。|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|  
|取得 FileTable 中檔案或目錄的絕對路徑或相對 UNC 路徑。|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|  
|經由提供路徑的方法，取得 FileTable 中指定之檔案或目錄的路徑定位器識別碼值。|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|  
  
##  <a name="BestPracticeRelativePaths"></a> 如何：使用可攜式程式碼的相對路徑  
 若要讓程式碼和應用程式獨立於目前的電腦和資料庫之外，請避免撰寫依賴絕對檔案路徑的程式碼。 相反地，同時使用 [FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md) 和 [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)函數，以取得檔案在執行階段的完整路徑，如下列範例所示。 根據預設， **GetFileNamespacePath** 函數會傳回資料庫根路徑之下的檔案相對路徑。  
  
```tsql  
USE database_name;  
DECLARE @root nvarchar(100);  
DECLARE @fullpath nvarchar(1000);  
  
SELECT @root = FileTableRootPath();  
SELECT @fullpath = @root + file_stream.GetFileNamespacePath()  
    FROM filetable_name  
    WHERE name = N'document_name';  
  
PRINT @fullpath;  
GO  
```  
  
##  <a name="restrictions"></a> 重要限制  
  
###  <a name="nesting"></a> 巢狀層級  
  
> **重要！！** 您不能在 FileTable 目錄中儲存超過 15 層的子目錄。 當您儲存了 15 層的子目錄時，最低的一層將無法包含任何檔案，因為這些檔案代表另外的一層。  
  
###  <a name="fqnlength"></a> 完整路徑名稱長度  
  
> **重要！！** NTFS 檔案系統支援遠超過 Windows Shell 和大多數 Windows API 的 260 字元限制的路徑名稱。 因此，可以使用 Transact-SQL 建立 FileTable 檔案階層中完整路徑名稱超過 260 字元的檔案，但卻無法以 Windows 檔案總管或許多其他 Windows 應用程式檢視或開啟這些檔案。 不過，您可以繼續使用 Transact-SQL 存取這些檔案。  
  
##  <a name="fullpath"></a> FileTable 中儲存之項目的完整路徑  
 FileTable 中儲存之檔案或目錄的完整路徑，由下列元素做為開頭：  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體層級為 FILESTREAM 檔 I/O 存取啟用共用。  
  
2.  **DIRECTORY_NAME** 於資料庫層級指定。  
  
3.  **FILETABLE_DIRECTORY** 於 FileTable 層級指定。  
  
 所產生的階層如下：  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\`  
  
 此目錄階層會形成 FileTable 命名空間的根。 在此目錄階層之下，FileTable 的 FILESTREAM 資料將會儲存為檔案，以及其下也可以再包含檔案與子目錄的子目錄。  
  
 請務必牢記，於此執行個體層級的 FILESTREAM 共用之下所建立的目錄階層，是一個虛擬的目錄階層。 此階層儲存於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，且不會實際於 NTFS 檔案系統中呈現出來。 所有存取 FILESTREAM 共用之下以及其所包含之 FileTables 中檔案與目錄的作業，都會由檔案系統中內嵌的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件所攔截與處理。  
  
##  <a name="roots"></a> 執行個體、資料庫與 FileTable 層級上根目錄的語意  
 此目錄階層結構遵循下列語義：  
  
-   執行個體層級的 FILESTREAM 共用由管理員所設定，而且會儲存為伺服器屬性。 您可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，重新命名此共用。 伺服器重新啟動之前重新命名作業不會生效。  
  
-   當您建立新的資料庫時，資料庫層級的 **DIRECTORY_NAME** 預設為 null。 管理員可使用 **ALTER DATABASE** 陳述式設定或變更此名稱。 該執行個體中的名稱不行重複 (不分大小寫)。  
  
-   一般來說，當您建立 FileTable 時，會提供 **FILETABLE_DIRECTORY** 名稱作為 **CREATE TABLE** 陳述式的一部分。 您也可以使用 **ALTER TABLE** 命令變更此名稱。  
  
-   您無法透過檔案 I/O 作業變更這些根目錄的名稱。  
  
-   您無法以獨佔的檔案控制開啟這些根目錄。  
  
##  <a name="is_directory"></a> FileTable 結構描述中的 is_directory 資料行  
 下表描述 **is_directory** 資料行以及與將 FILESTREAM 資料包含於 FileTable 中的 **file_stream** 資料行之間的互動。  
  
||||  
|-|-|-|  
|*is_directory* **value**|*file_stream* **value**|**行為**|  
|FALSE|NULL|此為無效的組合，將由系統定義的條件約束所攔截。|  
|FALSE|\<值>|該項目代表檔案。|  
|TRUE|NULL|該項目代表目錄。|  
|TRUE|\<值>|此為無效的組合，將由系統定義的條件約束所攔截。|  
  
##  <a name="alwayson"></a> 使用虛擬網路名稱 (VNN) 搭配 AlwaysOn 可用性群組  
 當包含 FILESTREAM 或 FileTable 資料的資料庫屬於 AlwaysOn 可用性群組時：  
  
-   FILESTREAM 和 FileTable 函數會接受或傳回虛擬網路名稱 (VNN) 而非電腦名稱。 如需有關這些函數的詳細資訊，請參閱 [Filestream and FileTable Functions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md) (Filestream 和 FileTable 函數 (Transact-SQL))。  
  
-   透過檔案系統 API 對 FILESTREAM 或 FileTable 資料進行的所有存取都應該使用 VNN 而非電腦名稱。 如需詳細資訊，請參閱 [FILESTREAM 和 FileTable 與 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟用 FileTable 的必要條件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)   
 [建立、改變及卸除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [利用 Transact-SQL 存取 FileTable](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [使用檔案輸入輸出 API 存取 FileTable](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
  
  

