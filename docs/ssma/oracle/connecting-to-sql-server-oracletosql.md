---
title: 連接到 SQL Server (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: fe6cc43dd2f31bafbc8c8715a1ce926d68dedbd2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="connecting-to-sql-server-oracletosql"></a>連接到 SQL Server (OracleToSQL)
若要將 Oracle 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008 R2 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014，您必須連接到任一目標執行個體的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 SSMA 連線時，取得執行個體中的所有資料庫的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]並顯示資料庫中繼資料中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管。 SSMA 會儲存有關哪一個執行個體資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]您已連線，但不會儲存密碼。  
  
您的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]維持使用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]如果您想要的使用中連接到伺服器。 您可以離線直到資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉資料。  
  
執行個體相關的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]並不會自動同步處理。 相反地，若要更新的中繼資料中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管 中，您必須手動更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料。 如需詳細資訊，請參閱 「 同步處理[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料 」 這個主題稍後的章節。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 權限  
用來連接到帳戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]需要不同的權限視帳戶執行的動作而定：  
  
-   要轉換至 Oracle 物件[!INCLUDE[tsql](../../includes/tsql_md.md)]語法，來更新中繼資料從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，或若要儲存指令碼轉換的語法，帳戶必須具有執行個體的登入權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   資料庫物件載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，帳戶必須隸屬**sysadmin**伺服器角色。 如此才能安裝 CLR 組件。  
  
-   若要將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，帳戶必須隸屬**sysadmin**伺服器角色。 如此才能執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式的資料移轉的套件。  
  
-   若要執行的程式碼所產生的 SSMA，帳戶必須具有**Execute**中的所有使用者定義函數的權限**ssma_oracle**目標資料庫的結構描述。 這些函式提供的 Oracle 系統函式，對等的功能和已轉換的物件所使用。  
  
如果用來連接到帳戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]是執行所有移轉工作，此帳戶必須是成員**sysadmin**伺服器角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 連接  
轉換到 Oracle 資料庫物件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法中，您必須連接到執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]您要移轉的 Oracle 資料庫。  
  
當您定義的連接屬性時，您也可以指定其中將移轉物件和資料的資料庫。 連線之後，您可以自訂這個對應 Oracle 結構描述層級[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需詳細資訊，請參閱[對應至 SQL Server 結構描述的 Oracle 結構描述&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)。  
  
> [!IMPORTANT]  
> 您嘗試連接到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請確定執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]正在執行，而且可接受連接。  
  
**若要連接到 SQL Server**  
  
1.  在**檔案**功能表上，選取**連接到 SQL Server**。  
  
    如果您先前連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，命令名稱將會是**重新連接到 SQL Server**。  
  
2.  在 [連線] 對話方塊中，輸入或選取的執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   如果您要連接到本機電腦上的預設執行個體，您可以輸入**localhost**或一個點 (**。**)。  
  
    -   如果您要連接到另一部電腦上的預設執行個體，請輸入電腦的名稱。  
  
    -   如果您要連接到另一部電腦上的具名執行個體，請輸入電腦名稱，後面接著反斜線，然後執行個體名稱，例如 MyServer\MyInstance。  
  
3.  如果您的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]設定為非預設連接埠上接受連接，請輸入用於連接埠號碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中的連線**伺服器連接埠**方塊。 預設執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，預設連接埠號碼為 1433年。 具名執行個體，SSMA 會嘗試取得連接埠號碼從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]瀏覽器服務。  
  
4.  在**資料庫**方塊中，輸入目標資料庫的名稱。  
  
    此選項時，無法提供您重新連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
5.  在**驗證**方塊中，選取要用於連線的驗證類型。 若要使用目前的 Windows 帳戶，請選取**Windows 驗證**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入，選取**SQL Server 驗證**，然後提供登入名稱和密碼。  
  
6.  安全的連線，會新增兩個控制項，**加密連接**和**TrustServerCertificate**核取方塊。 只有當**加密連接**勾選， **TrustServerCertificate**核取方塊會顯示。 當**加密連接**(true) 會檢查和**TrustServerCertificate**未核取 (false)，它將會驗證 SQL Server SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 若要確保這種情況，憑證必須安裝在用戶端和伺服器端上。  
  
7.  按一下 **[連接]**。  
  
**較高的版本相容性**  
  
-   您可以連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016 時所建立的移轉專案[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005年。  
  
-   您可以連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016 時所建立的移轉專案[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年但是不能也就是連接至較低版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   您可以連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016 所建立的專案時 SQL Server 2012。  
  
||||||||  
|-|-|-|-|-|-|-|  
|**專案類型與目標伺服器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005<br /> (版本： 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008<br /> (版本： 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 <br />(Version:13.x)|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||是||
|Azure SQL DB||||||是|
  
> [!IMPORTANT]  
> 根據專案類型，但不是根據版本的資料庫物件的轉換會執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]您已連線到。 如果是[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005年專案轉換為實行依照[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 即使您已連線到較高版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016年)。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步處理 SQL Server 中繼資料  
有關的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫不會自動更新。 中的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管 是中繼資料的快照集，當您第一次連接至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，或最後一個每當您手動更新的中繼資料。 您可以手動更新所有資料庫，或任何單一資料庫或資料庫物件的中繼資料。  
  
**同步處理中繼資料**  
  
1.  請確定您連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
2.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管，選取之資料庫旁邊的核取方塊，或您想要更新的結構描述的資料庫。  
  
    例如，若要更新所有資料庫的中繼資料，選取旁**資料庫**。  
  
3.  以滑鼠右鍵按一下**資料庫**，或個別的資料庫或資料庫結構描述，然後再選取**同步處理資料庫**。  
  
## <a name="next-step"></a>下一個步驟  
移轉的下一個步驟取決於您專案的需求：  
  
-   若要自訂 Oracle 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫和結構描述，請參閱[對應至 SQL Server 結構描述的 Oracle 結構描述&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)。  
  
-   若要自訂專案的組態選項，請參閱[設定專案選項&#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。  
  
-   若要自訂的來源和目標資料類型對應，請參閱[對應 Oracle 和 SQL Server 資料類型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
-   如果您不需要執行任何這些工作，您可以將轉換成的 Oracle 資料庫物件定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件定義。 如需詳細資訊，請參閱[轉換 Oracle 結構描述&#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[SQL server 資料庫移轉 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
