---
title: 連接到 Oracle 資料庫 (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 0673afd74ef1c11b9c800d128ea25e0189a635e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-oracle-database-oracletosql"></a>連接到 Oracle 資料庫 (OracleToSQL)
若要將 Oracle 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您必須連接到您想要移轉的 Oracle 資料庫。 當您連線時，SSMA 會取得所有 Oracle 結構描述的相關中繼資料中，然後顯示 Oracle 中繼資料總管 窗格中。 SSMA 會儲存在資料庫伺服器的相關資訊，但不會儲存密碼。  
  
資料庫的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接，如果您想要的使用中連接到資料庫。  
  
Oracle 資料庫的相關中繼資料不會自動更新。 相反地，如果您想要更新 Oracle 中繼資料總管 中的中繼資料，您必須手動更新它。 如需詳細資訊，請參閱本主題稍後的 「 重新整理 Oracle 中繼資料 」 一節。  
  
## <a name="required-oracle-permissions"></a>必要的 Oracle 權限  
用來連接到 Oracle 資料庫的帳戶至少必須有**連接**權限。 這可讓 SSMA 從連接的使用者所擁有的結構描述中取得中繼資料。 若要取得其他結構描述中物件的中繼資料，並再將這些結構描述中的物件，帳戶必須具有下列權限：  
  
-   建立任何程序  
  
-   執行任何程序  
  
-   選取任何資料表  
  
-   選取任何順序  
  
-   建立任何類型  
  
-   建立任何觸發程序  
  
-   選取任何字典  
  
## <a name="establishing-a-connection-to-oracle"></a>建立 Oracle 的連接  
當您連接至資料庫時，SSMA 會讀取資料庫中繼資料，然後將此中繼資料加入至專案檔。 此中繼資料時，會使用 SSMA 會將轉換物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法，以及當它能將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以瀏覽 Oracle 中繼資料總管 窗格中的這個中繼資料，然後檢閱個別的資料庫物件的屬性。  
  
> [!IMPORTANT]  
> 您嘗試連接之前，請確定資料庫伺服器正在執行，且可接受連接。  
  
**若要連接到 Oracle**  
  
1.  在**檔案**功能表上，選取**Connect to Oracle**。  
  
    如果您先前連線到 Oracle，命令名稱將**重新連接到 Oracle**。  
  
2.  在**提供者**方塊中，選取**Oracle 用戶端提供者**或**OLE DB 提供者**，取決於已安裝的提供者。 預設為 Oracle 用戶端。  
  
3.  在**模式**方塊中，選取 **標準模式**， **TNSNAME 模式**，或**連接字串模式**。  
  
    使用指定的伺服器名稱和連接埠的標準模式。 若要手動指定 Oracle 服務名稱中使用服務名稱模式。 使用連接字串模式提供完整連接字串。  
  
4.  如果您選取**標準模式**，提供下列值：  
  
    1.  在**伺服器名稱**方塊中，輸入或選取的名稱或資料庫伺服器的 IP 位址。  
  
    2.  如果資料庫伺服器未設定為接受連接的預設通訊埠 (1521)，請輸入用於在 Oracle 連接的連接埠號碼**伺服器連接埠**方塊。  
  
    3.  在**Oracle SID**方塊中，輸入系統識別項。  
  
    4.  在**使用者名**方塊中，輸入具有必要權限的 Oracle 帳戶。  
  
    5.  在**密碼**方塊中，指定的使用者名稱輸入的密碼。  
  
5.  如果您選取**TNSNAME 模式**，提供下列值：  
  
    1.  在**連接識別碼**方塊中，輸入連接資料庫的識別碼 （TNS 別名）。  
  
    2.  在**使用者名**方塊中，輸入具有必要權限的 Oracle 帳戶。  
  
    3.  在**密碼**方塊中，指定的使用者名稱輸入的密碼。  
  
6.  如果您選取**連接字串模式**，提供連接字串中的**連接字串**方塊。  
  
    下列範例會顯示 OLE DB 連接字串：  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    下列範例示範使用整合式的安全性的 Oracle 用戶端連接字串：  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    如需詳細資訊，請參閱[連接至 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)。  
  
## <a name="reconnecting-to-oracle"></a>重新連接到 Oracle  
資料庫伺服器的連接會保持作用中，直到您關閉專案。 當您重新開啟專案時，您必須重新連接，如果您想要的使用中連接到資料庫。 您可以離線直到您想要更新中繼資料，資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，並將資料移轉。  
  
## <a name="refreshing-oracle-metadata"></a>重新整理 Oracle 中繼資料  
Oracle 資料庫的相關中繼資料不會自動重新整理。 Oracle 中繼資料總管 中的中繼資料是快照集的中繼資料，當您第一次連接時，或您手動重新整理中繼資料的最後一次。 您可以手動更新所有結構描述、 在單一結構描述或個別的資料庫物件的中繼資料。  
  
**若要重新整理中繼資料**  
  
1.  請確定您已連線到資料庫。  
  
2.  在 Oracle 中繼資料總管，選取您想要更新每個結構描述或資料庫物件旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下**結構描述**，個別結構描述或資料庫物件，然後再選取**從資料庫重新整理**。  
  
    如果您沒有作用中連線，將會顯示 SSMA **Connect to Oracle**對話方塊，讓您可以連線。  
  
4.  在重新整理從資料庫 對話方塊，指定要重新整理的物件。  
  
    -   若要重新整理物件，請按一下**Active**物件，直到出現箭號相鄰的欄位。  
  
    -   若要防止進行重新整理的物件，請按一下**Active**相鄰的物件，直到欄位**X**隨即出現。  
  
    -   若要重新整理或拒絕物件目錄，按一下  **Active**類別資料夾旁的欄位。  
  
    若要檢視定義的色彩編碼，請按一下**圖例** 按鈕。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>下一個步驟  
  
-   移轉程序的下一個步驟是[連接到 SQL Server 執行個體](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f)。  
  
## <a name="see-also"></a>另請參閱  
[SQL server 資料庫移轉 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
