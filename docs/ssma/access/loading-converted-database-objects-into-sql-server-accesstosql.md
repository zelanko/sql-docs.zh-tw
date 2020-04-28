---
title: 將已轉換的資料庫物件載入 SQL Server （AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, loading converted objects into SQL Azure
- Access databases, loading converted objects into SQL Server
- data, securing
- loading objects into SQL Azure
- loading objects into SQL Server
- migrating objects into SQL Azure
- migrating objects into SQL Server
- moving objects into SQL Azure
- moving objects into SQL Server
- schemas, loading into SQL Azure
- schemas, loading into SQL Server
- scripting converted objects
- securing data
- SQL Azure, loading objects into
- SQL Server, loading objects into
- synchronizing metadata with SQL Azure
- synchronizing metadata with SQL Server
- uploading objects into SQL Azure
- uploading objects into SQL Server
ms.assetid: 4e854eee-b10c-4f0b-9d9e-d92416e6f2ba
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7effaa973b7a39df6fc0b9385a5cfde4fdad18d4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67986318"
---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>將已轉換的資料庫物件載入 SQL Server （AccessToSQL）
將 Access 資料庫物件轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 之後，您可以將產生的資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure。 您可以讓 SSMA 建立物件，也可以自行編寫物件的腳本並執行腳本。 此外，SSMA 也可讓您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫的實際內容來更新目標中繼資料。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>選擇同步處理和腳本  
如果您想要將已轉換的資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]載入或 SQL Azure 而不進行修改，您可以讓 SSMA 直接建立或重新建立資料庫物件。 該方法既快速又簡單，但不允許自訂會定義[!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件的程式碼，而不是預存程式。  
  
如果您想要修改用[!INCLUDE[tsql](../../includes/tsql-md.md)]來建立物件的，或如果您想要更充分掌控物件的建立，請使用 SSMA 來建立腳本。 接著，您可以修改這些腳本、個別建立每個物件，甚至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 Agent 來排程建立這些物件。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>使用 SSMA 與 SQL Server 同步處理物件  
若要使用 SSMA 來[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立或 sql azure 資料庫物件，請在或 Sql [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] azure 中繼資料 Explorer 中選取物件，然後同步處理物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與或 sql Azure，如下列程式所示。 根據預設，如果物件已存在或 SQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] azure 中，而且 SSMA 中繼資料有一些本機變更或這些物件定義的更新，則 SSMA 將會改變或 sql Azure 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的物件定義。 您可以藉由編輯**專案設定**來變更預設行為。  
  
> [!NOTE]  
> 您可以選取未[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從 Access 資料庫轉換的現有或 SQL Azure 資料庫物件。 不過，SSMA 不會重新建立或改變那些物件。  
  
**若要與 SQL Server 或 SQL Azure 同步處理物件**  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Sql Azure 中繼資料 Explorer 中，展開[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]頂端或 sql azure 節點，然後展開 [**資料庫**]。  
  
2.  選取要處理的物件：  
  
    -   若要同步處理完整的資料庫，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要同步處理或省略物件的個別物件或類別，請選取或清除物件或資料夾旁邊的核取方塊。  
  
3.  在您選取要在或 SQL Azure 元[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料 Explorer 中處理的物件之後，請以滑鼠右鍵按一下 [**資料庫**]，然後按一下 [**與資料庫同步處理**]。  
  
    您也可以用滑鼠右鍵按一下物件或其父資料夾，然後按一下 [**與資料庫同步處理**]，來同步處理個別物件或物件的類別。  
  
    之後，SSMA 將會顯示 [**與資料庫同步處理**] 對話方塊，您可以在其中看到兩個專案群組。 在左側，SSMA 會顯示樹狀結構中所選取的資料庫物件。 在右側，您可以看到樹狀結構，代表 SSMA 中繼資料中的相同物件。 您可以按一下右側或左邊的 [+] 按鈕，展開樹狀目錄。 同步處理的方向會顯示在這兩個樹狀結構之間的 [動作] 資料行中。  
  
    動作正負號可以有三種狀態：  
  
    -   向左箭號表示中繼資料的內容將會儲存在資料庫中（預設值）。  
  
    -   向右箭號表示資料庫內容將會覆寫 SSMA 中繼資料。  
  
    -   「交叉符號」表示不會採取任何動作。  
  
    按一下動作符號以變更狀態。 當您按一下 [**同步處理資料庫**] 對話方塊的 **[確定]** 按鈕時，就會執行實際的同步處理。  
  
## <a name="scripting-objects"></a>編寫物件腳本  
如果您想要儲存[!INCLUDE[tsql](../../includes/tsql-md.md)]已轉換之資料庫物件的定義，或想要變更物件定義並自行執行腳本，您可以將已轉換的資料庫物件定義儲存[!INCLUDE[tsql](../../includes/tsql-md.md)]至腳本。  
  
**若要將一或多個物件儲存至腳本**  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料] Explorer 中，展開最上層節點（伺服器名稱），然後展開 [**資料庫**]。  
  
2.  請進行下列任一或多項操作：  
  
    -   若要編寫完整資料庫的腳本，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要編寫或省略個別的視圖，請展開資料庫，展開 [ **views**]，然後選取或清除此視圖旁的核取方塊。  
  
    -   若要編寫或省略個別的資料表，請展開資料庫，展開 [**資料表**]，然後選取或清除資料表旁的核取方塊。  
  
    -   若要編寫或省略資料表的個別索引，請展開資料表，展開 [**索引**]，然後選取或清除索引。  
  
3.  以滑鼠右鍵按一下 [**資料庫**]，然後選取 [**另存**新檔]。  
  
    您也可以撰寫個別物件的腳本。 若要編寫物件的腳本，不論選取哪一個物件，請以滑鼠右鍵按一下物件，然後選取 [**另存**新檔] 腳本。  
  
4.  在 [**另存**新檔] 對話方塊中，找出您要儲存腳本的資料夾，在 [**檔案名**] 方塊中輸入檔案名，然後按一下 **[確定]**。  
  
    SSMA 將會附加 .sql 副檔名。  
  
### <a name="modifying-scripts"></a>修改腳本  
將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件定義儲存為腳本之後，您就可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來修改腳本。  
  
**修改腳本**  
  
1.  在 [檔案][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **** 功能表上，指向 [開啟舊檔]****，再按一下 [檔案]****。  
  
2.  在 [**開啟**] 對話方塊中，找出並選取您的腳本檔案，然後按一下 **[確定]**。  
  
3.  使用 [查詢編輯器] 來編輯腳本檔案。  
  
    如需查詢編輯器的詳細資訊，請參閱《線上叢書》中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的「編輯器便利命令和功能」。  
  
4.  若要儲存腳本，請在 [檔案] 功能表上選取 [**儲存**]。  
  
### <a name="running-scripts"></a>執行腳本  
您可以在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行腳本或個別語句。  
  
**執行指令碼**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **在 [檔案**] 功能表上，指向 [**開啟**]，**然後按一下 [** 檔案]。  
  
2.  在 [**開啟**] 對話方塊中，找出並選取您的腳本檔案，然後按一下 **[確定]**。  
  
3.  若要執行完整的腳本，請按**F5**鍵。  
  
4.  若要執行一組語句，請在 [查詢編輯器] 視窗中選取語句，然後按**F5**鍵。  
  
如需如何使用查詢編輯器來執行腳本的詳細資訊，請參閱《 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]線上叢書》 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的「查詢」。  
  
您也可以從命令列使用**sqlcmd**公用程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來執行腳本。 如需**sqlcmd**的詳細資訊，請參閱《線上叢書[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 》中的「sqlcmd 公用程式」。 如需有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的詳細資訊，請參閱《線上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]叢書》中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的「自動化管理工作（代理程式）」。  
  
## <a name="securing-objects-in-sql-server"></a>保護 SQL Server 中的物件  
將已轉換的資料庫物件載入之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您就可以授與和拒絕那些物件的許可權。 在將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，最好先執行此動作。 如需如何在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]協助保護物件的詳細資訊，請參閱《線上叢書》中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的「資料庫和資料庫應用程式的安全性考慮」。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是將[資料移轉至 SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
