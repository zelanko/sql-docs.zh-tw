---
title: 連接到 MySQL （MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6cb47c0f06d7133b8c7454a4fa538937a0e78e19
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103175"
---
# <a name="connecting-to-mysql-mysqltosql"></a>連線到 MySQL (MySQLToSQL)
若要將 MySQL 資料庫遷移至 SQL Server 或 SQL Azure，您必須連線到您想要遷移的 MySQL 資料庫。 當您連線時，SSMA 會取得所有 MySQL 架構的相關中繼資料，然後在 [MySQL 中繼資料瀏覽器] 窗格中顯示。 SSMA 會儲存資料庫伺服器的相關資訊，但不會儲存密碼。  
  
您的資料庫連接會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想要資料庫的使用中連接，就必須重新連接。  
  
MySQL 資料庫的相關中繼資料不會自動更新。 相反地，如果您想要更新 MySQL Metadata Explorer 中的中繼資料，就必須手動更新它。 如需詳細資訊，請參閱本主題稍後的「重新整理 MySQL 中繼資料」一節。  
  
## <a name="required-mysql-permissions"></a>必要的 MySQL 許可權  
用來連線到 MySQL 資料庫的帳戶必須至少具有**connect**許可權。 這可讓 SSMA 從連接使用者所擁有的架構取得中繼資料。 若要取得其他架構中物件的中繼資料，然後轉換這些架構中的物件，此帳戶必須具備下列許可權：  
  
-   資料庫物件上的「顯示」許可權  
  
-   ' Information_schema ' 上的 ' SELECT ' 許可權  
  
-   Mysql 上的「選取」許可權（適用于 Udf）  
  
## <a name="establishing-a-connection-to-mysql"></a>建立 MySQL 的連線  
當您連接到資料庫時，SSMA 會讀取資料庫中繼資料，然後將此中繼資料加入至專案檔。 當 SSMA 將物件轉換成 SQL Server 或 SQL Azure 語法，以及當它將資料移轉至 SQL Server 或 SQL Azure 時，會使用此中繼資料。 您可以在 [MySQL 中繼資料瀏覽器] 窗格中流覽此中繼資料，並查看個別資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 嘗試連接之前，請確定資料庫伺服器正在執行，而且可以接受連接。  
  
**若要連接到 MySQL**  
  
1.  在 [檔案]**功能表上，選取 [連線****到 MySQL]** （在建立專案之後，將會啟用此選項）。  
  
    如果您先前已連線到 MySQL，命令名稱會**重新連接到 mysql**。  
  
2.  在 [**提供者**] 方塊中，選取 [MySQL ODBC 5.1 驅動程式（信任）]。 這是標準模式中的預設提供者。  
  
3.  在 [**模式]** 方塊中，選取 [**標準模式]**。 也是預設模式。  
  
    使用標準模式來指定伺服器名稱和埠。  
  
4.  在 [**標準模式]** 中，提供下列值：  
  
    1.  在 [**伺服器名稱**] 方塊中，輸入 MySQL 伺服器名稱。 在 [**伺服器埠**] 方塊中，將埠號碼輸入為3306。 這是預設通訊埠。  
  
    2.  在 [**使用者名稱**] 方塊中，輸入具有必要許可權的 MySQL 帳戶。  
  
    3.  在 [**密碼**] 方塊中，輸入指定之使用者名稱的密碼。  
  
5.  **SSL：** 如果您想要安全地連線到 MySQL，請核取 [ **SSL** ] 核取方塊，以使用安全通訊端層（ssl）。  
  
6.  **設定：** 它提供選項來設定透過安全通訊端層（SSL）的 MySQL 連線。  
  
    > [!NOTE]  
    > 若要**啟用 [設定]**，SSL 必須設定為 [ **True**]。  
  
    當您按一下 [設定] 按鈕時，就會出現對話方塊。 若要在連接到 MySQL 資料庫時使用加密，必須定義對話方塊中的下列三個憑證檔案的路徑 [隱私權增強郵件憑證（PEM）]：  
  
    -   **SSL 憑證頒發機構單位：** 指定具有信任 SSL Ca 清單之檔案的路徑。  
  
    -   **SSL 憑證：** 指定要用來建立安全連線的 SSL 憑證檔案名。  
  
    -   **SSL 金鑰：** 指定要用來建立安全連線的 SSL 金鑰檔名稱。  
  
    > [!NOTE]  
    > -   提供必要的資訊時，會啟用 [**確定]** 按鈕。 如果有任何檔案路徑無效，[確定] 按鈕將會保持停用狀態。  
    > -   [**取消**] 按鈕會關閉對話方塊，並從主要連接窗**體關閉 [** SSL] 選項。  
  
7.  如需詳細資訊，請參閱[連接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>重新連接至 MySQL  
您的資料庫伺服器連接會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想要資料庫的使用中連接，就必須重新連接。 您可以離線工作，直到您想要更新中繼資料、將資料庫物件載入 SQL Server 或 SQL Azure，以及遷移資料為止。  
  
## <a name="refreshing-mysql-metadata"></a>重新整理 MySQL 中繼資料  
MySQL 資料庫的相關中繼資料不會自動重新整理。 當您第一次連接時，或上次手動重新整理中繼資料時，MySQL 中繼資料 Explorer 中的中繼資料就是中繼資料的快照集。 您可以手動更新所有架構、單一架構或個別資料庫物件的中繼資料。  
  
**重新整理中繼資料**  
  
1.  請確定您已連接到資料庫。  
  
2.  在 [MySQL Metadata Explorer] 中，選取您要更新之每個架構或資料庫物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下 [**架構**] 或個別的架構或資料庫物件，然後選取 [**從資料庫**重新整理]。  
  
    如果您沒有使用中的連線，SSMA 會顯示 [**連接到 MySQL** ] 對話方塊，讓您可以連線。  
  
4.  在 [從資料庫重新整理] 對話方塊中，指定要重新整理的物件。  
  
    -   若要重新整理物件，請按一下物件旁的**現用**欄位，直到箭號出現為止。  
  
    -   若要防止重新整理物件，請按一下物件旁的**現用**欄位，直到**X**出現為止。  
  
    -   若要重新整理或拒絕物件的類別目錄，請按一下 [類別] 資料夾旁的 [**作用中] 欄位。**  
  
    -   若要查看色彩編碼的定義，請按一下 [**圖例**] 按鈕。  
  
5.  按一下 [確定]  。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是[連接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料庫遷移至 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
