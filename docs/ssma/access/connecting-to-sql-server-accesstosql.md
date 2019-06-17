---
title: 連接到 SQL Server (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0bedb8ba74d7965df34a102fb0d53a0cbdb248dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63139018"
---
# <a name="connecting-to-sql-server-accesstosql"></a>連接到 SQL Server (AccessToSQL)
若要將 Access 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必須連接到目標執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 SSMA 連線時，取得執行個體中之資料庫相關的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並顯示資料庫中繼資料中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管。 SSMA 會將哪一個執行個體的相關資訊儲存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您要連線，但不會儲存密碼。  
  
SQL Server 的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接到 SQL Server 是否作用中的連線到伺服器。 您的資料庫物件載入 SQL Server，並移轉資料之前，您可以離線工作。  
  
SQL Server 執行個體的相關中繼資料不會自動同步處理。 相反地，若要更新 SQL Server 中繼資料總管 中的中繼資料，您必須手動更新 SQL Server 中繼資料。 如需詳細資訊，請參閱本主題稍後的 「 同步處理 SQL Server 中繼資料 」 一節。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 權限  
用來連接到帳戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要不同的權限，根據該帳戶所執行的動作。  
  
-   要轉換到存取物件[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，來重新整理中繼資料，從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或是要儲存指令碼轉換的語法，帳戶必須具備登入的執行個體的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   資料庫物件載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，最小權限需求是中的成員資格**db_owner**之目標資料庫內的資料庫角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 連接  
轉換到存取資料庫物件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法中，您必須建立的執行個體的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您要移轉的 Access 資料庫。  
  
當您定義的連接屬性時，您也可以指定其中將移轉物件和資料的資料庫。 連線到之後，您可以自訂此對應，在存取資料庫層級[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)。  
  
> [!IMPORTANT]  
> 連接到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請確定執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行，而且可以接受連線。 如需詳細資訊，請參閱 「 連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫引擎 」 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
**若要連接到 SQL Server**  
  
1.  在 **檔案**功能表上，選取**連接到 SQL Server**。  
  
    如果您先前連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，命令名稱會是**重新連接到 SQL Server**。  
  
2.  在 **伺服器名稱**方塊中，輸入或選取的執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    -   如果您要連接到本機電腦上的預設執行個體，您可以輸入**localhost**或句點 ( **。** )。  
  
    -   如果您要連接到另一部電腦上的預設執行個體，請輸入電腦的名稱。  
  
    -   如果您要連接到具名執行個體，請輸入電腦名稱、 反斜線和執行個體名稱。 例如：MyServer\MyInstance。  
  
    -   若要連接到作用中使用者執行個體[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]，使用具名管道連接通訊協定和指定管道名稱，例如\\ \\.\pipe\sql\query。 如需詳細資訊，請參閱[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]文件。  
  
3.  如果您的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]設定為在非預設連接埠上接受連線中，輸入用於連接埠號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的連線**伺服器連接埠** 方塊中。 預設執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，預設連接埠號碼為 1433年。 具名執行個體，SSMA 會嘗試取得連接埠號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]瀏覽器服務。  
  
4.  在 **資料庫**方塊中，輸入物件和資料移轉的目標資料庫的名稱。  
  
    此選項時，無法提供重新連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    目標資料庫名稱不能包含空格或特殊字元。 比方說，您可存取資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名為"abc"的資料庫。 但您無法存取資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫名為"b-c"。  
  
    連線之後，您可以自訂這個對應每個資料庫。 如需詳細資訊，請參閱[對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)  
  
5.  在 **驗證**下拉式選單中，選取要用於連線的驗證類型。 若要使用目前的 Windows 帳戶，請選取**Windows 驗證**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入，選取**SQL Server 驗證**，然後提供 使用者名稱和密碼。  
  
6.  安全的連線，會新增兩個控制項，**加密連接**核取方塊並**TrustServerCertificate**核取方塊。 只有當**加密連接**核取方塊**TrustServerCertificate**核取方塊會顯示。 當**加密連接**是 checked(true) 並**TrustServerCertificate** unchecked(false)，將會驗證 SQL Server SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 若要確保此行為，以及伺服器端上的用戶端必須安裝憑證。  
  
7.  按一下 **[連接]** 。  
  
**較高的版本相容性**  
  
它允許連線/重新連線到更高版本的 SQL Server。  
  
1.  您將能夠連接到 SQL Server 2008 或 SQL Server 2012，當專案建立 SQL Server 2005。  
  
2.  您可以建立的專案是 SQL Server 2008，但它不允許連接至較低版本，也就是 SQL Server 2005 時，連接到 SQL Server 2012。  
  
3.  您可以在 SQL Server 2012 建立的專案時，連接到 SQL Server 2012。  
  
4.  較高的版本相容性不是有效的 SQL Azure。  
  
||||||||
|-|-|-|-|-|-|-|
|**專案類型與目標伺服器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 (版本：9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 (版本：10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||是||
|SQL Azure||||||是|
  
> [!IMPORTANT]  
> 資料庫物件的轉換被實行中，這是根據專案類型，但不是會根據連接的 SQL Server 的版本。 如果 SQL Server 2005 專案中，轉換會執行根據 SQL Server 2005 即使您已連線到較高版本的 SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步處理 SQL Server 中繼資料  
如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述變更連線之後，您可以與伺服器同步處理中繼資料。  
  
**同步處理 SQL Server 中繼資料**  
  
-   在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管]，以滑鼠右鍵按一下**資料庫**，然後選取**同步處理資料庫**。  
  
## <a name="reconnecting-to-sql-server"></a>重新連接到 SQL Server  
連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會保持作用中，直到您關閉專案為止。 當您重新開啟專案時，您必須重新連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果您想使用中的連接到伺服器。 您可以離線之前載入至資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並移轉資料。  
  
若要重新連接的程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立連接的程序相同。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要自訂來源和目標資料庫之間的對應，請參閱[對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)，否則為下一個步驟是將轉換至的資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法使用[轉換資料庫物件](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
