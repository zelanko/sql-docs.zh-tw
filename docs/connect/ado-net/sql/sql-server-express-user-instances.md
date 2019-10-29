---
title: SQL Server Express 使用者執行個體
description: 描述 SQL Server Express 使用者實例的支援。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 3b3ac1e395cc1240693ca0dc27324766964e0cfa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452018"
---
# <a name="sql-server-express-user-instances"></a>SQL Server Express 使用者執行個體

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition （SQL Server Express）支援使用者實例功能，只有在使用 Microsoft SqlClient Data Provider 進行 SQL Server 時才可使用。 使用者實例是父實例所產生之 SQL Server Express 資料庫引擎的個別實例。 使用者實例可讓不是本機電腦上系統管理員的使用者連接並連接到 SQL Server Express 資料庫。 每個實例會在個別使用者的安全性內容下執行，以每個使用者為基礎的單一實例。  
  
## <a name="user-instance-capabilities"></a>使用者實例功能  
使用者實例適用于在最低許可權使用者帳戶（LUA）下執行 Windows 的使用者，因為每個使用者都具有在其電腦上執行之實例的 SQL Server 系統管理員（`sysadmin`）許可權，而不需要以 Windows 的身分執行。系統管理員。 在具有有限許可權的使用者實例上執行的軟體，無法進行全系統變更，因為 SQL Server Express 的實例是在使用者的非系統管理員 Windows 帳戶下執行，而不是做為服務。 每個使用者執行個體都會與父執行個體，以及相同電腦上執行的所有其他使用者執行個體隔離。 在使用者實例上執行的資料庫只會以單一使用者模式開啟，而且多個使用者無法連接到在使用者實例上執行的資料庫。 複寫和分散式查詢也會針對使用者實例停用。  
  
如需詳細資訊，請參閱《SQL Server 線上叢書》的＜使用者執行個體＞。  
  
> [!NOTE]
>  使用者如果是他們自己電腦上的系統管理員，或涉及多個資料庫使用者的案例，則不需要使用者實例。  
  
## <a name="enabling-user-instances"></a>啟用使用者實例  
若要產生使用者實例，SQL Server Express 的父實例必須正在執行。 根據預設，在安裝 SQL Server Express 時會啟用使用者執行個體，也可以由系統管理員在父執行個體上執行 **sp_configure** 系統預存程序，而加以明確地啟用或停用。  
  
