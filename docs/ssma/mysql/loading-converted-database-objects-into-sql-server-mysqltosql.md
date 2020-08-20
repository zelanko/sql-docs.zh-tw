---
description: 將轉換的資料庫物件載入 SQL Server (MySQLToSQL)
title: 將轉換的資料庫物件載入 SQL Server (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 87960d05db8a12ebd7a8751f46c90a256ce73313
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463392"
---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>將轉換的資料庫物件載入 SQL Server (MySQLToSQL)
將 MySQL 資料庫轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql azure 之後，您可以將產生的資料庫物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sql azure。 您可以讓 SSMA 建立物件，也可以編寫物件的腳本，並自行執行腳本。 此外，SSMA 還可讓您以的實際內容或 Azure SQL Database 來更新目標中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>在同步處理和腳本之間進行選擇  
如果您想要將轉換的資料庫物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 而不進行修改，您可以讓 SSMA 直接建立或重新建立資料庫物件。 這種方法既快速又簡單，但不允許自訂定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 物件的 transact-sql 程式碼。  
  
如果您想要修改用來建立物件的 Transact-sql，或如果您想要更充分掌控建立的物件，請使用 SSMA 來建立腳本。 然後，您可以修改這些腳本、個別建立每個物件，甚至使用 SQL Server Agent 排程建立這些物件。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>使用 SSMA 與 SQL Server 同步處理物件  
若要使用 SSMA 來建立 SQL Server 或 Azure SQL Database 物件，請在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql Azure 中繼資料瀏覽器中選取物件，然後將物件與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sql azure 同步處理，如下列程式所示。 依預設，如果物件已存在於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL azure 中，且 SSMA 中繼資料對這些物件的定義有一些本機變更或更新，則 SSMA 會改變或 Sql Azure 中的物件定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以藉由編輯 **專案設定**來變更預設行為。  
  
> [!NOTE]  
> 您可以選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未從 MySQL 資料庫轉換的現有或 Azure SQL Database 物件。 但是，SSMA 不會重新建立或改變這些物件。  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>若要同步處理物件與 SQL Server 或 SQL Azure  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql Azure 中繼資料瀏覽器中，展開頂端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sql azure 節點，然後展開 [ **資料庫**]。  
  
2.  選取要處理的物件：  
  
    -   若要同步處理完整的資料庫，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要同步處理或省略物件的個別物件或類別，請選取或清除物件或資料夾旁邊的核取方塊。  
  
3.  在 SQL Server 或 SQL Azure 中繼資料瀏覽器中選取要處理的物件之後，以滑鼠右鍵按一下 [ **資料庫**]，然後按一下 [ **同步處理資料庫**]。  
  
    您也可以在物件或其父資料夾上按一下滑鼠右鍵，然後按一下 [ **與資料庫同步**處理]，以同步處理個別物件或物件的類別。  
  
    之後，SSMA 會顯示 [ **同步處理資料庫** ] 對話方塊，您可以在其中看到兩個專案群組。 SSMA 會在左側顯示樹狀結構中所選取的資料庫物件。 您可以在右側看到樹狀結構，代表 SSMA 中繼資料中的相同物件。 您可以按一下右邊或左邊的 [+] 按鈕來展開樹狀結構。 同步處理的方向會顯示在兩個樹狀結構之間的 [動作] 資料行中。  
  
    動作符號可以處於下列三種狀態：  
  
    -   向左箭號表示中繼資料的內容會儲存在資料庫中， (預設) 。  
  
    -   向右箭號表示資料庫內容會覆寫 SSMA 中繼資料。  
  
    -   交叉符號表示不會採取任何動作。  
  
    -   按一下動作符號以變更狀態。 當您按一下 [**同步處理資料庫**] 對話方塊的 **[確定]** 按鈕時，將會執行實際的同步處理。  
  
## <a name="scripting-objects"></a>編寫物件腳本  
若要儲存已 [!INCLUDE[tsql](../../includes/tsql-md.md)] 轉換之資料庫物件的定義，或自行改變物件定義和執行腳本，您可以將已轉換的資料庫物件定義儲存至 [!INCLUDE[tsql](../../includes/tsql-md.md)] 腳本。  
  
**將物件儲存為腳本**  
  
1.  當您選取要儲存至腳本的物件之後，請以滑鼠右鍵按一下 [ **資料庫**]，然後按一下 [ **另存為腳本**]。  
  
    您也可以用滑鼠右鍵按一下物件或其父資料夾，然後按一下 [ **另存為腳本**]，以編寫個別物件或物件類別的腳本。  
  
2.  在 [ **另存** 新檔] 對話方塊中，找出您想要儲存腳本的資料夾，在 [ **檔案名** ] 方塊中輸入檔案名，然後 [!INCLUDE[clickOK](../../includes/clickok-md.md)] SSMA 會附加 .sql 的副檔名。  
  
### <a name="modifying-scripts"></a>修改腳本  
將 SQL Server 或 SQL Azure 物件定義儲存為腳本之後，您可以使用 SQL Server Management Studio 來修改腳本。  
  
**若要修改腳本**  
  
1.  在 **Management Studio 的** [檔案] 功能表上，指向 [ **開啟**]， **然後按一下 [** 檔案]。  
  
2.  在 [開啟] 對話方塊中，找出並選取您的腳本檔案，然後按一下 **[確定]**。  
  
3.  使用 [查詢編輯器] 編輯腳本檔。如需查詢編輯器的詳細資訊，請參閱 SQL Server 線上叢書中的「編輯器的便利性命令和功能」。  
  
4.  若要儲存腳本，請在 [檔案] 功能表上選取 [ **儲存**]。  
  
### <a name="running-scripts"></a>執行腳本  
您可以在 SQL Server Management Studio 中執行腳本或個別語句。  
  
**執行指令碼**  
  
1.  在 **SQL Server Management Studio 的** [檔案] 功能表上，指向 [ **開啟** ]， **然後按一下 [** 檔案]。  
  
2.  在 [開啟] 對話方塊中，找出並選取您的腳本檔案，然後按一下 **[確定]**。  
  
3.  若要執行完整的腳本，請按 **F5** 鍵。  
  
4.  若要執行一組語句，請在 [查詢編輯器] 視窗中選取語句，然後按 **F5** 鍵。  
  
5.  如需如何使用查詢編輯器來執行腳本的詳細資訊，請參閱 SQL Server 線上叢書中的「SQL Server Management Studio Transact-SQL 查詢」。  
  
6.  您也可以使用 **sqlcmd** 公用程式從命令列執行腳本，也可以從 SQL Server Agent 執行腳本。 如需 **sqlcmd**的詳細資訊，請參閱 SQL Server 線上叢書中的「Sqlcmd 公用程式」。 如需 SQL Server Agent 的詳細資訊，請參閱 SQL Server 線上叢書中的「自動化管理工作 (SQL Server Agent) 」。  
  
## <a name="securing-objects-in-sql-server"></a>保護 SQL Server 中的物件  
將轉換的資料庫物件載入 SQL Server 之後，您可以授與和拒絕這些物件的許可權。 最好先完成這項作業，再將資料移轉至 SQL Server。 如需如何協助保護 SQL Server 中物件的相關資訊，請參閱 SQL Server 線上叢書中的「資料庫和資料庫應用程式的安全性考慮」。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是將 [MySQL 資料移轉至 SQL Server Azure SQL Database &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料庫遷移至 SQL Server Azure SQL Database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
