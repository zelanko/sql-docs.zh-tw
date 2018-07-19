---
title: 載入已轉換成 SQL Server (AccessToSQL) 資料庫物件 |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d3b0b450ffacaf547a537531ae45b51a5a79d5db
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773724"
---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>載入已轉換成 SQL Server (AccessToSQL) 資料庫物件
轉換到存取資料庫物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您可以載入到產生的資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以讓 SSMA 建立物件，或您可以編寫物件指令碼，並自行執行指令碼。 此外，SSMA 可讓您更新目標中繼資料的實際內容[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步處理和指令碼之間選擇  
如果您想要轉換的資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，而不需修改，您可以擁有 SSMA 直接建立或重新建立資料庫物件。 該方法是快速且容易使用，但不允許的自訂[!INCLUDE[tsql](../../includes/tsql_md.md)]定義程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的物件，預存程序之外。  
  
如果您想要修改[!INCLUDE[tsql](../../includes/tsql_md.md)]用來建立物件，或如果您想要更充分掌控物件建立時，使用 SSMA 建立指令碼。 您即可修改這些指令碼、 個別建立每個物件或甚至使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Agent 來排程建立這些物件。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>若要同步處理的物件與 SQL Server 使用 SSMA  
要用來建立 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫物件，您選取的物件中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管，然後同步處理的物件與[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，如下列程序中所示。 根據預設，如果物件已存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，而且若 SSMA 中繼資料有一些本機變更或更新至這些非常的物件，定義則 SSMA 會改變中的物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以變更預設行為，藉由編輯**專案設定**。  
  
> [!NOTE]  
> 您可以選取現有的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或未轉換從 Access 資料庫的 SQL Azure 資料庫物件。 不過，SSMA 會無法重新建立或改變這些物件。  
  
**SQL Server 或 SQL Azure 與同步處理物件**  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管，展開最上層[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 節點，然後展開**資料庫**。  
  
2.  選取要處理的物件：  
  
    -   若要同步處理完整的資料庫，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要同步處理，或省略個別物件或類別目錄的物件，選取或清除的物件或資料夾旁邊的核取方塊。  
  
3.  選取要處理中的物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管]，以滑鼠右鍵按一下**資料庫**，然後按一下 [**同步處理資料庫**。  
  
    您也可同步個別物件或類別目錄的物件，該物件或其父資料夾上按一下滑鼠右鍵，然後按一下**同步處理資料庫**。  
  
    之後，將會顯示 SSMA**同步處理資料庫**對話方塊中，您可以在其中看到兩個群組的項目。 在左邊，SSMA 會顯示選取的資料庫物件，代表在樹狀目錄中。 在右側，您可以看到代表 SSMA 中繼資料中的相同物件的樹狀結構。 您可以展開樹狀目錄，按一下向左或向 ' +' 按鈕。 放置於兩個樹系之間的 [動作] 欄會顯示同步處理方向。  
  
    動作符號可以是三種狀態：  
  
    -   向左箭號表示中繼資料的內容將會儲存在資料庫 （預設值）。  
  
    -   向右箭號表示資料庫的內容將會覆寫的 SSMA 中繼資料。  
  
    -   跨號表示將會採取任何動作。  
  
    按一下動作正負號，以變更狀態。 將會執行實際的同步處理，當您按一下**確定**按鈕**同步處理資料庫**對話方塊。  
  
## <a name="scripting-objects"></a>編寫物件指令碼  
如果您想要儲存[!INCLUDE[tsql](../../includes/tsql_md.md)]定義的轉換後的資料庫物件，或您想要變更的物件定義和執行指令碼自行，您可以儲存轉換的資料庫物件定義要[!INCLUDE[tsql](../../includes/tsql_md.md)]指令碼。  
  
**若要將一個或多個物件儲存到指令碼**  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管，展開最上層節點 （伺服器名稱），然後展開**資料庫**。  
  
2.  請進行下列任一或多項操作：  
  
    -   若要編寫指令碼的完整的資料庫，選取資料庫名稱旁邊的核取方塊。  
  
    -   若要編寫指令碼，或省略個別的檢視，展開資料庫，展開 [**檢視**，然後選取或清除檢視] 旁的核取方塊。  
  
    -   若要編寫指令碼或省略個別資料表中，展開資料庫，展開 **資料表**，然後選取或清除資料表旁的核取方塊。  
  
    -   若要編寫指令碼，或省略資料表的個別索引，將資料表展開，展開 **索引**，然後選取或清除索引。  
  
3.  以滑鼠右鍵按一下**資料庫**選取**將儲存為指令碼**。  
  
    您也可以編寫個別物件。 若要編寫指令碼的物件，無論哪個選取物件，以滑鼠右鍵按一下物件，然後選取**將儲存為指令碼**。  
  
4.  在**存**對話方塊方塊中，找出您要儲存指令碼中，輸入中的檔案名稱的資料夾**檔案名稱**方塊，然後再按一下**確定**。  
  
    SSMA 會將附加.sql 檔案的副檔名。  
  
### <a name="modifying-scripts"></a>修改指令碼  
在您儲存後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 做為指令碼的物件定義，您可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]修改指令碼。  
  
**若要修改指令碼**  
  
1.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]**檔案**功能表上，指向**開啟**，然後按一下 **檔案**。  
  
2.  在**開啟**對話方塊中，找出並選取您的指令碼檔案，然後按一下**確定**。  
  
3.  使用查詢編輯器，編輯指令碼檔案。  
  
    如需查詢編輯器的詳細資訊，請參閱 [編輯器便利命令和功能] 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
4.  若要儲存指令碼，在 [檔案] 功能表上，選取**儲存**。  
  
### <a name="running-scripts"></a>執行指令碼  
您可以在執行指令碼或個別的陳述式， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。  
  
**執行指令碼**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]**檔案**功能表上，指向**開啟**，然後按一下 **檔案**。  
  
2.  在**開啟**對話方塊中，找出並選取您的指令碼檔案，然後按一下**確定**。  
  
3.  若要執行完整的指令碼，請按**F5**索引鍵。  
  
4.  若要執行一組陳述式，選取陳述式在查詢編輯器 視窗，然後按**F5**索引鍵。  
  
如需如何使用查詢編輯器來執行指令碼的詳細資訊，請參閱 「[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)]查詢 」 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
您也可以執行從命令列指令碼，使用**sqlcmd**公用程式，以及從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式。 如需有關**sqlcmd**，請參閱中的 「 sqlcmd 公用程式 」[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。 如需有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式，請參閱 「 自動化管理工作 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式)"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="securing-objects-in-sql-server"></a>保護 SQL Server 中的物件  
您已載入至轉換的資料庫物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以授與及拒絕的權限的物件。 最好執行這項操作，然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需有關如何協助保護資訊中的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱中的 「 安全性考量的資料庫和資料庫應用程式"[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[將資料移轉至 SQL Server](http://msdn.microsoft.com/en-us/f3b18af7-1af0-499d-a00d-a0af94895625)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
