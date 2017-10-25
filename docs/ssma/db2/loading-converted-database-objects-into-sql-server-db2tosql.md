---
title: "載入已轉換成 SQL Server (DB2ToSQL) 資料庫物件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f74e15c261041ae0a68152417955a81ed96994f8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>載入已轉換成 SQL Server (DB2ToSQL) 資料庫物件
DB2 結構描述，以轉換之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以載入到產生的資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以讓 SSMA 建立物件，或您可以編寫物件指令碼，並自行執行指令碼。 此外，SSMA 可讓您更新目標中繼資料的實際內容[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步處理和指令碼之間選擇  
如果您想要轉換的資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]而不需修改，您可以擁有 SSMA 直接建立或重新建立資料庫物件。 該方法是快速且容易使用，但不允許的自訂[!INCLUDE[tsql](../../includes/tsql_md.md)]定義程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]預存程序以外的物件。  
  
如果您想要修改[!INCLUDE[tsql](../../includes/tsql_md.md)]用來建立物件，或如果您想要更充分掌控物件建立時，使用 SSMA 建立指令碼。 您即可修改這些指令碼、 個別建立每個物件或甚至使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Agent 來排程建立這些物件。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>若要同步處理的物件與 SQL Server 使用 SSMA  
要用來建立 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫物件，您選取的物件中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管，然後同步處理的物件與[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，如下列程序中所示。 根據預設，如果物件已存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，和如果 SSMA 中繼資料中的物件比更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 會改變中的物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以變更預設行為，藉由編輯**專案設定**。  
  
> [!NOTE]  
> 您可以選取現有的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫未轉換從 DB2 資料庫的物件。 不過，這些物件將不會重新建立或更改 SSMA。  
  
**若要同步處理 SQL Server 的物件**  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管，展開最上層[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 節點，然後展開**資料庫**。  
  
2.  選取要處理的物件：  
  
    -   若要同步處理完整的資料庫，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要同步處理，或省略個別物件或類別目錄的物件，選取或清除的物件或資料夾旁邊的核取方塊。  
  
3.  選取要處理中的物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管，以滑鼠右鍵按一下**資料庫**，然後按一下**同步處理資料庫**。  
  
    您也可同步個別物件或類別目錄的物件，該物件或其父資料夾上按一下滑鼠右鍵，然後按一下**同步處理資料庫**。  
  
    之後，將會顯示 SSMA**同步處理資料庫**對話方塊中，您可以在其中看到兩個群組的項目。 在左邊，SSMA 會顯示選取的資料庫物件，代表在樹狀目錄中。 在右側，您可以看到代表 SSMA 中繼資料中的相同物件的樹狀結構。 您可以展開樹狀目錄，按一下向左或向 ' +' 按鈕。 放置於兩個樹系之間的 [動作] 欄會顯示同步處理方向。  
  
    動作符號可以是三種狀態：  
  
    -   向左箭號表示中繼資料的內容將會儲存在資料庫 （預設值）。  
  
    -   向右箭號表示資料庫的內容將會覆寫的 SSMA 中繼資料。  
  
    -   跨號表示將會採取任何動作。  
  
按一下動作正負號，以變更狀態。 將會執行實際的同步處理，當您按一下**確定**按鈕**同步處理資料庫**對話方塊。  
  
## <a name="scripting-objects"></a>編寫物件指令碼  
若要儲存[!INCLUDE[tsql](../../includes/tsql_md.md)]轉換的資料庫物件，或要變更的物件定義和執行指令碼自行定義，您可以儲存轉換的資料庫物件定義要[!INCLUDE[tsql](../../includes/tsql_md.md)]指令碼。  
  
**若要儲存物件做為指令碼**  
  
1.  選取要儲存到指令碼的物件之後，以滑鼠右鍵按一下**資料庫**，然後按一下**將儲存為指令碼**。  
  
    您也可以編寫個別物件或類別目錄的物件，該物件或其父資料夾上按一下滑鼠右鍵，然後按一下**將儲存為指令碼**。  
  
2.  在**存**對話方塊方塊中，找出您要儲存指令碼中，輸入中的檔案名稱的資料夾**檔案名稱** 方塊中，然後[!INCLUDE[clickOK](../../includes/clickok_md.md)]。 SSMA 會將附加.sql 檔案的副檔名。  
  
### <a name="modifying-scripts"></a>修改指令碼  
在您儲存後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件定義為一或多個指令碼，您可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]來檢視和修改指令碼。  
  
**若要修改指令碼**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]**檔案**功能表上，指向**開啟**，然後按一下**檔案**。  
  
2.  在**開啟**對話方塊，並選取您的指令碼檔案，然後按一下確定。
  
3.  使用查詢編輯器，編輯指令碼檔案。  
  
    如需查詢編輯器的詳細資訊，請參閱 [編輯器便利命令和功能] 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
4.  若要儲存指令碼，在 [檔案] 功能表按一下**儲存**。  
  
### <a name="running-scripts"></a>執行指令碼  
您可以在執行指令碼或個別的陳述式， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。  
  
**執行指令碼**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]**檔案**功能表上，指向**開啟**，然後按一下**檔案**。  
  
2.  在**開啟**對話方塊方塊中，選取您的指令碼檔案，然後按一下[!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  若要執行完整的指令碼，請按**F5**索引鍵。  
  
4.  若要執行一組陳述式，選取陳述式在查詢編輯器 視窗，然後按**F5**索引鍵。  
  
如需如何使用查詢編輯器來執行指令碼的詳細資訊，請參閱 「[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)]查詢 」 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
您也可以執行從命令列指令碼，使用**sqlcmd**公用程式，以及從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式。 如需有關**sqlcmd**，請參閱中的 「 sqlcmd 公用程式 」[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。 如需有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式，請參閱 「 自動化管理工作 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式)"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="securing-objects-in-sql-server"></a>保護 SQL Server 中的物件  
您已載入至轉換的資料庫物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以授與及拒絕的權限的物件。 最好執行這項操作，然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需有關如何協助保護資訊中的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱中的 「 安全性考量的資料庫和資料庫應用程式"[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[移轉至 SQL Server 的 DB2 資料](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b)。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料移轉到 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  

