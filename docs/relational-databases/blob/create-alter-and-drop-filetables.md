---
title: "建立、改變及卸除 FileTable | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], altering
- FileTables [SQL Server], dropping
- FileTables [SQL Server], creating
ms.assetid: 47d69e37-8778-4630-809b-2261b5c41c2c
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0445d1e3f300031a0154e253009a516364cd4fc3
ms.lasthandoff: 04/11/2017

---
# <a name="create-alter-and-drop-filetables"></a>建立、改變及卸除 FileTable
  描述如何建立新的 FileTable，或是改變或卸除現有的 FileTable。  
  
##  <a name="BasicsCreate"></a> 建立 FileTable  
 FileTable 是一種特殊化使用者資料表，它具有預先定義且固定的結構描述。 這個結構描述會儲存 FILESTREAM 資料、檔案和目錄資訊，以及檔案屬性。 如需有關 FileTable 結構描述的詳細資訊，請參閱＜ [FileTable Schema](../../relational-databases/blob/filetable-schema.md)＞。  
  
 您可以使用 Transact-SQL 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來建立新的 FileTable。 因為 FileTable 具有固定的結構描述，所以您不需要指定資料行的清單。 用於建立 FileTable 的簡單語法可讓您指定：  
  
-   目錄名稱。 在 FileTable 資料夾階層中，這個資料表層級目錄會成為在資料庫層級中指定之資料庫目錄的子系，以及儲存在資料表中之檔案或目錄的父系。  
  
-   要用於 FileTable **Name** 資料行中之檔案名稱的定序名稱。  
  
-   要用於 3 個自動建立的主索引鍵條件約束和唯一條件約束的名稱。  
  
###  <a name="HowToCreate"></a> 如何：建立 FileTable  
 **使用 Transact-SQL 建立 FileTable**  
 您可以使用 **AS FileTable** 選項來呼叫 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 陳述式，藉以建立 FileTable。 因為 FileTable 具有固定的結構描述，所以您不需要指定資料行的清單。 您可以針對新的 FileTable 指定下列設定：  
  
1.  **FILETABLE_DIRECTORY**。 指定目錄，以做為 FileTable 中儲存之所有檔案和目錄的根目錄。 在資料庫的所有 FileTable 目錄名稱之間，此名稱必須是唯一的。 不論目前的定序設定為何，唯一性的比較都不區分大小寫。  
  
    -   此值的資料類型為 **nvarchar(255)** ，並使用 **Latin1_General_CI_AS_KS_WS**的固定定序。  
  
    -   您所提供的目錄名稱必須符合有效目錄名稱的檔案系統需求。  
  
    -   在資料庫的所有 FileTable 目錄名稱之間，此名稱必須是唯一的。 不論目前的定序設定為何，唯一性的比較都不區分大小寫。  
  
    -   如果您在建立 FileTable 時未提供目錄名稱，則會使用 FileTable 本身的名稱做為目錄名稱。  
  
2.  **FILETABLE_COLLATE_FILENAME**。 指定定序名稱，用於套用至 FileTable 中的 **Name** 資料行。  
  
    1.  指定的定序必須 **不區分大小寫** ，以符合 Windows 檔案命名語意。  
  
    2.  如果您未提供 **FILETABLE_COLLATE_FILENAME**的值，或指定 **database_default**，則資料行會繼承目前資料庫的定序。 如果目前的資料庫定序區分大小寫，則會引發錯誤，而且 **CREATE TABLE** 作業會失敗。  
  
3.  您也可以指定要用於 3 個自動建立的主索引鍵條件約束和唯一條件約束的名稱。 如果您未提供名稱，則系統會產生名稱，如本主題稍後所述。  
  
    -   **FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME**  
  
    -   **FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME**  
  
    -   **FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME**  
  
 **範例**  
  
 下列範例會建立新的 FileTable，並指定 **FILETABLE_DIRECTORY** 和 **FILETABLE_COLLATE_FILENAME**的使用者定義值。  
  
