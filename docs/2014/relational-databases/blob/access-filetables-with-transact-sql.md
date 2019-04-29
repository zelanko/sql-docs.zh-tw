---
title: 利用 Transact-SQL 存取 FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 28447ca0e1e503e73826aba5e02b22bf71cff6c3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920312"
---
# <a name="access-filetables-with-transact-sql"></a>利用 Transact-SQL 存取 FileTable
  描述 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料操作語言 (DML) 命令如何與 FileTable 搭配使用。  
  
##  <a name="BasicsInsert"></a> FileTable 上的 INSERT 作業  
 下列考量適用於 FileTable 上的 **INSERT** 作業：  
  
-   所有檔案屬性資料行都有 NOT NULL 條件約束。 若未明確設定值，則會提供適當的預設值。  
  
-   若 INSERT 陳述式設定 **name**、**path_locator**、**parent_path_locator** 或檔案屬性，則會強制執行系統定義的條件約束。  
  
-   提供 [GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql) 函數的檔案系統路徑，應用程式就可以取得檔案或目錄的 **path_locator**。  
  
##  <a name="BasicsUpdate"></a> FileTable 上的 UPDATE 作業  
 下列考量適用於 FileTable 上的 **UPDATE** 作業：  
  
-   允許更新任何使用者定義的資料。  
  
-   若 INSERT 陳述式設定 **name**、 **path_locator**、 **parent_path_locator**或檔案屬性，則會強制執行系統定義的條件約束。  
  
-   您可以更新 **file_stream** 資料行中的 FILESTREAM 資料，而不影響任何其他資料行 (包括時間戳記)。  
  
##  <a name="BasicsDelete"></a> FileTable 上的 DELETE 作業  
 下列考量適用於 FileTable 上的 **DELETE** 作業：  
  
-   刪除資料列也會從檔案系統中移除對應的檔案或目錄。  
  
-   若資料列對應至包含其他檔案或目錄的目錄，則無法刪除資料列。  
  
##  <a name="BasicsConstraints"></a> 針對 FileTable 上 DML 作業強制執行的條件約束  
 系統定義的條件約束可確保 DML 動作不會危害檔案命名空間階層的完整性。 強制執行的條件約束包括：  
  
-   當您設定或變更檔案或目錄的 **名稱** 時：  
  
    -   會強制執行 Windows 檔案及目錄命名慣例。  
  
    -   會強制執行上層目錄中名稱的唯一性。  
  
-   當您設定或變更 **path_locator** 或 **parent_path_locator**以設定或變更檔案或目錄的位置時：  
  
    -   會強制執行唯一性。  
  
    -   會強制執行目錄和檔案之階層樹狀目錄的一致性 (包括 **path_locator** 和 **parent_path_locator** 值的一致性)。  
  
-   當 **file_stream** 資料行不是 Null 時，則無法將 **is_directory** 的值設定為 true。 **file_stream** 資料行中的資料指出資料列代表檔案，而非代表目錄。  
  
-   檔案屬性資料行不得為 Null。 會使用預設值強制執行 NOT NULL 條件約束。  
  
-   **last_access_time** 的值不能早於 **last_write_time** 和 **creation_time**。  
  
## <a name="see-also"></a>另請參閱  
 [載入檔案至 FileTable](load-files-into-filetables.md)   
 [使用 FileTables 中的目錄與路徑](work-with-directories-and-paths-in-filetables.md)   
 [使用檔案輸入輸出 API 存取 FileTable](access-filetables-with-file-input-output-apis.md)   
 [FileTable DDL、函數、預存程序及檢視](../views/views.md)  
  
  
