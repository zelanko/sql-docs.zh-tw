---
title: 連接至 SQL Server (AccessToSQL) |Microsoft Docs
description: 瞭解如何連接到 SQL Database 的目標實例，以遷移 Access 資料庫。 SSMA 會取得 SQL Database 中資料庫的相關中繼資料。
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
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
ms.openlocfilehash: 1bd54d3fdf90447dbbf8b35a96c6b454ca6c4e56
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869538"
---
# <a name="connecting-to-sql-server-accesstosql"></a>連接至 SQL Server (AccessToSQL) 

若要將 Access 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您必須連接到的目標實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 當您連接時，SSMA 會取得實例中資料庫的相關中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並在 **SQL Server 中繼資料瀏覽器** 中顯示資料庫中繼資料。 SSMA 會儲存您所連接之實例的相關資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，但不會儲存密碼。

您的連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保持作用中，直到您關閉專案為止。 當您重新開啟專案時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果您想要使用中的伺服器連接，則必須重新連接到。 您可以離線工作，直到您將資料庫物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並遷移資料為止。

有關實例的中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會自動同步處理。 相反地，若要更新 SQL Server 中繼資料瀏覽器中的中繼資料，您必須手動更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料。 如需詳細資訊，請參閱本主題稍後的「同步處理 SQL Server 中繼資料」一節。

## <a name="required-sql-server-permissions"></a>必要的 SQL Server 許可權

用來連接的帳戶 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要不同的許可權，視帳戶執行的動作而定：

- 若要將 Access 物件轉換成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法、從更新中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，或將轉換的語法儲存至腳本，此帳戶必須具有登入實例的許可權 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

- 若要將資料庫物件載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，帳戶必須是 **db_ddladmin** 資料庫角色的成員。

- 若要將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，帳戶必須是 **db_owner** 資料庫角色的成員。

## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 連接

將 Access 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語法之前，您必須建立與實例的連接，以便將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] access 資料庫移轉至其中。

當您定義連接屬性時，您也會指定要遷移物件和資料的資料庫。 連接至之後，您可以在 Access 資料庫層級自訂此對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱 [對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)。

> [!IMPORTANT]
> 連接至之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請確定的實例正在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而且可以接受連接。

連線至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]：

1. **在 [檔案**] 功能表上，選取 **[連接到 SQL Server]**。
   如果您先前已連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，命令名稱將會 **重新連接到 SQL Server**。

2. 在 [ **伺服器名稱** ] 方塊中，輸入或選取實例的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
   - 如果您要連接到本機電腦上的預設實例，可以輸入 `localhost` 或 () 的點 `.` 。
   - 如果您要連接至另一部電腦上的預設實例，請輸入電腦的名稱。
   - 如果您要連接到已命名的實例，請輸入電腦名稱稱、反斜線和實例名稱。 例如： `MyServer\MyInstance` 。
   - 若要連接到的使用中使用者實例 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] ，請使用具名管道通訊協定來連接，然後指定管道名稱，例如 `\\.\pipe\sql\query` 。 如需詳細資訊，請參閱 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 文件。

3. 如果您的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為接受非預設通訊埠上的連接，請 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [ **伺服器埠** ] 方塊中輸入用於連接的埠號碼。 若是的預設實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，預設的埠號碼為1433。 若為已命名的實例，SSMA 會嘗試從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器服務取得埠號碼。

4. 在 [ **資料庫** ] 方塊中，輸入物件和資料移轉的目標資料庫名稱。
   當您重新連接至時，無法使用此選項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
   目標資料庫名稱不能包含空格或特殊字元。 例如，您可以將 Access 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名為的資料庫 `abc` 。 但是，您無法將 Access 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名為的資料庫 `a b-c` 。
   連接之後，您可以為每個資料庫自訂此對應。 如需詳細資訊，請參閱 [對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)

5. 在 [ **驗證** ] 下拉式功能表中，選取要用於連接的驗證類型。 若要使用目前的 Windows 帳戶，請選取 [ **Windows 驗證**]。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，請選取 [ **SQL Server Authentication**]，然後提供使用者名稱和密碼。

6. 若為安全連線，則會新增兩個控制項，[ **加密連接** ] 核取方塊和 [ **TrustServerCertificate** ] 核取方塊。 只有當 [ **加密** 連線] 核取方塊已核取時，才會顯示 **TrustServerCertificate** 核取方塊。 核取 [ **加密連接** ] (true) 並取消核取 [ **TrustServerCertificate** ] (false) ，將會驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 憑證。 驗證伺服器憑證是 SSL 交握的一部分，而且這麼做可以確保伺服器是所要連接的正確伺服器。 為了確保這一點，憑證必須安裝在用戶端上，也必須安裝在伺服器端。

7. 按一下 [ **連接**]。

> [!IMPORTANT]
> 雖然您可以連接到較高的版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，相較于建立遷移專案時所選擇的版本，資料庫物件的轉換取決於目標版本的專案，而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您連接的版本。

## <a name="synchronizing-sql-server-metadata"></a>同步處理 SQL Server 中繼資料

如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 架構在您連接之後變更，您可以同步處理中繼資料與伺服器。

若要同步處理 SQL Server 中繼資料，請 **SQL Server Metadata Explorer**，以滑鼠右鍵按一下 [ **資料庫**]，然後選取 [ **與資料庫同步**]。

## <a name="reconnecting-to-sql-server"></a>重新連接到 SQL Server

您的連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保持作用中，直到您關閉專案為止。 當您重新開啟專案時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果您想要使用中的伺服器連接，則必須重新連接到。 您可以離線工作，直到您將資料庫物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並遷移資料為止。

重新連接的程式與建立連線的程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相同。

## <a name="next-steps"></a>後續步驟

如果您想要自訂來源與目標資料庫之間的對應，請參閱 [對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md) ; 否則，下一步是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [轉換資料庫物件](converting-access-database-objects-accesstosql.md)將資料庫物件轉換成語法。

## <a name="see-also"></a>另請參閱

[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)