```tsql  
CREATE TABLE DocumentStore AS FileTable  
    WITH (   
          FileTable_Directory = 'DocumentTable',  
          FileTable_Collate_Filename = database_default  
         );  
GO  
```  
  
 下列範例也會建立新的 FileTable。 因為未指定使用者定義值，所以 **FILETABLE_DIRECTORY** 的值會成為 FileTable 的名稱， **FILETABLE_COLLATE_FILENAME** 的值會成為 database_default，而主索引鍵和唯一條件約束則會接受系統產生的名稱。  
  
```tsql  
CREATE TABLE DocumentStore AS FileTable;  
GO  
```  
  
 **使用 SQL Server Management Studio 建立 FileTable**  
 在物件總管中，展開選取之資料庫底下的物件、以滑鼠右鍵按一下 [資料表]**** 資料夾，然後選取 [New FileTable (新增 FileTable)]****。  
  
 此選項會開啟新的指令碼視窗，其中包含您可以自訂及執行以建立 FileTable 的 Transact-SQL 指令碼範本。 使用 **[查詢]** 功能表上的 **[指定範本參數的值]** 選項，輕鬆地自訂指令碼。  
  
###  <a name="ReqCreate"></a> 建立 FileTable 的需求和限制  
  
-   您無法改變現有的資料表，以便將它轉換成 FileTable。  
  
-   先前在資料庫層級中指定的上層目錄必須具有非 Null 值。 如需指定資料庫層級目錄的相關資訊，請參閱 [啟用 FileTable 的必要條件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)。  
  
-   因為 FileTable 包含 FILESTREAM 資料行，所以 FileTable 需要使用有效的 FILESTREAM 檔案群組。 您可以選擇性地指定有效的 FILESTREAM 檔案群組，當做建立 FileTable 之 **CREATE TABLE** 命令的一部分。 如果您沒有指定檔案群組，則 FileTable 就會使用資料庫的預設 FILESTREAM 檔案群組。 如果資料庫沒有 FILESTREAM 檔案群組，則系統會引發錯誤。  
  
-   您無法將資料表條件約束建立成 **CREATE TABLE…AS FILETABLE** 陳述式的一部分。 不過，您之後可以使用 **ALTER TABLE** 陳述式來加入條件約束。  
  
-   您無法在 **tempdb** 資料庫或任何其他系統資料庫中建立 FileTable。  
  
-   您無法將 FileTable 建立成暫存資料表。  
  
##  <a name="BasicsAlter"></a> 改變 FileTable  
 因為 FileTable 具有預先定義且固定的結構描述，所以您無法加入或變更其資料行。 不過，您可以在 FileTable 中加入自訂索引、觸發程序、條件約束及其他選項。  
  
 如需使用 ALTER TABLE 陳述式啟用或停用 FileTable 命名空間 (包括系統定義的條件約束) 的相關資訊，請參閱 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)。  
  
###  <a name="HowToChange"></a> 如何：變更 FileTable 的目錄  
 **使用 Transact-SQL 變更 FileTable 的目錄**  
 呼叫 ALTER TABLE 陳述式，並提供有效的新 **FILETABLE_DIRECTORY** SET 選項值。  
  
 **範例**  
  
```tsql  
ALTER TABLE filetable_name  
    SET ( FILETABLE_DIRECTORY = N'directory_name' );  
GO  
```  
  
 **使用 SQL Server Management Studio 變更 FileTable 的目錄**  
 在物件總管中，以滑鼠右鍵按一下 [FileTable]，並選取 [屬性]**** 開啟 [資料表屬性]**** 對話方塊。 在 **[FileTable]** 頁面上，輸入 **[FileTable 目錄名稱]**的新值。  
  
###  <a name="ReqAlter"></a> 改變 FileTable 的需求和限制  
  
