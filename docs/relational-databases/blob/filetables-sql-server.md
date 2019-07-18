---
title: FileTables (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], overview
- FileTables [SQL Server]
- FileTable [SQL Server], see FileTables [SQL Server]
- FileTable [SQL Server]
ms.assetid: a57b629c-e9ed-48fd-9a48-ed3787d80c8f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 66af409c92de623d4470b066f59f7fd7bab6aa5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822353"
---
# <a name="filetables-sql-server"></a>FileTable (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FileTable 功能可將 Windows 檔案命名空間的支援以及與 Windows 應用程式的相容性提供給儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的檔案資料。 FileTable 可讓應用程式整合其儲存和資料管理元件，並且透過非結構化資料和中繼資料提供整合式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務 (包含全文檢索搜尋和語意搜尋)。  
  
 換句話說，您可以將檔案和文件儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特殊資料表 (稱為 FileTable) 中，而從 Windows 應用程式存取它們，就像它們儲存在檔案系統中一樣，並不需要對用戶端應用程式進行任何變更。  
  
 FileTable 功能是根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FILESTREAM 技術所建立。 若要深入了解 FILESTREAM，請參閱 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)。  
  
##  <a name="Goals"></a> FileTable 功能的優點  
 FileTable 功能的目標包括：  
  
-   儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫內檔案資料的 Windows API 相容性。 Windows API 相容性包括下列項目：  
  
    -   FILESTREAM 資料的非交易式資料流存取和就地更新。  
  
    -   目錄和檔案的階層式命名空間。  
  
    -   檔案屬性的儲存，例如建立日期和修改日期。  
  
    -   Windows 檔案和目錄管理 API 的支援。  
  
-   與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的相容性，包括針對 FILESTREAM 和檔案屬性資料進行的管理工具、服務和關聯式查詢功能。  
  
 因此，FileTable 會移除一道重大障礙，可讓您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來儲存和管理目前位於檔案伺服器上之檔案的非結構化資料。 企業可以將這項資料從檔案伺服器移入 FileTable，以便運用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所提供的整合式管理和服務。 同時，企業可以針對將這項資料視為檔案系統中之檔案的現有 Windows 應用程式，維持 Windows 應用程式相容性。  
 
  
##  <a name="Description"></a> 何謂 FileTable  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對於需要將檔案和目錄儲存在資料庫中、具備 Windows API 相容性和非交易式存取的應用程式而言，提供特殊的 **檔案資料表**(也稱為 **FileTable**)。 FileTable 是包含預先定義結構描述的特殊化使用者資料表，可儲存 FILESTREAM 資料、檔案和目錄階層資訊，以及檔案屬性。  
  
 FileTable 提供了下列功能：  
  
-   FileTable 代表目錄和檔案的階層。 它會儲存與該階層中所有節點相關的資料 (目錄以及它們所包含的檔案)。 這個階層是從您建立 FileTable 時指定的根目錄開始。  
  
-   FileTable 中的每個資料列都代表一個檔案或目錄。  
  
-   每個資料列都包含下列項目。 如需 FileTable 結構描述的詳細資訊，請參閱 [FileTable 結構描述](../../relational-databases/blob/filetable-schema.md)。  
  
    -   資料流資料的 **file_stream** 資料行和 **stream_id** (GUID) 識別碼。 (目錄的 **file_stream** 資料行為 NULL)。  
  
    -   用於代表和維護目前項目 (檔案或目錄) 與目錄階層的 **path_locator** 和 **parent_path_locator** 資料行。  
  
    -   檔案 I/O API 可用的 10 個檔案屬性，例如建立日期和修改日期。  
  
    -   支援針對檔案和文件進行全文檢索搜尋和語意搜尋的類型資料行。  
  
-   FileTable 會強制執行特定系統定義的條件約束和觸發程序來維護檔案命名空間語意。  
  
-   當您針對非交易式存取設定資料庫時，就會透過針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所設定的 FILESTREAM 共用來公開以 FileTable 表示的檔案和目錄階層。 這會提供 Windows 應用程式的檔案系統存取。  
  
 FileTable 的某些其他特性包括：  
  
