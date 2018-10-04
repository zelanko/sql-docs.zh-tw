---
title: 已轉換的資料庫物件載入至 SQL Server (OracleToSQL) |Microsoft Docs
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
manager: v-thobro
ms.openlocfilehash: fa7e74d94fba34ebb3ae1e11ccaae308dd14e3e8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685256"
---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>將轉換的資料庫物件載入 SQL Server (OracleToSQL)
Oracle 結構描述轉換至 SQL Server 之後，您可以產生的資料庫物件載入 SQL Server。 您可以讓 SSMA 建立物件，或者您可以編寫物件指令碼，然後自己執行的指令碼。 此外，SSMA 也可讓您使用 SQL Server 資料庫的實際內容來更新目標中繼資料。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同步處理和指令碼之間進行選擇  
如果您想要轉換之資料庫物件載入 SQL Server，而不需修改，您可以直接建立或重新建立資料庫物件的 SSMA。 方法既快速又簡單，但不允許自訂[!INCLUDE[tsql](../../includes/tsql-md.md)]定義預存程序以外的 SQL Server 物件的程式碼。  
  
如果您想要修改[!INCLUDE[tsql](../../includes/tsql-md.md)]用來建立物件，或如果您想要更充分掌控物件建立時，使用 SSMA 建立指令碼。 您可以再修改這些指令碼，每個物件會個別建立，甚至使用 SQL Server Agent 來排程建立這些物件。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>使用 SSMA 與 SQL Server 同步處理物件  
若要使用 SSMA 建立 SQL Server 資料庫物件，您在 SQL Server 中繼資料總管 中選取的物件，然後再同步處理物件與 SQL Server，如下列程序中所示。 根據預設，如果物件已存在於 SQL Server，而且如果 SSMA 中繼資料是比 SQL Server 中的物件則 SSMA 會改變 SQL Server 中的物件定義。 您可以變更預設行為，藉由編輯**專案設定**。  
  
> [!NOTE]  
> 您可以選取現有的 SQL Server 資料庫物件，不從 Oracle 資料庫進行轉換。 不過，這些物件將不會重新建立或更改 SSMA。  
  
**若要使用 SQL Server 同步處理物件**  
  
1.  在 SQL Server 中繼資料總管，展開最上層的 SQL Server 節點，然後再展開**資料庫**。  
  
2.  選取要處理的物件：  
  
    -   若要同步處理完整的資料庫，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要同步處理，或省略個別物件或類別目錄的物件，選取或清除的物件或資料夾旁邊的核取方塊。  
  
3.  選取要在 SQL Server 中繼資料總管 中處理的物件之後，以滑鼠右鍵按一下**資料庫**，然後按一下**同步處理資料庫**。  
  
    您也可同步個別物件或類別目錄的物件，該物件或其父資料夾上按一下滑鼠右鍵，然後按一下**同步處理資料庫**。  
  
    之後，將會顯示的 SSMA**同步處理資料庫**對話方塊中，您可以在其中看到兩個項目群組。 在左側，SSMA 會顯示選取的資料庫物件，表示在樹狀目錄中。 在右側，您可以看到代表 SSMA 中繼資料中的相同物件的樹狀結構。 您可以展開樹狀目錄，按一下向左或向 [+] 按鈕。 放置兩個樹狀結構之間的 [動作] 欄中顯示的同步處理方向。  
  
    動作登可以有三種狀態：  
  
    -   向左箭號表示的中繼資料內容會儲存在資料庫 （預設值）。  
  
    -   向右箭號表示資料庫內容將會覆寫的 SSMA 中繼資料。  
  
    -   跨正負號表示將會採取任何動作。  
  
按一下動作正負號，以變更狀態。 當您按一下時，將會執行實際的同步處理 **[確定]** 按鈕**同步處理資料庫**對話方塊。  
  
## <a name="scripting-objects"></a>編寫物件指令碼  
若要儲存[!INCLUDE[tsql](../../includes/tsql-md.md)]定義的轉換後的資料庫物件，或改變的物件定義，然後自己執行指令碼，您可以將儲存已轉換的資料庫物件定義以便[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼。  
  
**若要將物件儲存為指令碼**  
  
1.  選取要儲存到指令碼的物件之後，以滑鼠右鍵按一下**資料庫**，然後按一下**儲存為指令碼**。  
  
    您也可以編寫個別物件或類別目錄的物件，該物件或其父資料夾上按一下滑鼠右鍵，然後按一下**儲存為指令碼**。  
  
2.  在 **另存新檔**對話方塊方塊中，找出您想要用來儲存指令碼中，輸入中的檔案名稱的資料夾**檔案名稱**方塊，然後再按一下 確定 SSMA 會將.sql 副檔名的附加。  
  
### <a name="modifying-scripts"></a>修改指令碼  
您已儲存的 SQL Server 物件定義為一個或多個指令碼之後，您可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來檢視和修改指令碼。  
  
**若要修改指令碼**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**檔案**功能表上，指向**開啟**，然後按一下 **檔案**。  
  
2.  在 [**開啟**] 對話方塊中，選取您的指令碼檔案，然後按一下 [確定]。
  
3.  使用查詢編輯器中編輯指令碼檔案。  
  
    如需有關查詢編輯器的詳細資訊，請參閱 [編輯器便利命令和功能] SQL Server 線上叢書 》 中。  
  
4.  若要儲存指令碼，在 [檔案] 功能表，按一下**儲存**。  
  
### <a name="running-scripts"></a>執行指令碼  
您可以在執行指令碼或個別的陳述式， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
**若要執行指令碼**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**檔案**功能表上，指向**開啟**，然後按一下 **檔案**。  
  
2.  在 **開啟** 對話方塊中，選取您的指令碼檔案，然後按一下 確定  
  
3.  若要執行完整的指令碼，請按**F5**索引鍵。  
  
4.  若要執行一組陳述式，選取陳述式在查詢編輯器 視窗，然後按**F5**索引鍵。  
  
如需如何使用查詢編輯器來執行指令碼的詳細資訊，請參閱 「[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]查詢 「 SQL Server 線上叢書 》 中。  
  
您也可以執行從命令列指令碼，利用**sqlcmd**公用程式，並從 SQL Server Agent。 如需詳細資訊**sqlcmd**，請參閱 SQL Server 線上叢書 》 中的 「 sqlcmd 公用程式 」。 如需有關 SQL Server Agent 的詳細資訊，請參閱 「 自動化系統管理工作 (SQL Server Agent) 」 在 SQL Server 線上叢書 》 中。  
  
## <a name="securing-objects-in-sql-server"></a>保護 SQL Server 中的物件  
轉換的資料庫物件載入 SQL Server 之後，您可以授與和拒絕這些物件的權限。 它是個不錯的主意，若要這樣做之前移轉至 SQL Server 的資料。 如需如何協助保護 SQL Server 中的物件資訊，請參閱 「 安全性考量的資料庫和資料庫應用程式"SQL Server 線上叢書 》 中。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[將資料移轉至 SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[移轉的 Oracle 資料庫到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