-   您無法改變 **FILETABLE_COLLATE_FILENAME**的值。  
  
-   您無法變更、卸除或停用 FileTable 的系統定義資料行。  
  
-   您無法將新的使用者資料行、計算資料行或已保存的計算資料行加入至 FileTable。  
  
##  <a name="BasicsDrop"></a> 卸除 FileTable  
 您可以使用 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md) 陳述式的一般語法來卸除 FileTable。  
  
 當您卸除 FileTable 時，也會一併卸除下列物件：  
  
-   也會一併卸除 FileTable 的所有資料行以及與資料表相關聯的所有物件，例如索引、條件約束及觸發程序。  
  
-   FileTable 目錄和其所含的子目錄會從資料庫的 FILESTREAM 檔案及目錄階層中消失。  
  
 如果 FileTable 的檔案命名空間中存在開啟的檔案控制代碼，DROP TABLE 命令就會失敗。 如需關閉開啟之控制代碼的相關資訊，請參閱 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)。  
  
##  <a name="BasicsOtherObjects"></a> 當您建立 FileTable 時也會建立其他資料庫物件  
 當您建立新的 FileTable 時，也會建立一些系統定義的索引和條件約束。 您不能改變或卸除這些物件，只有當 FileTable 本身卸除時它們才會消失。 若要查看這些物件的清單，請查詢目錄檢視 [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)。  
  
```tsql  
--View all objects for all filetables, unsorted  
SELECT * FROM sys.filetable_system_defined_objects;  
GO  
  
--View sorted list with friendly names  
SELECT OBJECT_NAME(parent_object_id) AS 'FileTable', OBJECT_NAME(object_id) AS 'System-defined Object'  
    FROM sys.filetable_system_defined_objects  
    ORDER BY FileTable, 'System-defined Object';  
GO  
```  
  
 **建立新 FileTable 時所建立的索引**  
 當您建立新的 FileTable 時，也會建立下列系統定義的索引：  
  
|||  
|-|-|  
|**資料行**|**索引類型**|  
|[path_locator] ASC|主索引鍵、非叢集|  
|[parent_path_locator] ASC、<br /><br /> [name] ASC|唯一、非叢集|  
|[stream_id] ASC|唯一、非叢集|  
  
 **建立新 FileTable 時所建立的條件約束**  
 當您建立新的 FileTable 時，也會建立下列系統定義的條件約束：  
  
|條件約束|強制執行|  
|-----------------|--------------|  
|下列資料行的預設條件約束：<br /><br /> creation_time<br /><br /> is_archive<br /><br /> is_directory<br /><br /> is_hidden<br /><br /> is_offline<br /><br /> is_readonly<br /><br /> is_system<br /><br /> is_temporary<br /><br /> last_access_time<br /><br /> last_write_time<br /><br /> path_locator<br /><br /> stream_id|系統定義的預設條件約束會針對指定的資料行強制執行預設值。|  
|檢查條件約束|系統定義的檢查條件約束會強制執行下列需求：<br /><br /> 有效的檔案名稱。<br /><br /> 有效的檔案屬性。<br /><br /> 父物件必須是目錄。<br /><br /> 在檔案操作期間，會鎖定命名空間階層。|  
  
 **系統定義之條件約束的命名慣例**  
 上述之系統定義條件約束的命名格式為 **\<條件約束類型>_\<資料表名稱>[\_\<資料行名稱>]\_\<唯一碼>**，其中：  
  
-   其中的 <條件約束類型>** 是 CK (檢查條件約束)、DF (預設條件約束)、FK (外部索引鍵)、PK (主索引鍵) 或 UQ (唯一條件約束)。  
  
-   *\<唯一碼>* 是讓名稱成為唯一名稱的系統產生字串。 這個字串可能會包含 FileTable 名稱和唯一識別碼。  
  
## <a name="see-also"></a>另請參閱  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  