```sql
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
使用者實例的網路通訊協定必須是本機具名管道。 無法在 SQL Server 的遠端實例上啟動使用者實例，也不允許 SQL Server 登入。  
  
## <a name="connecting-to-a-user-instance"></a>連線到使用者執行個體  
`User Instance` 和 `AttachDBFilename`<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> 關鍵字可以讓 <xref:Microsoft.Data.SqlClient.SqlConnection> 連線至使用者執行個體。 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> `UserInstance` 和 `AttachDBFilename` 屬性也支援使用者實例。  
  
請注意下列有關範例連接字串的資訊，如下所示：  
  
- `Data Source` 關鍵字會參考正在產生使用者實例 SQL Server Express 的父實例。 預設實例為 .\sqlexpress。  
  
- `Integrated Security` 設定為 `true`。 若要連接到使用者實例，則需要 Windows 驗證;不支援 SQL Server 登入。  
  
- `User Instance` 設定為 `true`，它會叫用使用者實例。 (預設為 `false`。)  
  
- `AttachDbFileName` 連接字串關鍵字是用來附加主資料庫檔案（.mdf），其必須包含完整路徑名稱。 `AttachDbFileName` 也會對應至 <xref:Microsoft.Data.SqlClient.SqlConnection> 連接字串內的「擴充屬性」和「初始檔案名」索引鍵。  
  
- 以「管線」符號括住的 `|DataDirectory|` 替代字串會參考開啟連接之應用程式的資料目錄，並提供指出 .mdf 和 .ldf 資料庫和記錄檔位置的相對路徑。 如果您想要在別處尋找這些檔案，您必須提供檔案的完整路徑。  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  您也可以使用 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> 和 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> 屬性，在執行時間建立連接字串。  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>使用&#124;DataDirectory&#124;替代字串  
`DataDirectory` 可與 `AttachDbFileName` 搭配使用以表示資料檔案的相對路徑，開發人員因此能根據資料來源的相對路徑建立連接字串，而不需指定完整路徑。  
  
`DataDirectory` 指向的實體位置取決於應用程式的類型。 在此範例中，要附加的 Northwind .mdf 檔案位於應用程式的 \app_data 資料夾中。  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
當使用 `DataDirectory` 時，在目錄結構中產生的檔案路徑不能高於替代字串所指向的目錄。 例如，如果完全展開的 `DataDirectory` 是 C:\AppDirectory\app_data，則上面顯示的範例連接字串會運作，因為它位於 c:\AppDirectory. 之下 不過，嘗試將 `DataDirectory` 指定為 `|DataDirectory|\..\data`將會導致錯誤，原因為 \data 不是 \AppDirectory 的子目錄。  
  
如果連接字串具有格式不正確的替代字串，則會擲回 <xref:System.ArgumentException>。  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient> 會將替代字串解析為本機電腦檔案系統的完整路徑。 因此，不支援遠端伺服器、HTTP 和 UNC 路徑名稱。 如果伺服器不在本機電腦上，當連接開啟時，就會擲回例外狀況（exception）。  
  
當 <xref:Microsoft.Data.SqlClient.SqlConnection> 開啟時，系統會將它從預設的 SQL Server Express 實例重新導向至執行時間起始的實例，並在呼叫者的帳戶下執行。  
  
> [!NOTE]
>  可能需要增加 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> 值，因為使用者實例可能需要較長的時間來載入，而不是一般實例。  
  
下列程式碼片段會開啟新的 `SqlConnection`、在主控台視窗中顯示連接字串，然後在結束 `using` 程式碼區塊時關閉連接。  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
>  在 SQL Server 內執行的 common language runtime （CLR）程式碼不支援使用者實例。 如果在連接字串中有 `User Instance=true` 的 <xref:Microsoft.Data.SqlClient.SqlConnection> 上呼叫 `Open`，則會擲回 <xref:System.InvalidOperationException>。  
  
## <a name="lifetime-of-a-user-instance-connection"></a>使用者實例連接的存留期  
不同于以服務方式執行的 SQL Server 版本，SQL Server Express 實例不需要手動啟動和停止。 每次使用者登入並連接到使用者實例時，如果使用者實例尚未執行，則會啟動該實例。 使用者實例資料庫已設定 `AutoClose` 選項，因此資料庫會在一段時間沒有活動之後自動關閉。 在上次連接到實例之後，已啟動的 sqlservr.exe 會保持執行狀態一段有限的超時時間，因此，如果在過期時間之前開啟另一個連接，就不需要重新開機該進程。 如果在該超時期限過期之前未開啟任何新的連線，使用者實例會自動關閉。 父執行個體的系統管理員可以使用 **sp_configure** 來變更 **user instance timeout** 選項，藉此設定使用者執行個體的逾時期限持續期間。 預設值是 60 分鐘。  
  
> [!NOTE]
>  如果在連接字串中使用 `Min Pool Size`，且其值大於零，則連接共用器一律會維護幾個開啟的連接，而且使用者實例不會自動關閉。  
  
## <a name="how-user-instances-work"></a>使用者實例的工作方式  
初次針對每個使用者產生使用者執行個體時，會將 **master** 和 **msdb** 系統資料庫從 Template Data 資料夾複製到使用者的本機應用程式資料存放庫目錄下方專供使用者執行個體使用的路徑。 這個路徑通常是 `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`。 當使用者執行個體啟動時，**tempdb**、記錄檔，以及追蹤檔案也會寫入至這個目錄。 為實例產生的名稱，保證對每個使用者而言是唯一的。  
  
根據預設，Windows Builtin\Users 群組的所有成員都會被授與在本機實例上連接的許可權，以及 SQL Server 二進位檔的讀取和執行許可權。 一旦驗證主控使用者實例的呼叫使用者的認證，該使用者就會變成該實例上的 `sysadmin`。 只有共用記憶體會針對使用者實例啟用，這表示只有本機電腦上的作業可以進行。  
  
使用者必須被授與連接字串中所指定之 .mdf 和 .ldf 檔案的讀取和寫入權限。  
  
> [!NOTE]
>  .Mdf 和 .ldf 檔案分別代表資料庫和記錄檔。 這兩個檔案是相符的集合，因此在備份和還原作業期間必須小心。 資料庫檔案包含記錄檔確切版本的相關資訊，如果資料庫與錯誤的記錄檔結合，就不會開啟。  
  
為避免資料損毀，使用者實例中的資料庫會以獨佔存取權開啟。 如果兩個不同的使用者實例在同一部電腦上共用相同的資料庫，第一個實例上的使用者必須先關閉資料庫，然後才能在第二個實例中開啟。  
  
## <a name="user-instance-scenarios"></a>使用者實例案例  
使用者實例為資料庫應用程式開發人員提供的 SQL Server 資料存放區，不會相依于其開發電腦上具有系統管理帳戶的開發人員。 使用者實例是以 Access/Jet 模型為基礎，其中資料庫應用程式只會連接到檔案，而使用者則會自動擁有所有資料庫物件的完整許可權，而不需要系統管理員介入來授與無權. 在使用者以最低許可權使用者帳戶（LUA）執行，而且沒有伺服器或本機電腦的系統管理許可權，而且還需要建立資料庫物件和應用程式的情況下，它才適用。 使用者實例可讓使用者在執行時間建立實例，在使用者自己的安全性內容下執行，而不是在更具特殊許可權系統服務的安全性內容中執行。  
  
> [!IMPORTANT]
>  使用者實例僅適用于所有使用它的應用程式都完全受信任的案例。  
  
使用者實例的案例包括：  
  
- 不需要共用資料的任何單一使用者應用程式。  
  
- ClickOnce 部署。 如果目標電腦上已安裝 .NET Framework 2.0 (或更新版本) 或 .NET Core 1.0 (或更新版本) 和 SQL Server Express，則非系統管理員的使用者也可以安裝及使用因採取 ClickOnce 動作而下載的安裝套件。 請注意，如果這是安裝程式的一部分，系統管理員必須安裝 SQL Server Express。 如需詳細資訊，請參閱[ClickOnce Deployment for Windows Forms](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms)。
  
- 使用 Windows 驗證的專用 ASP.NET 裝載。 單一 SQL Server Express 實例可以裝載在內部網路上。 應用程式會使用 ASPNET Windows 帳戶進行連接，而不是使用模擬。 使用者實例不應用於協力廠商或共用的裝載案例，其中所有應用程式會共用相同的使用者實例，而且不會再維持彼此隔離。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
