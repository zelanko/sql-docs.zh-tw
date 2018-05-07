---
title: 載入已轉換成 SQL Server (SybaseToSQL) 資料庫物件 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c3c5f0d28224afce206949ae9011c6777458325e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>載入已轉換成 SQL Server (SybaseToSQL) 資料庫物件
Sybase Adaptive Server Enterprise (ASE) 資料庫物件，以轉換之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您可以載入到產生的資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以讓 SSMA 建立物件，或您可以編寫物件指令碼，並自行執行指令碼。 此外，SSMA 可讓您更新目標中繼資料的實際內容[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步處理和指令碼之間選擇  
如果您想要轉換的資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，而不需修改，您可以擁有 SSMA 直接建立或重新建立資料庫物件。 這個方法是快速且容易使用，但不允許的自訂[!INCLUDE[tsql](../../includes/tsql_md.md)]定義程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的物件，預存程序之外。  
  
如果您想要修改[!INCLUDE[tsql](../../includes/tsql_md.md)]用來建立物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，或如果您想要更充分掌控時機與方法會在建立物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，若要建立使用 SSMA[!INCLUDE[tsql](../../includes/tsql_md.md)]指令碼。 您即可修改這些指令碼、 個別建立每個物件或甚至使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的代理程式排程建立這些物件。  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>將物件載入 SQL Server 或 SQL Azure 使用 SSMA  
要用來建立 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫物件，您選取的物件中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管，然後同步處理的物件與[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，如下列程序中所示。 根據預設，如果物件已存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，而且若 SSMA 中繼資料有一些本機變更或更新至這些非常的物件，定義則 SSMA 會改變中的物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以變更預設行為，藉由編輯**專案設定**。  
  
> [!NOTE]  
> 您可以選取現有的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或未轉換從 ASE 資料庫的 SQL Azure 資料庫物件。 不過，這些物件將會重新建立或更改 SSMA。  
  
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
  
**若要儲存物件做為指令碼**  
  
1.  選取要儲存到指令碼的物件之後，以滑鼠右鍵按一下**資料庫**，然後選取**將儲存為指令碼**。  
  
    您也可以編寫個別物件或類別目錄的物件，以滑鼠右鍵按一下物件或其包含的資料夾，然後選取**儲存指令碼**。  
  
2.  在**存**對話方塊方塊中，找出您要儲存指令碼中，輸入中的檔案名稱的資料夾**檔案名稱**方塊，然後再按一下**確定**。  
  
    SSMA 會將附加.sql 檔案的副檔名。  
  
### <a name="modifying-scripts"></a>修改指令碼  
在您儲存後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 做為一或多個指令碼的物件定義，您可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]來檢視和修改指令碼。  
  
**若要修改指令碼**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]**檔案**功能表上，指向**開啟**，然後按一下 **檔案**。  
  
2.  在**開啟**對話方塊中，瀏覽至並選取您的指令碼檔案，然後按一下**確定**。  
  
3.  使用查詢編輯器的指令碼檔案及編輯。  
  
    如需查詢編輯器的詳細資訊，請參閱 [編輯器便利命令和功能] 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
4.  若要儲存指令碼，在 [檔案] 功能表上，選取**儲存**。  
  
### <a name="running-scripts"></a>執行指令碼  
您可以在執行指令碼或個別的陳述式， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。  
  
**執行指令碼**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]**檔案**功能表上，指向**開啟**，然後按一下 **檔案**。  
  
2.  在**開啟**對話方塊中，瀏覽至並選取您的指令碼檔案，然後按一下**確定**。  
  
3.  若要執行完整的指令碼，請按**F5**索引鍵。  
  
4.  若要執行一組陳述式，選取陳述式在查詢編輯器 視窗，然後按**F5**索引鍵。  
  
如需如何使用查詢編輯器來執行指令碼的詳細資訊，請參閱 「[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)]查詢 」 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
您也可以執行從命令列指令碼，使用**sqlcmd**公用程式，以及從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式。 如需有關**sqlcmd**，請參閱中的 「 sqlcmd 公用程式 」[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。 如需有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式，請參閱 「 自動化管理工作 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式)"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="securing-objects-in-sql-server"></a>保護 SQL Server 中的物件  
您已載入至轉換的資料庫物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以授與及拒絕的權限的物件。 最好執行這項操作，然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需有關如何協助保護資訊中的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱中的 「 安全性考量的資料庫和資料庫應用程式"[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[移轉 Sybase ASE 資料插入 SQL Server / SQL Azure(SybaseToSQL)](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811)。  
  
## <a name="see-also"></a>另請參閱  
[Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
