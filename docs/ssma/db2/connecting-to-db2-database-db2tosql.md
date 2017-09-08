---
title: "連接到 DB2 資料庫 (DB2ToSQL) |Microsoft 文件"
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
ms.assetid: 5eb5801d-f0c3-4127-97c0-0b1ef49f4844
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3c7d7f8162968d579f1e3e1346fb2498ebf941cb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-db2-database-db2tosql"></a>連接到 DB2 資料庫 (DB2ToSQL)
若要將 DB2 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您必須連接到您想要移轉的 DB2 資料庫。 當您連線時，SSMA 會取得所有 DB2 結構描述的相關中繼資料中，然後顯示在 DB2 中繼資料總管 窗格中。 SSMA 會儲存在資料庫伺服器的相關資訊，但不會儲存密碼。  
  
資料庫的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接，如果您想要的使用中連接到資料庫。  
  
DB2 資料庫的相關中繼資料不會自動更新。 相反地，如果您想要更新的中繼資料，在 DB2 中繼資料總管 中，您必須手動更新它。 如需詳細資訊，請參閱本主題稍後的 「 重新整理 DB2 中繼資料 」 一節。  
  
## <a name="required-db2-permissions"></a>必要的 DB2 權限  
使用者的授權會定義的命令和物件可供使用者清單。 這份清單，藉此控制使用者動作。 DB2 中沒有預先決定的群組，如授權、 執行個體層級和 DB2 資料庫的層級的權限。 這可讓 SSMA 從連接的使用者所擁有的結構描述中取得中繼資料。 若要取得其他結構描述中物件的中繼資料，並再將這些結構描述中的物件，帳戶必須具有下列權限：  
  
-   移轉結構描述的結構描述存取通常授與 PUBLIC 除非在建立使用限制關鍵字  
  
-   資料移轉的資料存取需要的資料存取  
  
## <a name="establishing-a-connection-to-db2"></a>建立 DB2 的連接  
當您連接至資料庫時，SSMA 會讀取資料庫中繼資料，然後將此中繼資料加入至專案檔。 此中繼資料時，會使用 SSMA 會將轉換物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法，以及當它能將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以瀏覽此中繼資料，在 DB2 中繼資料總管 窗格中的，並檢視個別資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 您嘗試連接之前，請確定資料庫伺服器正在執行，且可接受連接。  
  
**若要連接至 DB2**  
  
1.  在**檔案**功能表上，選取**連接到 DB2**。  
  
    如果您先前已連線至 DB2，命令名稱將**重新連接至 DB2**。  
  
2.  在**提供者**方塊，您會看到**OLE DB 提供者**這是目前唯一的 DB2 用戶端存取提供者。  
  
3.  在**管理員**您可以選取方塊**Db2 for zOs**，或**DB2 for luw 會**  
  
4.  在**模式**方塊中，選取 **標準模式**，或**連接字串模式**。  
  
    使用指定的伺服器名稱和連接埠的標準模式。 若要手動指定 DB2 服務名稱中使用服務名稱模式。 使用連接字串模式提供完整連接字串。  
  
5.  如果您選取**標準模式**，提供下列值：  
  
    -   在**伺服器名稱**方塊中，輸入或選取的名稱或資料庫伺服器的 IP 位址。  
  
    -   如果資料庫伺服器未設定為接受連接的預設通訊埠 (1521)，請輸入用於在 DB2 連接的連接埠號碼**伺服器連接埠**方塊。  
  
    -   在**伺服器連接埠**方塊中，輸入的 TCP/IP 連接埠號碼。  
  
    -   在**初始目錄**方塊中，輸入資料庫名稱  
  
    -   在**使用者名**方塊中，輸入具有必要權限的 DB2 帳戶。  
  
    -   在**密碼**方塊中，指定的使用者名稱輸入的密碼。  
  
6.  如果您選取**連接字串模式**，提供連接字串中的**連接字串**方塊。  
  
    下列範例會顯示 OLE DB 連接字串：  
  
    `Provider=OraOLEDB.DB2;Data Source=MyDB2DB;User Id=myUsername;Password=myPassword;`  
  
    下列範例示範使用整合式的安全性的 DB2 用戶端連接字串：  
  
    `Data Source=MyDB2DB;Integrated Security=yes;`  
  
    如需詳細資訊，請參閱[連接至 Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)。  
  
## <a name="reconnecting-to-db2"></a>重新連接至 DB2 伺服器  
資料庫伺服器的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接，如果您想要的使用中連接到資料庫。 您可以離線直到您想要更新中繼資料，資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，並將資料移轉。  
  
## <a name="refreshing-db2-metadata"></a>重新整理 DB2 中繼資料  
DB2 資料庫的相關中繼資料不會自動重新整理。 DB2 中繼資料總管 中的中繼資料是快照集的中繼資料，當您第一次連接時，或您手動重新整理中繼資料的最後一次。 您可以手動更新所有結構描述、 在單一結構描述或個別的資料庫物件的中繼資料。  
  
**若要重新整理中繼資料**  
  
1.  請確定您已連線到資料庫。  
  
2.  在 DB2 中繼資料總管，選取您想要更新每個結構描述或資料庫物件旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下**結構描述**，個別結構描述或資料庫物件，然後再選取**從資料庫重新整理**。  
  
    如果您沒有作用中連線，將會顯示 SSMA**連接到 DB2**對話方塊，讓您可以連線。  
  
4.  在重新整理從資料庫 對話方塊，指定要重新整理的物件。  
  
    -   若要重新整理物件，請按一下**Active**物件，直到出現箭號相鄰的欄位。  
  
    -   若要防止進行重新整理的物件，請按一下**Active**相鄰的物件，直到欄位**X**隨即出現。  
  
    -   若要重新整理或拒絕物件目錄，按一下  **Active**類別資料夾旁的欄位。  
  
    若要檢視定義的色彩編碼，請按一下**圖例** 按鈕。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>下一個步驟  
  
-   移轉程序的下一個步驟是[連接到 SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)。  
  
## <a name="see-also"></a>另請參閱  
[DB2 資料庫移轉至 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

