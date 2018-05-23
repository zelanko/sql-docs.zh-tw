---
title: 記憶體內部 OLTP 的 SQL Server Management Studio 支援 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ee847b5f-6a1a-448e-a746-d61a023881ff
caps.latest.revision: 31
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3ddd883651796b31d1cc8745df47a9e0eb44bc7b
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="sql-server-management-studio-support-for-in-memory-oltp"></a>SQL Server Management Studio 對記憶體中 OLTP 的支援
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 是用於管理您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基礎結構的整合式環境。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供工具來設定、監視以及管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 如需詳細資訊，請參閱 [SQL Server Management Studio](http://msdn.microsoft.com/library/66a6b7b1-de6a-4161-82bd-98ded486947b)  
  
 本主題中的工作描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 管理記憶體最佳化資料表、記憶體最佳化資料表上的索引、原生編譯預存程序，以及使用者定義的記憶體最佳化資料表類型。  
  
 如需有關如何以程式設計方式建立記憶體最佳化資料表的詳細資訊，請參閱 [建立記憶體最佳化資料表和原生編譯的預存程序](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)。  
  
### <a name="to-create-a-database-with-a-memory-optimized-data-filegroup"></a>若要建立具有記憶體最佳化資料檔案群組的資料庫  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine 的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [資料庫]，然後按一下 [新增資料庫]。  
  
3.  請按一下 [檔案群組] 頁面，以新增記憶體最佳化的資料檔案群組。 在 [記憶體最佳化資料] 下，按一下 [新增檔案群組]，然後輸入記憶體最佳化資料檔案群組的名稱。  標示為 [FILESTREAM 檔案] 的欄代表檔案群組中的容器數目。 容器是在 [一般] 頁面上加入的。  
  
4.  按一下 [一般] 頁面，將檔案 (容器) 加入檔案群組中。 在 [資料庫檔案] 下，按一下 [新增]。 將 [檔案類型] 選取為 [FILESTREAM 資料]、指定容器的邏輯名稱、選取記憶體最佳化檔案群組，並且確定 [自動成長/大小上限] 設定為 [無限制]。  
  
     如需如何使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]建立新資料庫的詳細資訊，請參閱[建立資料庫](../../relational-databases/databases/create-a-database.md)。  
  
### <a name="to-create-a-memory-optimized-table"></a>若要建立記憶體最佳化的資料表  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下資料庫的 [資料表] 節點，再按一下 [新增]，然後按一下 [記憶體最佳化的資料表]。  
  
     隨即顯示建立記憶體最佳化資料表的範本。  
  
2.  若要取代範本參數，請在 [查詢] 功能表上，按一下 [指定範本參數的值]。  
  
     如需有關如何使用範本的詳細資訊，請參閱[範本總管](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8)。  
  
3.  在 [物件總管] 中，資料表的排序是先按照磁碟資料表，然後再按照記憶體最佳化資料表。 您可以使用 [物件總管詳細資料]查看所有按照名稱排序的資料表。  
  
### <a name="to-create-a-natively-compiled-stored-procedure"></a>若要建立原生編譯的預存程序  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下資料庫的 [預存程序] 節點，再按一下 [新增]，然後按一下 [原生編譯的預存程序]。  
  
     建立原生編譯預存程序的範本會顯示。  
  
2.  若要取代範本參數，請在 [查詢] 功能表上，按一下 [指定範本參數的值]  
  
     如需有關如何建立新的預存程序的詳細資訊，請參閱[建立預存程序](../../relational-databases/stored-procedures/create-a-stored-procedure.md)。  
  
### <a name="to-create-a-user-defined-memory-optimized-table-type"></a>若要建立使用者定義的記憶體最佳化資料表類型  
  
1.  在 [物件總管]**物件總管** 中，展開資料庫的 [類型] 節點，以滑鼠右鍵按一下 [使用者定義資料表類型] 節點，按一下 [新增]，然後按一下 [使用者定義的記憶體最佳化資料表類型]。  
  
     建立使用者定義的記憶體最佳化資料表類型的範本隨即顯示。  
  
2.  若要取代範本參數，請在 [查詢] 功能表上，按一下 [指定範本參數的值]。  
  
     如需有關如何建立新的預存程序的詳細資訊，請參閱 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)。  
  
## <a name="memory-monitoring"></a>記憶體監視  
  
#### <a name="view-memory-usage-by-memory-optimized-objects-report"></a>檢視依記憶體最佳化物件的記憶體使用量報表  
  
-   在 [物件總管] 中，以滑鼠右鍵按一下資料庫，再按一下 [報表]，並按一下 [標準報表]，然後按一下 [依記憶體最佳化物件的記憶體使用量]。  
  
     此報表會提供資料庫中，記憶體最佳化物件使用之記憶體空間的詳細資料。  
  
#### <a name="view-properties-for-allocated-and-used-memory-for-a-table-database"></a>檢視資料表、資料庫之「配置的記憶體」與「使用的記憶體」的屬性  
  
