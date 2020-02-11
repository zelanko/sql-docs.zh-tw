---
title: 將已轉換的資料庫物件載入 SQL Server （OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 97c34beb0cbe27e8d3c88b922690dc369fb7103b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68262992"
---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>將轉換的資料庫物件載入 SQL Server (OracleToSQL)
將 Oracle 架構轉換成 SQL Server 之後，您就可以將產生的資料庫物件載入 SQL Server。 您可以讓 SSMA 建立物件，也可以自行編寫物件的腳本並執行腳本。 此外，SSMA 也可讓您使用 SQL Server 資料庫的實際內容來更新目標中繼資料。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>選擇同步處理和腳本  
如果您想要將轉換的資料庫物件載入 SQL Server 而不進行修改，您可以讓 SSMA 直接建立或重新建立資料庫物件。 該方法既快速又簡單，但不允許自訂可定義 SQL Server [!INCLUDE[tsql](../../includes/tsql-md.md)]物件的程式碼，而不是預存程式。  
  
如果您想要修改用[!INCLUDE[tsql](../../includes/tsql-md.md)]來建立物件的，或如果您想要更充分掌控物件的建立，請使用 SSMA 來建立腳本。 接著，您可以修改這些腳本、個別建立每個物件，甚至使用 SQL Server Agent 來排程建立這些物件。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>使用 SSMA 與 SQL Server 同步處理物件  
若要使用 SSMA 來建立 SQL Server 資料庫物件，請在 SQL Server Metadata Explorer 中選取物件，然後與 SQL Server 同步處理物件，如下列程式所示。 根據預設，如果物件已存在 SQL Server 中，而且 SSMA 中繼資料比 SQL Server 中的物件新，SSMA 將會改變 SQL Server 中的物件定義。 您可以藉由編輯**專案設定**來變更預設行為。  
  
> [!NOTE]  
> 您可以選取尚未從 Oracle 資料庫轉換的現有 SQL Server 資料庫物件。 不過，SSMA 不會重新建立或改變那些物件。  
  
**若要使用 SQL Server 同步處理物件**  
  
1.  在 SQL Server 中繼資料 Explorer] 中，展開頂端 SQL Server 節點，然後展開 [**資料庫**]。  
  
2.  選取要處理的物件：  
  
    -   若要同步處理完整的資料庫，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要同步處理或省略物件的個別物件或類別，請選取或清除物件或資料夾旁邊的核取方塊。  
  
3.  在 SQL Server 中繼資料 Explorer 中選取要處理的物件之後，以滑鼠右鍵按一下 [**資料庫**]，然後按一下 [**與資料庫同步處理**]。  
  
    您也可以用滑鼠右鍵按一下物件或其父資料夾，然後按一下 [**與資料庫同步處理**]，來同步處理個別物件或物件的類別。  
  
    之後，SSMA 將會顯示 [**與資料庫同步處理**] 對話方塊，您可以在其中看到兩個專案群組。 在左側，SSMA 會顯示樹狀結構中所選取的資料庫物件。 在右側，您可以看到樹狀結構，代表 SSMA 中繼資料中的相同物件。 您可以按一下右側或左邊的 [+] 按鈕，展開樹狀目錄。 同步處理的方向會顯示在這兩個樹狀結構之間的 [動作] 資料行中。  
  
    動作正負號可以有三種狀態：  
  
    -   向左箭號表示中繼資料的內容將會儲存在資料庫中（預設值）。  
  
    -   向右箭號表示資料庫內容將會覆寫 SSMA 中繼資料。  
  
    -   「交叉符號」表示不會採取任何動作。  
  
按一下動作符號以變更狀態。 當您按一下 [**同步處理資料庫**] 對話方塊的 **[確定]** 按鈕時，就會執行實際的同步處理。  
  
## <a name="scripting-objects"></a>編寫物件腳本  
若要[!INCLUDE[tsql](../../includes/tsql-md.md)]儲存已轉換之資料庫物件的定義，或變更物件定義並自行執行腳本，您可以將已轉換的資料庫物件定義[!INCLUDE[tsql](../../includes/tsql-md.md)]儲存至腳本。  
  
**將物件儲存為腳本**  
  
1.  選取要儲存到腳本的物件之後，以滑鼠右鍵按一下 [**資料庫**]，然後按一下 [**另存**新檔]。  
  
    您也可以用滑鼠右鍵按一下物件或其上層資料夾，然後按一下 [**另存**新檔]，來撰寫個別物件或物件類別的腳本。  
  
2.  在 [**另存**新檔] 對話方塊中，找出您想要儲存腳本的資料夾，在 [**檔案名**] 方塊中輸入檔案名，然後按一下 [確定 SSMA 將附加 .sql 副檔名。  
  
### <a name="modifying-scripts"></a>修改腳本  
將 SQL Server 物件定義儲存為一或多個腳本之後，您就可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來查看和修改腳本。  
  
**修改腳本**  
  
1.  在 [檔案][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **** 功能表上，指向 [開啟舊檔]****，再按一下 [檔案]****。  
  
2.  在 [**開啟**] 對話方塊中，選取您的腳本檔案，然後按一下 [確定]。
  
3.  使用 [查詢編輯器] 來編輯腳本檔案。  
  
    如需查詢編輯器的詳細資訊，請參閱 SQL Server 線上叢書中的「編輯器便利命令和功能」。  
  
4.  若要儲存腳本，請按一下 [檔案] 功能表上的 [**儲存**]。  
  
### <a name="running-scripts"></a>執行腳本  
您可以在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行腳本或個別語句。  
  
**執行指令碼**  
  
1.  在 [檔案][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **** 功能表上，指向 [開啟舊檔]****，再按一下 [檔案]****。  
  
2.  在 [**開啟**] 對話方塊中，選取您的腳本檔案，然後按一下 [確定]。  
  
3.  若要執行完整的腳本，請按**F5**鍵。  
  
4.  若要執行一組語句，請在 [查詢編輯器] 視窗中選取語句，然後按**F5**鍵。  
  
如需如何使用查詢編輯器來執行腳本的詳細資訊，請參閱[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL Server 線上叢書中的「查詢」。  
  
您也可以從命令列使用**sqlcmd**公用程式和 SQL Server Agent 來執行腳本。 如需**sqlcmd**的詳細資訊，請參閱 SQL Server 線上叢書中的「Sqlcmd 公用程式」。 如需 SQL Server Agent 的詳細資訊，請參閱 SQL Server 線上叢書中的「自動化管理工作（SQL Server Agent）」。  
  
## <a name="securing-objects-in-sql-server"></a>保護 SQL Server 中的物件  
將已轉換的資料庫物件載入 SQL Server 之後，您就可以授與和拒絕那些物件的許可權。 在將資料移轉至 SQL Server 之前，最好先執行此動作。 如需如何在 SQL Server 中協助保護物件的詳細資訊，請參閱 SQL Server 線上叢書中的「資料庫和資料庫應用程式的安全性考慮」。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是將[資料移轉至 SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Oracle 資料庫移轉至 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
