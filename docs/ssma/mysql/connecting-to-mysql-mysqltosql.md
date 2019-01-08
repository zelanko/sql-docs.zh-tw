---
title: 連接到 MySQL (MySQLToSQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 233b6824ef527a9ed4e7e02164a08e31e41f3699
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52409496"
---
# <a name="connecting-to-mysql-mysqltosql"></a>連線到 MySQL (MySQLToSQL)
若要將 MySQL 資料庫移轉至 SQL Server 或 SQL Azure，您必須連接至您想要移轉的 MySQL 資料庫。 當您連線時，SSMA 中取得所有 MySQL 結構描述的相關中繼資料，然後顯示 MySQL 中繼資料總管 窗格中。 SSMA 會儲存在資料庫伺服器的相關資訊，但不會儲存密碼。  
  
資料庫的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連線，如果您想要的使用中連接到資料庫。  
  
MySQL 資料庫的相關中繼資料不會自動更新。 相反地，如果您想要更新 MySQL 中繼資料總管 中的中繼資料，您必須以手動方式更新它。 如需詳細資訊，請參閱本主題稍後的 「 重新整理 MySQL 中繼資料 」 一節。  
  
## <a name="required-mysql-permissions"></a>必要的 MySQL 權限  
用來連接到 MySQL 資料庫的帳戶至少必須有**CONNECT**權限。 這可讓 SSMA 從連線的使用者所擁有的結構描述取得中繼資料。 若要取得其他結構描述中物件的中繼資料，然後將這些結構描述中的物件轉換的帳戶必須具有下列權限：  
  
-   [顯示] 資料庫物件的權限  
  
-   'Information_schema' 的 'SELECT' 權限  
  
-   在 mysql （適用於 Udf) 上的 'SELECT' 權限  
  
## <a name="establishing-a-connection-to-mysql"></a>建立 MySQL 連線  
當您連接到資料庫時，SSMA 讀取資料庫中繼資料，然後將此中繼資料新增至專案檔。 SSMA 會將物件轉換成 SQL Server 或 SQL Azure 的語法，以及將資料移轉到 SQL Server 或 SQL Azure 時，會使用此中繼資料。 您可以瀏覽這個 MySQL 中繼資料總管 窗格中的中繼資料，然後檢閱個別的資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 您嘗試連接之前，請確定資料庫伺服器正在執行，而且可以接受連線。  
  
**若要連線至 MySQL**  
  
1.  在 **檔案**功能表上，選取**連線到 MySQL** （專案建立之後將會啟用此選項）。  
  
    如果您先前已連線至 MySQL，命令名稱會是**重新連接至 MySQL**。  
  
2.  在 **提供者**方塊中，選取 MySQL ODBC 5.1 驅動程式 （受信任）。 它是以標準模式的預設提供者。  
  
3.  在 **模式**方塊中，選取**標準模式**。 也是預設模式。  
  
    使用指定的伺服器名稱和連接埠的標準模式。  
  
4.  在 **標準模式**，提供下列值：  
  
    1.  在 **伺服器名稱**方塊中，輸入 MySQL 伺服器名稱。 在 **伺服器的連接埠**方塊中，輸入連接埠號碼為 3306。 它是預設的連接埠。  
  
    2.  在 **使用者名**方塊中，輸入 MySQL 帳戶具有必要的權限。  
  
    3.  在 **密碼**方塊中，指定的使用者名稱輸入的密碼。  
  
5.  **SSL:** 如果您想要安全地連線至 MySQL，請使用的安全通訊端層 (SSL)，藉由檢查**SSL**核取方塊。  
  
6.  **設定：** 它提供一個選項來設定 MySQL 透過安全通訊端層 (SSL) 連線。  
  
    > [!NOTE]  
    > 若要啟用**設定**，必須將 SSL **，則為 True**。  
  
    按一下 [設定] 按鈕，對話方塊隨即出現。 若要使用加密，而連線至 MySQL 資料庫，以顯示在對話方塊中的下列三個憑證檔案的路徑必須被定義 [隱私權增強式郵件憑證 (PEM)]:  
  
    -   **SSL 憑證授權單位：** 一份信任 SSL Ca 的指定檔案的路徑。  
  
    -   **SSL 憑證：** 指定要用來建立安全連線的 SSL 憑證檔案的名稱。  
  
    -   **SSL 金鑰：** 指定要用來建立安全連線的 SSL 金鑰檔案的名稱。  
  
    > [!NOTE]  
    > -   **確定**已提供所需的資訊時，已啟用 按鈕。 如果任一檔案路徑無效，則會維持停用 [確定] 按鈕。  
    > -   **取消** 按鈕關閉對話方塊並**關閉**SSL 選項，從主要的連接形式。  
  
7.  如需詳細資訊，請參閱 <<c0> [ 連接到 MySQL &#40;MySQLToSQL&#41;</c0>](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>重新連線至 MySQL  
資料庫伺服器的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連線，如果您想要的使用中連接到資料庫。 您想要更新中繼資料、 將資料庫物件載入 SQL Server 或 SQL Azure 移轉資料之前，您可以離線工作。  
  
## <a name="refreshing-mysql-metadata"></a>重新整理 MySQL 中繼資料  
MySQL 資料庫的相關中繼資料不會自動重新整理。 MySQL 中繼資料總管 中的中繼資料是快照集的中繼資料，當您第一次連接時或您手動重新整理中繼資料的最後一次。 您可以手動更新所有結構描述、 單一結構描述，或個別的資料庫物件的中繼資料。  
  
**若要重新整理中繼資料**  
  
1.  請確定您已連線到資料庫。  
  
2.  在 [MySQL 中繼資料總管] 中，選取您想要更新每個結構描述或資料庫物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下**結構描述**，或個別的結構描述或資料庫物件，然後按**從資料庫重新整理**。  
  
    如果您沒有作用中連線，將會顯示 SSMA**連接到 MySQL**對話方塊，讓您可以連線。  
  
4.  在從資料庫 對話方塊中重新整理中，指定要重新整理的物件。  
  
    -   若要重新整理物件，請按一下**Active**物件，直到出現箭號旁的欄位。  
  
    -   若要防止物件正在重新整理，請按一下**Active**欄位旁的物件，直到**X**隨即出現。  
  
    -   重新整理，或拒絕物件的類別，請按一下**Active**類別資料夾旁的欄位。  
  
    -   若要檢視的定義的色彩編碼，請按一下**圖例** 按鈕。  
  
5.  按一下 [確定] 。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[連接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[移轉 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
