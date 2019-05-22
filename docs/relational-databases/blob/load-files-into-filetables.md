---
title: 載入檔案至 FileTable | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], migrating files
- FileTables [SQL Server], bulk loading
- FileTables [SQL Server], loading files
ms.assetid: dc842a10-0586-4b0f-9775-5ca0ecc761d9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c36a1b7235b1a323bbace94762411aa2c71df15b
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65094263"
---
# <a name="load-files-into-filetables"></a>載入檔案至 FileTable
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  描述如何載入或移轉檔案至 FileTable 中。  
  
##  <a name="BasicsLoadNew"></a> 將檔案載入或移轉至 FileTable  
 您選擇用於將檔案載入或移轉至 FileTable 中的方法，取決於目前儲存檔案的位置。  
  
|檔案的目前位置|移轉選項|  
|-------------------------------|---------------------------|  
|檔案目前儲存在檔案系統中。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 沒有檔案的知識。|因為 FileTable 會顯示成 Windows 檔案系統中的資料夾，所以您可以使用任何移動或複製檔案的可用方法，輕鬆地將檔案載入新的 FileTable。 這些方法包括 Windows 檔案總管、命令列選項 (包括 xcopy 與 robocopy)，以及自訂指令碼或應用程式。<br /><br /> 您無法將現有的資料夾轉換為 FileTable。|  
|檔案目前儲存在檔案系統中。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含內有指向檔案之指標的中繼資料資料表。|第一個步驟是使用上述其中一種方法移動或複製檔案。<br /><br /> 第二個步驟是將中繼資料的現有資料表，更新為指向該檔案的新位置。<br /><br /> 如需詳細資訊，請參閱本文中的[範例：將檔案從檔案系移轉至 FileTable](#HowToMigrateFiles)。|  
  
###  <a name="HowToLoadNew"></a> 如何：將檔案載入 FileTable  
您可使用下列方法將檔案載入 FileTable：  
  
-   在 [Windows 檔案總管] 中，將檔案從來源資料夾拖放至新的 FileTable 資料夾。  
  
-   透過命令提示字元或在批次檔或指令碼中，使用命令列選項，例如 MOVE、COPY、XCOPY 或 ROBOCOPY。  
  
-   在 C# 或 Visual Basic.NET 中撰寫自訂應用程式，來移動或複製檔案。 從 **System.IO** 命名空間呼叫方法。  
  
###  <a name="HowToMigrateFiles"></a> 範例：將檔案從檔案系移轉至 FileTable  
 在此案例中，您的檔案儲存在檔案系統中，而且您在擁有內含指向該檔案之指標的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，具有中繼資料表。 您想要將檔案移入 FileTable，然後使用 FileTable UNC 路徑來取代中繼資料內每個檔案的原始 UNC 路徑。 [GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md) 函式可協助您達成此目標。  
  
 在此範例中，假設存在現有的資料庫資料表 **PhotoMetadata**，其中包含相片的相關資料。 這個資料表中有一個 **varchar** (512) 類型的 **UNCPath**資料行，其中包含對應至 .jpg 檔案的實際 UNC 路徑。  
  
 若要將影像檔從檔案系統移轉至 FileTable，您必須進行下列動作：  
  
1.  建立新的 FileTable 以保存該檔案。 這個範例使用資料表名稱 **dbo.PhotoTable**，但並未顯示建立資料表的程式碼。  
  
2.  使用 xcopy 或類似的工具，將 .jpg 檔案及其目錄結構複製到 FileTable 的根目錄中。  
  
3.  使用類似下例的程式碼，修正 **PhotoMetadata** 資料表中的中繼資料：  
  
```sql  
--  Add a path locator column to the PhotoMetadata table.  
ALTER TABLE PhotoMetadata ADD pathlocator hierarchyid;  
  
-- Get the root path of the Photo directory on the File Server.  
DECLARE @UNCPathRoot varchar(100) = '\\RemoteShare\Photographs';  
  
-- Get the root path of the FileTable.  
DECLARE @FileTableRoot varchar(1000);  
SELECT @FileTableRoot = FileTableRootPath('dbo.PhotoTable');  
  
-- Update the PhotoMetadata table.  
  
-- Replace the File Server UNC path with the FileTable path.  
UPDATE PhotoMetadata  
    SET UNCPath = REPLACE(UNCPath, @UNCPathRoot, @FileTableRoot);  
  
-- Update the pathlocator column to contain the pathlocator IDs from the FileTable.  
UPDATE PhotoMetadata  
    SET pathlocator = GetPathLocator(UNCPath);  
```  
  
##  <a name="BasicsBulkLoad"></a> 將檔案大量載入 FileTable  
 FileTable 的大量作業行為和一般資料表相同，包含以下條件：  
  
 FileTable 具有系統定義的條件約束，可確保維持檔案與目錄命名空間的完整性。 大量載入至 FileTable 中的資料，必須通過這些條件約束的驗證。 因為某些大量插入作業允許忽略資料表條件約束，所以系統會強制執行下列要求。  
  
-   針對 FileTable 進行的強制執行條件約束之大量載入，與針對任何其他資料表所進行的大量載入作業執行方式相同。 此類別目錄包括以下作業：  
  
    -   含有 CHECK_CONSTRAINTS 子句的 bcp。  
  
    -   含有 CHECK_CONSTRAINTS 子句的 BULK INSERT。  
  
    -   INSERT INTO ...不含 IGNORE_CONSTRAINTS 子句的 SELECT * FROM OPENROWSET(BULK …)。  
  
-   除非已停用 FileTable 系統定義的條件約束，否則不強制執行條件約束的 FileTable 大量載入作業將會失敗。 此類別目錄包括以下作業：  
  
    -   不含 CHECK_CONSTRAINTS 子句的 bcp。  
  
    -   不含 CHECK_CONSTRAINTS 子句的 BULK INSERT。  
  
    -   INSERT INTO ...含 IGNORE_CONSTRAINTS 子句的 SELECT * FROM OPENROWSET(BULK …)。  
  
###  <a name="HowToBulkLoad"></a> 如何：將檔案大量載入 FileTable  
 您可以使用各種方法將檔案大量載入 FileTable：  
  
-   **bcp**  
  
    -   使用 **CHECK_CONSTRAINTS** 子句呼叫。  
  
    -   停用 FileTable 命名空間，但不使用 **CHECK_CONSTRAINTS** 子句呼叫。 然後重新啟用 FileTable 命名空間。  
  
-   **BULK INSERT**  
  
    -   使用 **CHECK_CONSTRAINTS** 子句呼叫。  
  
    -   停用 FileTable 命名空間，但不使用 **CHECK_CONSTRAINTS** 子句呼叫。 然後重新啟用 FileTable 命名空間。  
  
-   **INSERT INTO ...SELECT \* FROM OPENROWSET(BULK ...)**  
  
    -   使用 **IGNORE_CONSTRAINTS** 子句呼叫。  
  
    -   停用 FileTable 命名空間，且不使用 **IGNORE_CONSTRAINTS** 子句進行呼叫。 然後重新啟用 FileTable 命名空間。  
  
 如需停用 FileTable 條件約束的詳細資訊，請參閱 [管理 FileTables](../../relational-databases/blob/manage-filetables.md)。  
  
###  <a name="disabling"></a> 如何：為大量載入停用 FileTable 條件約束  
 若不希望大量載入檔案至 FileTable 時發生強制啟動系統定義之條件約束負擔，您可暫時停用該條件約束。 如需詳細資訊，請參閱 [管理作業步驟](../../relational-databases/blob/manage-filetables.md)。  
  
## <a name="see-also"></a>另請參閱  
 [利用 Transact-SQL 存取 FileTable](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [使用檔案輸入輸出 API 存取 FileTable](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
  
  
