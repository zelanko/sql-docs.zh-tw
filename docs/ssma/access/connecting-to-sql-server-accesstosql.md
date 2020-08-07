---
title: 連接到 SQL Server (AccessToSQL) |Microsoft Docs
description: 瞭解如何連接到 SQL Database 的目標實例，以遷移 Access 資料庫。 SSMA 會取得 SQL Database 中資料庫的相關中繼資料。
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 612921c1640b97135c96a5f81c3099722bf5bb4c
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939110"
---
# <a name="connecting-to-sql-server-accesstosql"></a>連接到 SQL Server (AccessToSQL) 
若要將 Access 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您必須連接到的目標實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 當您連接時，SSMA 會取得實例中資料庫的相關中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並在 [中繼資料] Explorer 中顯示資料庫中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 SSMA 會儲存您所連接之實例的相關資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，但不會儲存密碼。  
  
您的 SQL Server 連接會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時，如果您想要使用伺服器的作用中連接，就必須重新連接到 SQL Server。 在您將資料庫物件載入 SQL Server 並遷移資料之前，您可以離線工作。  
  
有關 SQL Server 實例的中繼資料不會自動同步處理。 相反地，若要更新 SQL Server 中繼資料 Explorer 中的中繼資料，您必須手動更新 SQL Server 中繼資料。 如需詳細資訊，請參閱本主題稍後的「同步處理 SQL Server 中繼資料」一節。  
  
## <a name="required-sql-server-permissions"></a>必要的 SQL Server 許可權  
用來連接到的帳戶 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要不同的許可權，視該帳戶所執行的動作而定。  
  
-   若要將 Access 物件轉換成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法、重新整理中的中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，或將已轉換的語法儲存至腳本，該帳戶必須具有登入實例的許可權 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   若要將資料庫物件載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，最低許可權需求是目標資料庫中**db_owner**資料庫角色的成員資格。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 連接  
將 Access 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語法之前，您必須先建立要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 遷移 access 資料庫之實例的連接。  
  
當您定義連接屬性時，也會指定要遷移物件和資料的資料庫。 連接到之後，您可以在 Access 資料庫層級自訂這個對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)。  
  
> [!IMPORTANT]  
> 在連接到之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請確定的實例正在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而且可以接受連接。 如需詳細資訊，請參閱《線上叢書》中的「連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫引擎」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
**若要連接到 SQL Server**  
  
1.  在 [檔案]**功能表上**，選取 **[連線至 SQL Server]**。  
  
    如果您先前已連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，命令名稱會**重新連接到 SQL Server**。  
  
2.  在 [**伺服器名稱**] 方塊中，輸入或選取實例的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
    -   如果您要連接到本機電腦上的預設實例，您可以輸入**localhost**或點 (**.**) 。  
  
    -   如果您要連接到另一部電腦上的預設實例，請輸入電腦的名稱。  
  
    -   如果您要連接到已命名的實例，請輸入電腦名稱稱、反斜線和實例名稱。 例如： MyServer\MyInstance。  
  
    -   若要連接到的使用中使用者實例 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] ，請使用具名管道通訊協定來連接，並指定管道名稱，例如 \\ \\ .\pipe\sql\query。 如需詳細資訊，請參閱 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 文件。  
  
3.  如果您的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為接受非預設通訊埠上的連接，請 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [**伺服器埠**] 方塊中輸入用於連接的通訊埠編號。 預設實例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設埠號碼為1433。 若為已命名的實例，SSMA 將會嘗試從 Browser 服務取得埠號碼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
4.  在 [**資料庫**] 方塊中，輸入物件和資料移轉的目標資料庫名稱。  
  
    重新連接到時，無法使用此選項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
    目標資料庫名稱不能包含空格或特殊字元。 例如，您可以將 Access 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名為 "abc" 的資料庫。 但是，您無法將 Access 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名為 "a b-c" 的資料庫。  
  
    連接之後，您可以為每個資料庫自訂此對應。 如需詳細資訊，請參閱[對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)  
  
5.  在 [**驗證**] 下拉式功能表中，選取要用於連接的驗證類型。 若要使用目前的 Windows 帳戶，請選取 [ **Windows 驗證**]。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，請選取 [ **SQL Server Authentication**]，然後提供 [使用者名稱] 和 [密碼]。  
  
6.  針對安全連線，會新增兩個控制項，[**加密連接**] 核取方塊和 [ **TrustServerCertificate** ] 核取方塊。 只有當 [**加密連接**] 核取方塊已核取時，才會顯示**TrustServerCertificate**核取方塊。 若已核取 [**加密**連線] (true) 而且未選取 [ **TrustServerCertificate** ] (false) ，將會驗證 SQL Server SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 若要確保這一點，憑證必須安裝在用戶端以及伺服器端。  
  
7.  按一下 [ **連接**]。  
  
**版本相容性較高**  
  
它可以連接/重新連接至較高版本的 SQL Server。  
  
1.  當建立的專案 SQL Server 2005 時，您將能夠連接到 SQL Server 2008 或 SQL Server 2012。  
  
2.  當建立的專案為 SQL Server 2008，但不允許連接到較低版本（也就是 SQL Server 2005）時，您將能夠連接到 SQL Server 2012。  
  
3.  當建立的專案為 SQL Server 2012 時，您才能夠連接到 SQL Server 2012。  
  
4.  較高版本的相容性對 SQL Azure 而言無效。  
  
|專案類型與目標伺服器版本的比較|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 (版本： 9. x) |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 (版本： 10. x) |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 (版本： 11. x) |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 (版本： 12. x) |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 (版本： 13. x) |SQL Azure|  
|-|-|-|-|-|-|-|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||是||
|SQL Azure||||||是|
  
> [!IMPORTANT]  
> 資料庫物件的轉換是根據專案類型執行，而不是根據連接的 SQL Server 版本。 在 SQL Server 2005 專案的情況下，即使您已連接到更高版本的 SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016) ，還是會根據 SQL Server 2005 來執行轉換。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步處理 SQL Server 中繼資料  
如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 架構在您連接之後變更，您可以同步處理中繼資料與伺服器。  
  
**同步處理 SQL Server 中繼資料**  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料 Explorer 中，以滑鼠右鍵按一下 [**資料庫**]，然後選取 [**與資料庫同步處理**]。  
  
## <a name="reconnecting-to-sql-server"></a>重新連接到 SQL Server  
您的連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保持作用中狀態，直到您關閉專案為止。 當您重新開啟專案時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果您想要使用伺服器的作用中連接，就必須重新連接到。 在您將資料庫物件載入並遷移資料之前，您可以離線工作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
重新連接到的程式與建立連線的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 過程相同。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要自訂來源與目標資料庫之間的對應，請參閱[對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)。否則，下一個步驟是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用[convert 資料庫物件](converting-access-database-objects-accesstosql.md)，將資料庫物件轉換成語法  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
