---
title: 複寫管理物件概念 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- replication [SQL Server], RMO
- programming interfaces [SQL Server replication]
- replication [SQL Server], how-to topics
- RMO [SQL Server]
- Replication Management Objects
- programming [SQL Server replication], RMO
ms.assetid: 37476d50-fb47-49e3-9504-3b163ac381d8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2cbc3571aa26728fa94957bb0c2f207ff769f4c4
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129568"
---
# <a name="replication-management-objects-concepts"></a>Replication Management Objects Concepts
  Replication Management Objects (RMO) 是一種 Managed 程式碼組件，用以封裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的複寫功能。 RMO 是由 <xref:Microsoft.SqlServer.Replication> 命名空間實作。  
  
 下列章節中的主題將說明如何使用 RMO 屬性，以程式設計方式控制複寫工作。  
  
 [設定散發](../configure-distribution.md)  
 本節中的主題示範如何使用 RMO 來設定發行與散發。  
  
 [Create a Publication](../publish/create-a-publication.md)  
 本章節中的主題示範如何使用 RMO 來建立、刪除和修改發行集與發行項。  
  
 [訂閱發行集](../subscribe-to-publications.md)  
 本章節中的主題示範如何使用 RMO 來建立、刪除和修改訂閱。  
  
 [保護複寫拓撲](../security/view-and-modify-replication-security-settings.md)  
 本章節中的主題示範如何使用 RMO 來檢視和修改安全性設定。  
  
 [同步處理訂閱 &#40;複寫&#41;](../synchronize-data.md)  
 本章節中的主題示範如何同步處理訂閱。  
  
 [監視複寫](../monitoring-replication.md)  
 本章節中的主題示範如何以程式設計方式監視複寫拓撲。  
  
## <a name="introduction-to-rmo-programming"></a>RMO 程式設計簡介  
 RMO 是針對程式設計 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫的所有層面所設計。 RMO 命名空間是 <xref:Microsoft.SqlServer.Replication>，而且它是 Microsoft.SqlServer.Rmo.dll 所實作，這個檔案是 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 組件。 同時也屬於 <xref:Microsoft.SqlServer.Replication> 命名空間的 Microsoft.SqlServer.Replication.dll 組件，會實作 Managed 程式碼介面，以設計各種複寫代理程式的程式 (快照集代理程式、散發代理程式以及合併代理程式)。 可從 RMO 存取其類別以同步處理訂閱。 在由 Microsoft.SqlServer.Replication.BusinessLogicSupport.dll 組件所實作的 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 命名空間中的類別，是用以為合併式複寫建立自訂商務邏輯。 這個組件與 RMO 無關。  
  
## <a name="deploying-applications-based-on-rmo"></a>根據 RMO 部署應用程式  
 RMO 相依於隨附在所有版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (但 SQL Server Compact 除外) 中之複寫元件與用戶端連線元件。 若要根據 RMO 部署應用程式，您必須在應用程式將執行的電腦上，安裝含有複寫元件與用戶端連線元件的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本。  
  
## <a name="getting-started-with-rmo"></a>RMO 使用者入門  
 本章節描述如何使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 啟動簡單的 RMO 專案。  
  
#### <a name="to-create-a-new-microsoft-visual-c-project"></a>若要建立新的 Microsoft Visual C# 專案  
  
1.  啟動 Visual Studio。  
  
2.  在 [檔案] 功能表上，按一下 [新增專案]。 [新增專案]  對話方塊隨即出現。  
  
3.  在 [專案類型] 對話方塊中，選取 [Visual C# 專案]。 在 [範本] 窗格中，選取 [Windows 應用程式]。  
  
4.  (選擇性) 在 [名稱] 中，鍵入新應用程式的名稱。  
  
5.  按一下 [確定]，載入 Visual C# Windows 範本。  
  
6.  在 [專案] 功能表上，選取 [新增參考] 項目。 [新增參考] 對話方塊隨即出現。  
  
7.  從 [.NET] 索引標籤的清單中選取下列組件，然後按一下 [確定]。  
  
    -   Microsoft.SqlServer.Replication .NET 程式設計介面  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   複寫代理程式程式庫  
  
    > [!NOTE]  
    >  使用 CTRL 鍵以選取一個以上的檔案。  
  
8.  (選擇性) 重複步驟 6。 按一下 [瀏覽] 索引標籤，導覽至 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM，選取 Microsoft.SqlServer.Replication.BusinessLogicSupport.dll，然後按一下 [確定]。  
  
9. 在 [檢視] 功能表中，按一下 [程式碼]。  
  
10. 在程式碼中的命名空間陳述式前面，輸入下列 `using` 陳述式來限定 RMO 命名空間中的類型：  
  
    ```  
    // These namespaces are required.  
    using Microsoft.SqlServer.Replication;  
    using Microsoft.SqlServer.Management.Common;  
    // This namespace is only used when creating custom business  
    // logic for merge replication.  
    using Microsoft.SqlServer.Replication.BusinessLogicSupport;   
    ```  
  
#### <a name="to-create-a-new-microsoft-visual-basic-net-project"></a>建立新的 Microsoft Visual Basic .NET 專案  
  
1.  啟動 Visual Studio。  
  
2.  在 [檔案] 功能表上，選取 [新增專案]。 [新增專案]  對話方塊隨即出現。  
  
3.  在 [專案類型] 窗格中，選取 [Visual Basic]。 在 [範本] 窗格中，選取 [Windows 應用程式]。  
  
4.  (選擇性) 在 [名稱] 方塊中，鍵入新應用程式的名稱。  
  
5.  按一下 [確定]，載入 Visual Basic Windows 範本。  
  
6.  在 [專案] 功能表上，選取 [新增參考]。 [新增參考] 對話方塊隨即出現。  
  
7.  從 [.NET] 索引標籤的清單中選取下列組件，然後按一下 [確定]。  
  
    -   Microsoft.SqlServer.Replication .NET 程式設計介面  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   複寫代理程式程式庫  
  
    > [!NOTE]  
    >  使用 CTRL 鍵以選取一個以上的檔案。  
  
8.  (選擇性) 重複步驟 6。 按一下 [瀏覽] 索引標籤，導覽至 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM，選取 Microsoft.SqlServer.Replication.BusinessLogicSupport.dll，然後按一下 [確定]。  
  
9. 在 [檢視] 功能表中，按一下 [程式碼]。  
  
10. 在程式碼的任何宣告前面，輸入下列 `Imports` 陳述式，以限定 RMO 命名空間中的類型。  
  
    ```  
    ' These namespaces are required.  
    Imports Microsoft.SqlServer.Replication  
    Imports Microsoft.SqlServer.Management.Common  
    ' This namespace is only used when creating custom business  
    ' logic for merge replication.  
    Imports Microsoft.SqlServer.Replication.BusinessLogicSupport   
    ```  
  
## <a name="connecting-to-a-replication-server"></a>連接至複寫伺服器  
 RMO 程式設計物件需要使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別的執行個體，來建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的連接。 這個伺服器連接會獨立於任何 RMO 程式設計物件之外建立。 接著會在執行個體建立期間將它傳遞到 RMO 物件，或是將它指派到物件的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。 以此方式，就可以個別建立和管理 RMO 程式設計物件與連接物件執行個體，而且多個 RMO 程式設計物件可以重複使用單一連接物件。 下列規則適用於應用程式伺服器的連接：  
  
-   連接的所有屬性是針對指定的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件所定義。  
  
-   每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的連接都必須有它自己的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
-   會將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件指派到要在伺服器上建立或存取的 RMO 程式設計物件之 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
-   <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> 方法會開啟伺服器的連接。 必須先呼叫這個方法，才能呼叫在使用此連接的任何 RMO 程式設計物件上存取伺服器之任何方法。  
  
-   因為 RMO 與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 都使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，所以 RMO 與 SMO 物件都可以使用相同的連接。 如需詳細資訊，請參閱[連線到 SQL Server 的執行個體](../../server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)。  
  
-   在 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件中，會提供所有建立連接及成功登入伺服器的驗證資訊。  
  
-   Windows 驗證是預設值。 若要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證，必須將 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> 設定為 `false` 與 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A>，而且 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> 必須設定為有效的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入與密碼。 安全性認證必須以安全方式儲存和處理，而且每當有需要時必須在執行階段提供。  
  
-   對於多執行緒應用程式，應該在每個執行緒中使用個別的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
 在 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> 物件上呼叫 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 方法，以關閉 RMO 物件所使用的使用中伺服器連接。  
  
## <a name="setting-rmo-properties"></a>設定 RMO 屬性  
 RMO 程式設計物件的屬性代表在伺服器這些複寫物件的屬性。 在伺服器建立新複寫物件時，會使用 RMO 屬性來定義這些物件。 對於現有的物件，RMO 屬性代表現有物件的屬性，只能修改可寫入或是可設定的屬性。 屬性可以在新物件或是現有物件上設定。  
  
### <a name="setting-properties-for-new-replication-objects"></a>設定新複寫物件的屬性  
 在伺服器建立新複寫物件時，您必須先指定所有必要的屬性，才能呼叫物件的 `Create` 方法。 如需為新複寫物件設定屬性的詳細資訊，請參閱[設定發行和散發](../configure-publishing-and-distribution.md)。  
  
### <a name="setting-properties-for-existing-replication-objects"></a>設定現有複寫物件的屬性  
 對於存在於伺服器上的複寫物件，視物件而定，RMO 可能支援變更某些或是所有其屬性的能力。 只可以變更可寫入的或可設定的屬性。 在變更屬性之前，必須先呼叫 `Load` 或 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法，從伺服器取得目前的屬性。 呼叫這些方法表示要修改現有的物件。  
  
 依預設，當變更物件屬性時，RMO 會根據要使用的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 之執行模式，將這些變更認可到伺服器。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 方法可用以在嘗試擷取或是變更其屬性之前，先驗證存在於伺服器的物件。 如需變更複寫物件屬性的詳細資訊，請參閱[檢視及修改散發者和發行者屬性](../view-and-modify-distributor-and-publisher-properties.md)。  
  
> [!NOTE]  
>  當有多個 RMO 用戶端或是多個 RMO 程式設計物件的執行個體，在伺服器上存取相同複寫物件時，可以呼叫 RMO 物件的 `Refresh` 方法，以便根據伺服器上物件目前的狀態來更新屬性。  
  
### <a name="caching-property-changes"></a>快取屬性變更  
 當將 <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 屬性設定為 <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes.CaptureSql> 時，會擷取 RMO 產生的所有 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，這樣就可以使用其中一個執行方法，以單一批次手動執行它們。 RMO 可讓您使用物件的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法，以擷取屬性變更並在單一批次中一起認可它們。 若要快取屬性變更，必須將物件的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 屬性設定為 `true`。 在快取 RMO 中的屬性變更時，<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件仍然會控制何時將變更傳送到伺服器。 如需快取複寫物件之屬性變更的詳細資訊，請參閱[檢視及修改散發者和發行者屬性](../view-and-modify-distributor-and-publisher-properties.md)。  
  
> [!IMPORTANT]  
>  雖然 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別支援在設定屬性時宣告明確的交易，不過，這樣的交易可能會平擾內部複寫交易、可能會產生非預期的結果，而且不應該與 RMO 搭配使用。  
  
## <a name="example"></a>範例  
 這個範例會示範屬性變更的快取。 會快取對於交易式發行集屬性所做的變更，直到將它們明確地傳送到伺服器為止。  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_ChangeTranPub_cached)]  
  
## <a name="see-also"></a>另請參閱  
 [Replication System Stored Procedures Concepts](replication-system-stored-procedures-concepts.md)   
 [複寫程式設計概念](replication-programming-concepts.md)  
  
  