-   儲存在 FileTable 中的檔案和目錄資料會透過 Windows API 架構應用程式之非交易式檔案存取的 Windows 共用公開。 針對 Windows 應用程式，這看起來就像含有其檔案和目錄的一般共用。 應用程式可以使用一組豐富的 Windows API，來管理此共用下的檔案和目錄。  
  
-   透過此共用顯示的目錄階層就是在 FileTable 內部維護的單純邏輯目錄結構。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件會攔截透過 Windows 共用建立或變更檔案或目錄的呼叫，然後將它們反映在 FileTable 的對應關聯式資料中。  
  
-   Windows API 作業的本質為非交易式，而且並未與使用者交易相關聯。 不過，系統完全支援儲存在 FileTable 中之 FILESTREAM 資料的交易式存取，就如同一般資料表中的任何 FILESTREAM 資料行。  
  
-   FileTable 也可以透過一般 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取進行查詢和更新。 它們也會與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具和備份等功能整合。  

-   您無法透過 dbmail 傳送電子郵件要求，且無法附加位於 Filestream 目錄的檔案 (也因此無法附加位於 FileTable 的檔案)。 檔案系統篩選驅動程式 RsFx0420 會檢查進入和離開 Filestream 資料夾的傳入 I/O 要求。 若要求並非來自 SQLServer 可執行檔及 Filesteam 程式碼，它們會明確遭到拒絕。
  
##  <a name="additional"></a> 使用 FileTable 的額外考量  
  
###  <a name="DBA"></a> 管理考量  
 **關於 FILESTREAM 和 FileTable**  
  
-   您可以分別設定 FileTable 與 FILESTREAM。 因此，您可以繼續使用 FILESTREAM 功能，而不需要啟用非交易式存取或建立 FileTable。  
  
-   除了透過 FileTable 以外，沒有 FILESTREAM 資料的非交易式存取。 因此，當您啟用非交易式存取時，並不會影響現有 FILESTREAM 資料行和應用程式的行為。  
  
 **關於 FileTable 和非交易式存取**  
  
-   您可以在資料庫層級中啟用或停用非交易式存取。  
  
-   您可以在資料庫層級中設定或微調非交易式存取，方法是關閉它，或是啟用唯讀或完整讀取/寫入存取。  
   
###  <a name="memory"></a> FileTable 不支援記憶體對應檔案  
 FileTable 不支援記憶體對應檔案。 記事本和小畫家是使用記憶體對應檔案的兩個常見的應用程式例子。 不能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的電腦上使用這些應用程式來開啟儲存在 FileTable 中的檔案。 但是，可以從遠端電腦使用這些應用程式來開啟儲存在 FileTable 中的檔案，因為在這些情況下不使用記憶體對應功能。  
   
##  <a name="reltasks"></a> 相關工作  
 [啟用 FileTable 的必要條件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
 描述如何啟用建立和使用 FileTable 的必要元件。  
  
 [建立、改變及卸除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
 描述如何建立新的 FileTable，或是改變或卸除現有的 FileTable。  
  
 [載入檔案至 FileTable](../../relational-databases/blob/load-files-into-filetables.md)  
 描述如何載入或移轉檔案至 FileTable 中。  
  
 [使用 FileTable 中的目錄與路徑](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
 描述在 FileTable 中儲存檔案的目錄結構。  
  
 [利用 Transact-SQL 存取 FileTable](../../relational-databases/blob/access-filetables-with-transact-sql.md)  
 描述 Transact-SQL 資料操作語言 (DML) 命令如何與 FileTable 搭配運作。  
  
 [使用檔案輸入輸出 API 存取 FileTable](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
 描述檔案系統 I/O 如何在 FileTable 上運作。  
  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
 描述用於管理 FileTable 的常見管理工作。  
  
##  <a name="relcontent"></a> 相關內容  
 [FileTable 結構描述](../../relational-databases/blob/filetable-schema.md)  
 描述 FileTable 預先定義且固定的結構描述。  
  
 [FileTable 與其他 SQL Server 功能的相容性](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)  
 描述 FileTable 如何搭配其他的 SQL Server 功能一起運作。  
  
 [FileTable DDL、函數、預存程序及檢視](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
 列出已加入或變更以支援 FileTable 功能的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件。  

## <a name="see-also"></a>另請參閱
[Filestream 及 FileTable 動態管理檢視 (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 目錄檢視 (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Filestream 和 FileTable 系統預存程序 (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)


  
  