1.  若要取得記憶體中使用量的相關資訊：  
  
    -   在 [物件總管] 中，以滑鼠右鍵按一下記憶體最佳化的資料表，按一下 [屬性]，然後按一下 [儲存體] 頁面。 [資料空間] 屬性的值表示資料表資料所用的記憶體。 [索引空間] 屬性的值表示資料表索引所用的記憶體。  
  
    -   在 [物件總管] 中，以滑鼠右鍵按一下資料庫，按一下 [屬性]，然後按一下 [一般] 頁面。 [配置給記憶體最佳化物件的記憶體] 屬性的值表示配置給資料庫中記憶體最佳化物件的記憶體。 [由記憶體最佳化物件所使用的記憶體] 屬性的值表示資料庫中記憶體最佳化物件所用的記憶體。  
  
## <a name="supported-features-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>下列項目所支援的功能： [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 支援具有最佳化資料的檔案群組、記憶體最佳化的資料表、索引與原生編譯的預存程序之資料庫的 Database Engine 所支援的功能和作業。  
  
 下列 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 功能已針對資料庫、資料表、預存程序、使用者定義資料表類型或索引物件更新或擴充，可支援 In-Memory OLTP。  
  
-   物件總管  
  
    -   操作功能表  
  
    -   篩選設定  
  
    -   編寫組件的指令碼為  
  
    -   工作  
  
    -   報表  
  
    -   屬性  
  
    -   資料庫工作：  
  
        -   附加和卸離包含記憶體最佳化資料表的資料庫。  
  
             [附加資料庫] 使用者介面並不會顯示記憶體最佳化的資料檔案群組。 不過，您還是可以附加資料庫，而且將能正確地附加資料庫。  
  
            > [!NOTE]  
            >  如果您要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 附加有記憶體最佳化資料檔案群組容器的資料庫，而且在另一部電腦上建立資料庫的記憶體最佳化資料檔案群組容器，這兩部電腦上記憶體最佳化資料檔案群組容器的位置必須相同。 若您希望資料庫的記憶體最佳化資料檔案群組容器的位置在新的電腦上有不同的位置，您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 附加資料庫。 在下列範例中，新的電腦上記憶體最佳化資料檔案群組容器的位置為 C:\Folder2。 但是，原本在第一部電腦上建立記憶體最佳化資料檔案群組容器的位置是 C:\Folder1。  
            >   
            >  `CREATE DATABASE[imoltp] ON`  
            >   
            >  `(NAME =N'imoltp',FILENAME=N'C:\Folder2\imoltp.mdf'),`  
            >   
            >  `(NAME =N'imoltp_mod1',FILENAME=N'C:\Folder2\imoltp_mod1'),`  
            >   
            >  `(NAME =N'imoltp_log',FILENAME=N'C:\Folder2\imoltp_log.ldf')`  
            >   
            >  `FOR ATTACH`  
            >   
            >  `GO`  
  
        -   產生指令碼。  
  
             在 [產生和發佈指令碼精靈] 中，[檢查物件是否存在] 指令碼選項的預設值為 FALSE。 如果精靈的 [設定指令碼編寫選項] 畫面將 [檢查物件是否存在] 指令碼選項的值設為 TRUE，則產生的指令碼會包含 "CREATE PROCEDURE <procedure_name> AS" 和 "ALTER PROCEDURE <procedure_name> <procedure_definition>"。 在執行時，產生的指令碼將傳回錯誤，因為原生編譯預存程序不支援 ALTER PROCEDURE。  
  
             若要變更每一個原生編譯預存程序其產生的指令碼：  
  
            1.  將 "CREATE PROCEDURE <procedure_name> AS" 中的 "AS" 取代成 "<procedure_definition>"。  
  
            2.  刪除 "ALTER PROCEDURE <procedure_name> <procedure_definition>"。  
  
        -   複製資料庫。 對於具有記憶體最佳化之物件的資料庫，交易時不會在目的伺服器上建立資料庫及傳送資料。  
  
        -   匯入和匯出資料。 使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈] 的 [從一個或多個資料表或檢視表複製資料] 選項。 如果目的地資料表是不存在於目的地資料庫中的記憶體最佳化資料表：  
  
            1.  在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈] 的 [指定資料表複製或查詢] 畫面，選取 [從一個或多個資料表或檢視表複製資料]。 然後按一下 [下一步]。  
  
            2.  按一下 [編輯對應]。 然後選取 [建立目的資料表] 並按一下 [編輯 SQL]。 輸入 CREATE TABLE 語法，在目的地資料庫上建立記憶體最佳化的資料表。 按一下 [確定] 並完成此精靈中的其餘步驟。  
  
        -   維護計畫。 記憶體最佳化資料表與其索引上不支援辨識索引和重建索引這兩項維護工作。 因此，當重建索引和辨識索引的維護計畫執行時，就會省略所選取資料庫中的記憶體最佳化資料表及其索引。  
  
             記憶體最佳化資料表及其索引上的範例掃描不支援更新統計資料維護工作。 因此，當更新統計資料的維護計畫執行時，記憶體最佳化資料表及其索引的統計資料就會一律更新至 **WITH FULLSCAN, NORECOMPUTE**。  
  
-   物件總管詳細資料窗格  
  
-   範本總管  
  
## <a name="unsupported-features-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>不為下列項目所支援的功能： [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 對於記憶體中 OLTP 物件， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 不支援 Database Engine 所不支援的功能和作業。  
  
 如需有關不支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的詳細資訊，請參閱 [記憶體內部 OLTP 不支援的 SQL Server 功能](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體中 OLTP 的 SQL Server 支援](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  
