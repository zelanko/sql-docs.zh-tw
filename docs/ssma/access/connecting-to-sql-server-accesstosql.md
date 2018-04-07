---
title: 連接到 SQL Server (AccessToSQL) |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 572c516cfac93f3122814cdc93a3eed4f2b9c291
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="connecting-to-sql-server-accesstosql"></a>連接到 SQL Server (AccessToSQL)
若要將 Access 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您必須連接到的目標執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 SSMA 連線時，取得有關執行個體中資料庫的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]並顯示資料庫中繼資料中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管。 SSMA 會儲存有關哪一個執行個體資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]您連線到，但不會儲存密碼。  
  
SQL Server 的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接到 SQL Server 是否使用中的連線到伺服器。 載入 SQL Server 資料庫物件，並移轉資料之前，您可以離線工作。  
  
SQL Server 執行個體的相關中繼資料不會自動同步處理。 相反地，若要更新 SQL Server 中繼資料總管 中的中繼資料，您必須手動更新 SQL Server 中繼資料。 如需詳細資訊，請參閱本主題稍後的 「 同步處理 SQL Server 中繼資料 」 一節。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 權限  
用來連接到帳戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]需要不同的權限，根據該帳戶所執行的動作。  
  
-   要轉換到存取物件[!INCLUDE[tsql](../../includes/tsql_md.md)]語法，請重新整理中繼資料從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，或是要儲存指令碼轉換的語法，帳戶必須具備登入的執行個體的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   資料庫物件載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，並將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，最小權限需求是中的成員資格**db_owner**之目標資料庫內的資料庫角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 連接  
轉換到存取資料庫物件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法中，您必須連接到執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]您要移轉的 Access 資料庫。  
  
當您定義的連接屬性時，您也可以指定其中將移轉物件和資料的資料庫。 連線之後，您可以自訂此對應在存取資料庫層級[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需詳細資訊，請參閱[對應來源和目標資料庫](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
> [!IMPORTANT]  
> 在連接之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請確定執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]正在執行，而且可接受連接。 如需詳細資訊，請參閱"連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫引擎 」 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
**若要連接到 SQL Server**  
  
1.  在**檔案**功能表上，選取**連接到 SQL Server**。  
  
    如果您先前連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，命令名稱將會是**重新連接到 SQL Server**。  
  
2.  在**伺服器名稱**方塊中，輸入或選取的執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   如果您要連接到本機電腦上的預設執行個體，您可以輸入**localhost**或一個點 (**。**)。  
  
    -   如果您要連接到另一部電腦上的預設執行個體，請輸入電腦的名稱。  
  
    -   如果您要連接到具名執行個體，請輸入電腦名稱、 反斜線和執行個體名稱。 例如： MyServer\MyInstance。  
  
    -   若要連接到作用中使用者執行個體的[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]，透過具名管道連線通訊協定和指定的管道名稱，例如\\ \\.\pipe\sql\query。 如需詳細資訊，請參閱 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 文件。  
  
3.  如果您的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]設定為非預設連接埠上接受連接，請輸入用於連接埠號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中的連線**伺服器連接埠**方塊。 預設執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，預設連接埠號碼為 1433年。 具名執行個體，SSMA 會嘗試取得連接埠號碼從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]瀏覽器服務。  
  
4.  在**資料庫**方塊中，輸入物件和資料移轉的目標資料庫的名稱。  
  
    此選項時，無法提供重新連接至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    目標資料庫名稱不能包含空格或特殊字元。 例如，您可以存取資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]名為"abc"的資料庫。 但您無法存取資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫名為"b-c"。  
  
    連接之後，您可以自訂這個對應每個資料庫。 如需詳細資訊，請參閱[對應來源和目標資料庫](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
5.  在**驗證**下拉式功能表，選取要用於連線的驗證類型。 若要使用目前的 Windows 帳戶，請選取**Windows 驗證**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入，選取**SQL Server 驗證**，然後提供使用者名稱和密碼。  
  
6.  安全的連線，會新增兩個控制項，**加密連接**核取方塊和**TrustServerCertificate**核取方塊。 只有當**加密連接**核取方塊**TrustServerCertificate**核取方塊會顯示。 當**加密連接**是 checked(true) 和**TrustServerCertificate** unchecked(false)，將會驗證 SQL Server SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 若要確保這種情況，憑證必須安裝在用戶端和伺服器端上。  
  
7.  按一下 **[連接]**。  
  
**較高的版本相容性**  
  
它會允許連接/重新連接至較新版本的 SQL Server。  
  
1.  您可以在 SQL Server 2005 所建立的專案時，連接到 SQL Server 2008 或 SQL Server 2012。  
  
2.  您可以建立的專案是 SQL Server 2008，但不是允許連接至較低版本，也就是 SQL Server 2005 時，連線到 SQL Server 2012。  
  
3.  您可以在 SQL Server 2012 所建立的專案時，連接到 SQL Server 2012。  
  
4.  較高的版本相容性不正確的 SQL Azure。  
  
||||||||
|-|-|-|-|-|-|-|
|**專案類型與目標伺服器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 (版本： 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 (版本： 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||是||
|SQL Azure||||||是|
  
> [!IMPORTANT]  
> 資料庫物件的轉換會執行根據專案類型，但不是會根據連接的 SQL Server 的版本。 發生 SQL Server 2005 專案時，轉換會執行 SQL Server 2005 根據即使您已連線到較高版本的 SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步處理 SQL Server 中繼資料  
如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構描述變更您連接之後，您可以與伺服器同步處理中繼資料。  
  
**同步處理 SQL Server 中繼資料**  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管，以滑鼠右鍵按一下**資料庫**，然後選取**同步處理資料庫**。  
  
## <a name="reconnecting-to-sql-server"></a>重新連接到 SQL Server  
您的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]維持使用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]如果您想要的使用中連接到伺服器。 您可以離線直到資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉資料。  
  
重新連接至伺服器的程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]建立之連接的程序相同。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要自訂來源和目標資料庫之間的對應，請參閱[對應來源和目標資料庫](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)否則下一個步驟是將轉換至的資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法使用[轉換資料庫物件](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
