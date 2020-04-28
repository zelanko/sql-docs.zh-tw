---
title: 連接到 Oracle Database （OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: fc25c36a0d0133975414f4c7270da2974b552f40
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266195"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>連線到 Oracle Database (OracleToSQL)
若要將 Oracle 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移至，您必須連接到您想要遷移的 oracle 資料庫。 當您連接時，SSMA 會取得所有 Oracle 架構的相關中繼資料，然後在 [Oracle 中繼資料瀏覽器] 窗格中顯示。 SSMA 會儲存資料庫伺服器的相關資訊，但不會儲存密碼。  
  
您的資料庫連接會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想要資料庫的使用中連接，就必須重新連接。  
  
Oracle 資料庫的相關中繼資料不會自動更新。 相反地，如果您想要更新 Oracle Metadata Explorer 中的中繼資料，就必須手動更新它。 如需詳細資訊，請參閱本主題稍後的「重新整理 Oracle 中繼資料」一節。  
  
## <a name="required-oracle-permissions"></a>必要的 Oracle 許可權  
用來連接到 Oracle 資料庫的帳戶必須至少具有**connect**許可權。 這可讓 SSMA 從連接使用者所擁有的架構取得中繼資料。 若要取得其他架構中物件的中繼資料，然後轉換這些架構中的物件，此帳戶必須具備下列許可權：  
  
-   建立任何程式  
  
-   執行任何程式  
  
-   選取任何資料表  
  
-   選取任何順序  
  
-   建立任何類型  
  
-   建立任何觸發程式  
  
-   選取任何字典  
  
## <a name="establishing-a-connection-to-oracle"></a>建立與 Oracle 的連接  
當您連接到資料庫時，SSMA 會讀取資料庫中繼資料，然後將此中繼資料加入至專案檔。 當 SSMA 將物件轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法，以及將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，會使用此中繼資料。 您可以在 [Oracle 中繼資料瀏覽器] 窗格中流覽此中繼資料，並查看個別資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 嘗試連接之前，請確定資料庫伺服器正在執行，而且可以接受連接。  
  
**連接到 Oracle**  
  
1.  **在 [檔案**] 功能表上，選取 **[連接到 Oracle]**。  
  
    如果您先前已連接到 Oracle，命令名稱將會**重新連接到 oracle**。  
  
2.  根據安裝的提供者，在 [**提供者**] 方塊中選取 [ **Oracle 用戶端提供者**] 或 [ **OLE DB 提供者**]。 預設值為 [Oracle client]。  
  
3.  在 [**模式]** 方塊中，選取 [**標準模式]**、[ **TNSNAME 模式]** 或 [**連接字串模式]**。  
  
    使用標準模式來指定伺服器名稱和埠。 使用服務名稱模式來手動指定 Oracle 服務名稱。 使用連接字串模式來提供完整的連接字串。  
  
4.  如果您選取 [**標準模式]**，請提供下列值：  
  
    1.  在 [**伺服器名稱**] 方塊中，輸入或選取資料庫伺服器的名稱或 IP 位址。  
  
    2.  如果資料庫伺服器未設定為接受預設通訊埠（1521）上的連接，請在 [**伺服器埠**] 方塊中輸入用於 Oracle 連接的通訊埠編號。  
  
    3.  在 [ **ORACLE SID** ] 方塊中，輸入系統識別碼。  
  
    4.  在 [**使用者名稱**] 方塊中，輸入具有必要許可權的 Oracle 帳戶。  
  
    5.  在 [**密碼**] 方塊中，輸入指定之使用者名稱的密碼。  
  
5.  如果您選取 [ **TNSNAME 模式]**，請提供下列值：  
  
    1.  在 [**連接識別碼]** 方塊中，輸入資料庫的 Connect IDENTIFIER （TNS alias）。  
  
    2.  在 [**使用者名稱**] 方塊中，輸入具有必要許可權的 Oracle 帳戶。  
  
    3.  在 [**密碼**] 方塊中，輸入指定之使用者名稱的密碼。  
  
6.  如果您選取 [**連接字串模式]**，請在 [**連接字串**] 方塊中提供連接字串。  
  
    下列範例顯示 OLE DB 連接字串：  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    下列範例顯示使用整合式安全性的 Oracle 用戶端連接字串：  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    如需詳細資訊，請參閱[連接到 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)。  
  
## <a name="reconnecting-to-oracle"></a>重新連接到 Oracle  
您的資料庫伺服器連接會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想要資料庫的使用中連接，就必須重新連接。 您可以離線工作，直到您想要更新中繼資料、將資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件載入及遷移資料為止。  
  
## <a name="refreshing-oracle-metadata"></a>重新整理 Oracle 中繼資料  
Oracle 資料庫的相關中繼資料不會自動重新整理。 當您第一次連接時，或上次手動重新整理中繼資料時，Oracle Metadata Explorer 中的中繼資料就是中繼資料的快照集。 您可以手動更新所有架構、單一架構或個別資料庫物件的中繼資料。  
  
**重新整理中繼資料**  
  
1.  請確定您已連接到資料庫。  
  
2.  在 [Oracle 中繼資料 Explorer] 中，選取您想要更新之每個架構或資料庫物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下 [**架構**] 或個別的架構或資料庫物件，然後選取 [**從資料庫**重新整理]。  
  
    如果您沒有使用中的連接，SSMA 會顯示 [**連接到 Oracle** ] 對話方塊，讓您可以連接。  
  
4.  在 [從資料庫重新整理] 對話方塊中，指定要重新整理的物件。  
  
    -   若要重新整理物件，請按一下物件旁的**現用**欄位，直到箭號出現為止。  
  
    -   若要防止重新整理物件，請按一下物件旁的**現用**欄位，直到**X**出現為止。  
  
    -   若要重新整理或拒絕物件的類別目錄，請按一下 [類別] 資料夾旁的 [**作用中] 欄位。**  
  
    若要查看色彩編碼的定義，請按一下 [**圖例**] 按鈕。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>後續步驟  
  
-   遷移程式的下一個步驟是[連接到 SQL Server 的實例](connecting-to-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Oracle 資料庫移轉至 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
