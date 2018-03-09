---
title: "連接至 MySQL (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 291f10d4f045747266297287903ba4cf900c09c5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-to-mysql-mysqltosql"></a>連接至 MySQL (MySQLToSQL)
若要移轉至 SQL Server 或 SQL Azure 的 MySQL 資料庫，您必須連接到您想要移轉的 MySQL 資料庫。 當您連線時，SSMA 會取得所有 MySQL 結構描述的相關中繼資料中，然後顯示 MySQL 中繼資料總管 窗格中。 SSMA 會儲存在資料庫伺服器的相關資訊，但不會儲存密碼。  
  
資料庫的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接，如果您想要的使用中連接到資料庫。  
  
MySQL 資料庫的相關中繼資料不會自動更新。 相反地，如果您想要更新 MySQL 中繼資料總管 中的中繼資料，您必須手動更新它。 如需詳細資訊，請參閱本主題稍後的 「 重新整理 MySQL 中繼資料 」 一節。  
  
## <a name="required-mysql-permissions"></a>需要的 MySQL 權限  
用來連接到 MySQL 資料庫的帳戶至少必須有**連接**權限。 這可讓 SSMA 從連接的使用者所擁有的結構描述中取得中繼資料。 若要取得其他結構描述中物件的中繼資料，並再將這些結構描述中的物件，帳戶必須具有下列權限：  
  
-   '顯示' 的資料庫物件的權限  
  
-   ' SELECT' 'Information_schema' 上的權限  
  
-   在 mysql （適用於 Udf) 上的 'SELECT' 權限  
  
## <a name="establishing-a-connection-to-mysql"></a>建立連接到 MySQL  
當您連接至資料庫時，SSMA 會讀取資料庫中繼資料，然後將此中繼資料加入至專案檔。 SSMA 會將物件轉換成 SQL Server 或 SQL Azure 的語法，以及它能將資料移轉至 SQL Server 或 SQL Azure 時，會使用此中繼資料。 您可以瀏覽這個 MySQL 中繼資料總管 窗格中的中繼資料，然後檢閱個別的資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 您嘗試連接之前，請確定資料庫伺服器正在執行，且可接受連接。  
  
**若要連接到 MySQL**  
  
1.  在**檔案**功能表上，選取**連接到 MySQL** （專案建立之後將會啟用此選項）。  
  
    如果您先前連線到 MySQL，命令名稱將**重新連接到 MySQL**。  
  
2.  在**提供者**方塊中，選取 MySQL ODBC 5.1 驅動程式 （信任）。 它是在標準模式的預設提供者。  
  
3.  在**模式**方塊中，選取**標準模式**。 也是預設模式。  
  
    使用指定的伺服器名稱和連接埠的標準模式。  
  
4.  在**標準模式**，提供下列值：  
  
    1.  在**伺服器名稱**方塊中，輸入 MySQL 伺服器名稱。 在**伺服器連接埠**方塊中，輸入要 3306 的連接埠號碼。 它是預設通訊埠。  
  
    2.  在**使用者名**方塊中，輸入 MySQL 帳戶具有必要的權限。  
  
    3.  在**密碼**方塊中，指定的使用者名稱輸入的密碼。  
  
5.  **SSL:**如果您想要安全地連接到 MySQL，請檢查使用的安全通訊端層 (SSL) **SSL**核取方塊。  
  
6.  **設定：** ，提供設定 MySQL 透過安全通訊端層 (SSL) 連線的選項。  
  
    > [!NOTE]  
    > 若要啟用**設定**，SSL 必須設為**True**。  
  
    按下按鈕 「 設定 」，對話方塊隨即出現。 若要使用加密，而連接到 MySQL 資料庫，出現在對話方塊中的下列三種憑證檔案的路徑必須被定義 [隱私權增強式郵件憑證 (PEM)]:  
  
    -   **SSL 憑證授權單位：**信任 SSL Ca 的清單中指定檔案的路徑。  
  
    -   **SSL 憑證：**指定要用來建立安全連線的 SSL 憑證檔案的名稱。  
  
    -   **SSL 金鑰：**指定要用來建立安全連線的 SSL 金鑰檔案的名稱。  
  
    > [!NOTE]  
    > -   **確定**按鈕已啟用時未提供必要的資訊。 如果任一檔案路徑無效，將會維持停用 [確定] 按鈕。  
    > -   **取消**按鈕關閉對話方塊和**關閉**SSL 選項，從主要的連線表單。  
  
7.  如需詳細資訊，請參閱[連接到 MySQL &#40;MySQLToSQL &#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>重新連接到 MySQL  
資料庫伺服器的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接，如果您想要的使用中連接到資料庫。 您要更新中繼資料，請載入 SQL Server 或 SQL Azure 的資料庫物件並移轉資料之前，您可以離線工作。  
  
## <a name="refreshing-mysql-metadata"></a>重新整理 MySQL 中繼資料  
MySQL 資料庫的相關中繼資料不會自動重新整理。 MySQL 中繼資料總管 中的中繼資料是快照集的中繼資料，當您第一次連接時，或您手動重新整理中繼資料的最後一次。 您可以手動更新所有結構描述、 在單一結構描述或個別的資料庫物件的中繼資料。  
  
**若要重新整理中繼資料**  
  
1.  請確定您已連線到資料庫。  
  
2.  在 MySQL 中繼資料總管，選取您想要更新每個結構描述或資料庫物件旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下**結構描述**，個別結構描述或資料庫物件，然後再選取**從資料庫重新整理**。  
  
    如果您沒有作用中連線，將會顯示 SSMA**連接到 MySQL**對話方塊，讓您可以連線。  
  
4.  在重新整理從資料庫 對話方塊，指定要重新整理的物件。  
  
    -   若要重新整理物件，請按一下**Active**物件，直到出現箭號相鄰的欄位。  
  
    -   若要防止進行重新整理的物件，請按一下**Active**相鄰的物件，直到欄位**X**隨即出現。  
  
    -   若要重新整理或拒絕物件目錄，按一下  **Active**類別資料夾旁的欄位。  
  
    -   若要檢視定義的色彩編碼，請按一下**圖例** 按鈕。  
  
5.  按一下 [確定] 。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[連接到 SQL Server &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>請參閱  
[將 MySQL 資料庫移轉至 SQL Server-Azure SQL DB &#40;MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
