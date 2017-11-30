---
title: "FileTableRootPath (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs: TSQL
helpviewer_keywords: FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 475c76c68198719de312a6a7ca9485097596d624
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回特定 FileTable 或目前資料庫的根層級 UNC 路徑。  
  
## <a name="syntax"></a>語法  
  
```  
  
FileTableRootPath ( [ ‘[schema_name.]FileTable_name’ ], @option )  
```  
  
## <a name="arguments"></a>引數  
 *FileTable_name*  
 FileTable 的名稱。 *FileTable_name*的型別**nvarchar**。 這是選擇性參數。 預設值為目前的資料庫。 指定*schema_name*也是選擇性的。 您可以傳遞 NULL 做*FileTable_name*使用預設參數值  
  
 *@option*  
 定義路徑之伺服器元件格式化方式的整數運算式。 *@option*可以有下列值之一：  
  
|值|描述|  
|-----------|-----------------|  
|**0**|傳回轉換成 NetBIOS 格式的伺服器名稱，例如：<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDB`<br /><br /> 這是預設值。|  
|**1**|在不轉換的情況下傳回伺服器名稱，例如：<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDB`|  
|**2**|傳回完整伺服器路徑，例如：<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDB`|  
  
## <a name="return-type"></a>傳回類型  
 **nvarchar(4000)**  
  
 當資料庫屬於 Alwayson 可用性群組，然後在**FileTableRootPath**函式會傳回虛擬網路名稱 (VNN) 而非電腦名稱。  
  
## <a name="general-remarks"></a>一般備註  
 **FileTableRootPath**函式會傳回 NULL，當下列條件的其中一個為 true 時：  
  
-   值*FileTable_name*不正確。  
  
-   呼叫端沒有足以參考指定資料表或目前資料庫的權限。  
  
-   FILESTREAM 選項的*database_directory*未設定為目前的資料庫。  
  
 如需詳細資訊，請參閱 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)。  
  
## <a name="best-practices"></a>最佳作法  
 若要讓程式碼和應用程式獨立於目前的電腦和資料庫之外，請避免撰寫依賴絕對檔案路徑的程式碼。 相反地，使用取得的檔案在執行階段的完整路徑**FileTableRootPath**和**GetFileNamespacePath**函式在一起，如下列範例所示。 根據預設， **GetFileNamespacePath** 函數會傳回資料庫根路徑之下的檔案相對路徑。  
  
```tsql  
USE MyDocumentDB;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 **FileTableRootPath**函式需要：  
  
-   可以取得特定 FileTable 根路徑之 FileTable 的 SELECT 權限。  
  
-   **db_datareader**或更高的權限，為取得目前資料庫中的根路徑。  
  
## <a name="examples"></a>範例  
 下列範例示範如何呼叫**FileTableRootPath**函式。  
  
```  
USE MyDocumentDB;  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB”  
SELECT FileTableRootPath();  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB\MyFileTable”  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB\MyFileTable”  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>請參閱  
 [使用 FileTable 中的目錄與路徑](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
