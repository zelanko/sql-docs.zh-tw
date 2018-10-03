---
title: 連接到 Oracle 資料庫 (OracleToSQL) |Microsoft Docs
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
manager: v-thobro
ms.openlocfilehash: 4ad868122fd8986c642bace1b2c9cf419bb89182
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47634327"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>連線到 Oracle Database (OracleToSQL)
若要將 Oracle 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必須連接到您想要移轉的 Oracle 資料庫。 當您連線時，SSMA 中取得所有 Oracle 結構描述的相關中繼資料，然後顯示 Oracle 中繼資料總管 窗格中。 SSMA 會儲存在資料庫伺服器的相關資訊，但不會儲存密碼。  
  
資料庫的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連線，如果您想要的使用中連接到資料庫。  
  
Oracle 資料庫的相關中繼資料不會自動更新。 相反地，如果您想要更新 Oracle 中繼資料總管 中的中繼資料，您必須以手動方式更新它。 如需詳細資訊，請參閱本主題稍後的 「 重新整理 Oracle 中繼資料 」 一節。  
  
## <a name="required-oracle-permissions"></a>必要的 Oracle 權限  
用來連接到 Oracle 資料庫的帳戶至少必須有**CONNECT**權限。 這可讓 SSMA 從連線的使用者所擁有的結構描述取得中繼資料。 若要取得其他結構描述中物件的中繼資料，然後將這些結構描述中的物件轉換的帳戶必須具有下列權限：  
  
-   建立任何程序  
  
-   執行任何程序  
  
-   選取任何資料表  
  
-   選取任何順序  
  
-   建立任何類型  
  
-   建立任何觸發程序  
  
-   選取任何字典  
  
## <a name="establishing-a-connection-to-oracle"></a>建立連線至 Oracle  
當您連接到資料庫時，SSMA 讀取資料庫中繼資料，然後將此中繼資料新增至專案檔。 將轉換物件時，使用此中繼資料的 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法，以及當它將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以瀏覽 Oracle 中繼資料總管 窗格中的此中繼資料，然後檢閱個別的資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 您嘗試連接之前，請確定資料庫伺服器正在執行，而且可以接受連線。  
  
**若要連接到 Oracle**  
  
1.  在 **檔案**功能表上，選取**連接到 Oracle**。  
  
    如果您先前連線到 Oracle，命令名稱會是**重新連接到 Oracle**。  
  
2.  在 **提供者**方塊中，選取**Oracle 用戶端提供者**或**OLE DB 提供者**，取決於已安裝的提供者。 預設值是 Oracle 用戶端。  
  
3.  在 **模式**方塊中，選取**標準模式**， **TNSNAME 模式**，或**連接字串模式**。  
  
    使用指定的伺服器名稱和連接埠的標準模式。 若要手動指定 Oracle 服務名稱中使用服務名稱模式。 您可以使用連接字串模式來提供完整的連接字串。  
  
4.  如果您選取**標準模式**，提供下列值：  
  
    1.  在 **伺服器名稱**方塊中，輸入或選取的資料庫伺服器的 IP 位址的名稱。  
  
    2.  如果資料庫伺服器未設定為接受連接的預設連接埠 (1521) 中，輸入用於在 Oracle 連接的連接埠號碼**伺服器的連接埠** 方塊中。  
  
    3.  在  **Oracle SID**方塊中，輸入的系統識別項。  
  
    4.  在 **使用者名**方塊中，輸入具有必要的權限的 Oracle 帳戶。  
  
    5.  在 **密碼**方塊中，指定的使用者名稱輸入的密碼。  
  
5.  如果您選取**TNSNAME 模式**，提供下列值：  
  
    1.  在 **連線識別碼**方塊中，輸入連接資料庫的識別碼 （TNS 別名）。  
  
    2.  在 **使用者名**方塊中，輸入具有必要的權限的 Oracle 帳戶。  
  
    3.  在 **密碼**方塊中，指定的使用者名稱輸入的密碼。  
  
6.  如果您選取**連接字串模式**，以提供連接字串**連接字串** 方塊中。  
  
    下列範例顯示的 OLE DB 連接字串：  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    下列範例顯示使用整合式的安全性的 Oracle 用戶端連接字串：  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    如需詳細資訊，請參閱 <<c0> [ 連接到 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)。</c0>  
  
## <a name="reconnecting-to-oracle"></a>重新連接到 Oracle  
資料庫伺服器的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連線，如果您想要的使用中連接到資料庫。 您可以離線直到您想要更新中繼資料，資料庫物件載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並移轉資料。  
  
## <a name="refreshing-oracle-metadata"></a>重新整理 Oracle 中繼資料  
Oracle 資料庫的相關中繼資料不會自動重新整理。 Oracle 中繼資料總管 中的中繼資料是快照集的中繼資料，當您第一次連接時或您手動重新整理中繼資料的最後一次。 您可以手動更新所有結構描述、 單一結構描述，或個別的資料庫物件的中繼資料。  
  
**若要重新整理中繼資料**  
  
1.  請確定您已連線到資料庫。  
  
2.  在 Oracle 中繼資料總管 中，選取您想要更新每個結構描述或資料庫物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下**結構描述**，或個別的結構描述或資料庫物件，然後按**從資料庫重新整理**。  
  
    如果您沒有作用中連線，將會顯示 SSMA**連接到 Oracle**對話方塊，讓您可以連線。  
  
4.  在從資料庫 對話方塊中重新整理中，指定要重新整理的物件。  
  
    -   若要重新整理物件，請按一下**Active**物件，直到出現箭號旁的欄位。  
  
    -   若要防止物件正在重新整理，請按一下**Active**欄位旁的物件，直到**X**隨即出現。  
  
    -   重新整理，或拒絕物件的類別，請按一下**Active**類別資料夾旁的欄位。  
  
    若要檢視的定義的色彩編碼，請按一下**圖例** 按鈕。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>下一個步驟  
  
-   移轉程序的下一個步驟是[連接到 SQL Server 的執行個體](connecting-to-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[移轉的 Oracle 資料庫到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
