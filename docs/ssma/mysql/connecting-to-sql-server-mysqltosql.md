---
title: 連接到 SQL Server （MySQLToSQL） |Microsoft Docs
description: 瞭解如何連接到 SQL Server 的目標實例，以遷移 MySQL 資料庫。 SSMA 會取得 SQL Server 中資料庫的相關中繼資料。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 462b209d73f48217cf9941adf2e3af45d62371cd
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394283"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>連線到 SQL Server (MySQLToSQL)
若要將 MySQL 資料庫遷移至 SQL Server，您必須連接到 SQL Server 的目標實例。 當您連接時，SSMA 會取得 SQL Server 實例中所有資料庫的相關中繼資料，並在 SQL Server 中繼資料瀏覽器中顯示資料庫中繼資料。 SSMA 會儲存您所連接 SQL Server 實例的資訊，但不會儲存密碼。  
  
您的 SQL Server 連接會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想要使用伺服器的作用中連接，就必須重新連接到 SQL Server。 在您將資料庫物件載入 SQL Server 並遷移資料之前，您可以離線工作。  
  
有關 SQL Server 實例的中繼資料不會自動同步處理。 相反地，若要更新 SQL Server 中繼資料 Explorer 中的中繼資料，您必須手動更新 SQL Server 中繼資料。 如需詳細資訊，請參閱本主題稍後的「同步處理 SQL Server 中繼資料」一節。  
  
## <a name="required-sql-server-permissions"></a>必要的 SQL Server 許可權  
用來連接到 SQL Server 的帳戶需要不同的許可權，視帳戶執行的動作而定：  
  
-   若要將 MySQL 物件轉換成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法、更新 SQL Server 的中繼資料，或將已轉換的語法儲存至腳本，該帳戶必須具有登入 SQL Server 實例的許可權。  
  
-   若要將資料庫物件載入 SQL Server，最低許可權需求是目標資料庫中**db_owner**資料庫角色的成員資格。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 連接  
將 MySQL 資料庫物件轉換成 SQL Server 語法之前，您必須先建立要在其中遷移 MySQL 資料庫的 SQL Server 實例連接。  
  
當您定義連接屬性時，也會指定要遷移物件和資料的資料庫。 連接到 SQL Server 之後，您可以在 MySQL 架構層級自訂此對應。 如需詳細資訊，請參閱[將 MySQL 資料庫對應至 SQL Server 架構 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> 嘗試連接到 SQL Server 之前，請確定 SQL Server 的實例正在執行中，而且可以接受連接。  
  
**若要連接到 SQL Server**  
  
1.  在 [檔案]**功能表上，選取 [連線****至 SQL Server]** （在建立專案之後，就會啟用此選項）。  
  
    如果您先前已連接到 SQL Server，命令名稱會**重新連接到 SQL Server**。  
  
2.  在 [連接] 對話方塊中，輸入或選取 SQL Server 實例的名稱。  
  
    -   如果您要連接到本機電腦上的預設實例，您可以輸入**localhost**或句點（**.**）。  
  
    -   如果您要連接到另一部電腦上的預設實例，請輸入電腦的名稱。  
  
    -   如果您要連接到另一部電腦上的已命名實例，請輸入電腦名稱稱，後面接著反斜線，然後是實例名稱，例如 MyServer\MyInstance。  
  
3.  如果您的 SQL Server 實例已設定為接受非預設通訊埠上的連接，請在 [**伺服器埠**] 方塊中輸入用於 SQL Server 連接的埠號碼。 針對 SQL Server 的預設實例，預設埠號碼為1433。 若為已命名的實例，SSMA 將會嘗試從 SQL Server Browser 服務取得埠號碼。  
  
4.  在 [**驗證**] 方塊中，選取要用於連接的驗證類型。 若要使用目前的 Windows 帳戶，請選取 [ **Windows 驗證**]。 若要使用 SQL Server 登入，請選取 [SQL Server Authentication]，然後提供 [登入名稱] 和 [密碼]。  
  
5.  針對安全連線，會加入兩個控制項： [**加密連接**] 和 [ **TrustServerCertificate** ] 核取方塊。 只有在核取 [**加密連接**] 時，才會顯示 [ **TrustServerCertificate** ] 核取方塊。 若已核取 [**加密**連線] （true），而且未選取 [ **TrustServerCertificate** （false）]，則會驗證 SQL Server SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 若要確保這一點，憑證必須安裝在用戶端以及伺服器端。  
  
6.  按一下 [連線]。  
  
**版本相容性較高**  
  
它可以連接/重新連接至較高版本的 SQL Server。  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當建立的專案是2005時，您將能夠連線到2008或2012或2014或 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當建立的專案是2008時，您將能夠連接到2012或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 但不允許連接到較低版本，亦即 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當建立的專案是2012時，您將能夠連接到2012或2014或 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當建立的專案為2014時，您只能連接到2014或 2016 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
5.  較高的版本相容性對「SQL Azure」無效。  
  
|專案類型與目標伺服器版本的比較|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> （版本： 9. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> （版本： 10. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />（版本： 11. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014<br />（版本： 12. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />（版本： 13. x）|SQL Azure|  
|-|-|-|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||是||  
|SQL Azure||||||是|  
  
> [!IMPORTANT]  
> 資料庫物件的轉換是根據專案類型執行，而不是根據所 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接之的版本。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 專案中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 即使您連接至較高版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016），還是會以每個2005執行轉換。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步處理 SQL Server 中繼資料  
SQL Server 資料庫的相關中繼資料不會自動更新。 當您第一次連接到 SQL Server 時，或上次手動更新中繼資料時，SQL Server 中繼資料 Explorer 中的中繼資料就是中繼資料的快照集。 您可以手動更新所有資料庫或任何單一資料庫或資料庫物件的中繼資料。  
  
**同步處理中繼資料**  
  
1.  請確定您已連線到 SQL Server。  
  
2.  在 SQL Server 中繼資料 Explorer] 中，選取您要更新之資料庫或資料庫架構旁的核取方塊。  
  
    例如，若要更新所有資料庫的中繼資料，請選取 [資料庫] 旁的方塊。  
  
3.  以滑鼠右鍵按一下 [資料庫] 或個別的資料庫或資料庫架構，然後選取 [**與資料庫同步處理**]。  
  
## <a name="next-step"></a>後續步驟  
遷移的下一個步驟取決於您的專案需求：  
  
-   若要自訂 MySQL 架構與 SQL Server 資料庫和架構之間的對應，請參閱[將 Mysql 資料庫對應至 SQL Server 架構 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   若要自訂專案的設定選項，請參閱[設定專案選項 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   若要自訂來源和目標資料類型的對應，請參閱將[MySQL 和 SQL Server 資料類型對應 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   如果您不需要執行上述任何一項工作，您可以將 MySQL 資料庫物件定義轉換成 SQL Server 的物件定義。 如需詳細資訊，請參閱將[MySQL 資料庫轉換 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料庫遷移至 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
