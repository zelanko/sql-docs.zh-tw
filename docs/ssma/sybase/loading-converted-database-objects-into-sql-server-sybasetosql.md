---
title: 已轉換的資料庫物件載入至 SQL Server (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f196050cfb3f32ba85f82dcdb6496483be8ff099
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47750482"
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>將轉換的資料庫物件載入 SQL Server (SybaseToSQL)
轉換 Sybase Adaptive Server Enterprise (ASE) 資料庫物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您可以載入到產生的資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您可以讓 SSMA 建立物件，或者您可以編寫物件指令碼，然後自己執行的指令碼。 此外，SSMA 可讓您更新目標中繼資料的實際內容[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步處理和指令碼之間進行選擇  
如果您想要轉換之資料庫物件載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，而不需修改，您可以讓 SSMA 上直接建立或重新建立資料庫物件。 這個方法既快速又簡單，但不允許的自訂[!INCLUDE[tsql](../../includes/tsql-md.md)]定義的程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或預存程序以外的 SQL Azure 物件。  
  
如果您想要修改[!INCLUDE[tsql](../../includes/tsql-md.md)]用來建立中的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，或如果您想要更充分掌控何時及如何在中建立的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，若要建立使用 SSMA[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼。 您可以修改這些指令碼，會個別建立每個物件然後甚至使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 代理程式排程建立這些物件。  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>使用 SSMA 將物件載入 SQL Server 或 SQL Azure  
要用來建立的 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫物件，您選取的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料總管，然後再同步處理的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，如下列程序中所示。 根據預設，如果物件已存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，而且如果 SSMA 中繼資料有一些本機變更或更新這些非常的物件，定義則 SSMA 會改變中的物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您可以變更預設行為，藉由編輯**專案設定**。  
  
> [!NOTE]  
> 您可以選取現有的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或未轉換從 ASE 資料庫的 SQL Azure 資料庫物件。 不過，這些物件將不會重新建立或改變 SSMA。  
  
**若要同步處理的物件，與 SQL Server 或 SQL Azure**  
  
1.  在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料總管，展開最上方[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 節點中，然後展開**資料庫**。  
  
2.  選取要處理的物件：  
  
    -   若要同步處理完整的資料庫，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要同步處理，或省略個別物件或類別目錄的物件，選取或清除的物件或資料夾旁邊的核取方塊。  
  
3.  選取要處理的物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料總管，以滑鼠右鍵按一下**資料庫**，然後按一下**同步處理資料庫**。  
  
    您也可同步個別物件或類別目錄的物件，該物件或其父資料夾上按一下滑鼠右鍵，然後按一下**同步處理資料庫**。  
  
    之後，將會顯示的 SSMA**同步處理資料庫**對話方塊中，您可以在其中看到兩個項目群組。 在左側，SSMA 會顯示選取的資料庫物件，表示在樹狀目錄中。 在右側，您可以看到代表 SSMA 中繼資料中的相同物件的樹狀結構。 您可以展開樹狀目錄，按一下向左或向 [+] 按鈕。 放置兩個樹狀結構之間的 [動作] 欄中顯示的同步處理方向。  
  
    動作登可以有三種狀態：  
  
    -   向左箭號表示的中繼資料內容會儲存在資料庫 （預設值）。  
  
    -   向右箭號表示資料庫內容將會覆寫的 SSMA 中繼資料。  
  
    -   跨正負號表示將會採取任何動作。  
  
按一下動作正負號，以變更狀態。 當您按一下時，將會執行實際的同步處理 **[確定]** 按鈕**同步處理資料庫**對話方塊。  
  
## <a name="scripting-objects"></a>編寫物件指令碼  
如果您想要儲存[!INCLUDE[tsql](../../includes/tsql-md.md)]定義的轉換後的資料庫物件，或您想要變更的物件定義和執行指令碼自行，您可以儲存轉換的資料庫物件定義以便[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼。  
  
**若要將物件儲存為指令碼**  
  
1.  選取要儲存到指令碼的物件之後，以滑鼠右鍵按一下**資料庫**，然後選取**儲存為指令碼**。  
  
    您也可以編寫個別物件或類別目錄的物件，以滑鼠右鍵按一下 物件或其包含的資料夾，然後選取**儲存指令碼**。  
  
2.  在 **另存新檔**對話方塊方塊中，找出您想要用來儲存指令碼中，輸入中的檔案名稱的資料夾**檔案名稱**方塊，然後再按一下**確定**。  
  
    SSMA 會將附加的.sql 檔案的副檔名。  
  
### <a name="modifying-scripts"></a>修改指令碼  
在您儲存後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件定義為一或多個指令碼，您可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來檢視和修改指令碼。  
  
**若要修改指令碼**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**檔案**功能表上，指向**開啟**，然後按一下 **檔案**。  
  
2.  在 [**開放**] 對話方塊中，瀏覽至並選取您的指令碼檔案，然後按一下**確定**。  
  
3.  編輯並使用查詢編輯器的指令碼檔案。  
  
    查詢編輯器的詳細資訊，請參閱 [編輯器便利命令和功能]，在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
4.  若要儲存指令碼，在 [檔案] 功能表上，選取**儲存**。  
  
### <a name="running-scripts"></a>執行指令碼  
您可以在執行指令碼或個別的陳述式， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
**若要執行指令碼**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**檔案**功能表上，指向**開啟**，然後按一下 **檔案**。  
  
2.  在 [**開放**] 對話方塊中，瀏覽至並選取您的指令碼檔案，然後按一下**確定**。  
  
3.  若要執行完整的指令碼，請按**F5**索引鍵。  
  
4.  若要執行一組陳述式，選取陳述式在查詢編輯器 視窗，然後按**F5**索引鍵。  
  
如需如何使用查詢編輯器來執行指令碼的詳細資訊，請參閱 「[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]查詢 」 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
您也可以執行從命令列指令碼，利用**sqlcmd**公用程式，以及從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式。 如需詳細資訊**sqlcmd**，請參閱中的 「 sqlcmd 公用程式 」[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。 如需詳細資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式，請參閱 「 自動化管理工作 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式)"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
## <a name="securing-objects-in-sql-server"></a>保護 SQL Server 中的物件  
轉換的資料庫物件載入之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以授與和拒絕權限，這些物件。 它是個不錯的主意，若要這樣做之前移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需有關如何協助保護資訊中的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 「 安全性考量的資料庫和資料庫應用程式 > 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[移轉 Sybase ASE 資料到 SQL Server / SQL Azure(SybaseToSQL)](http://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
