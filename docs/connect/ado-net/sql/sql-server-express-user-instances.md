---
title: SQL Server Express 使用者執行個體
description: 描述對 SQL Server Express 使用者執行個體的支援。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 91b00848fb42c64f1c180019a7618bf649488bd9
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896247"
---
# <a name="sql-server-express-user-instances"></a>SQL Server Express 使用者執行個體

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Microsoft SQL Server Express Edition (SQL Server Express) 支援只有在使用 Microsoft SqlClient Data Provider for SQL Server 時才提供的使用者執行個體功能。 使用者執行個體是 SQL Server Express 資料庫引擎的個別執行個體，這是由 SQL Server Express 的父執行個體所產生的。 使用者執行個體可讓不是本機電腦上系統管理員的使用者附加及連線到 SQL Server Express 資料庫。 每個執行個體都會在個別使用者的資訊安全內容下，以每個使用者一個執行個體為基礎的方式執行。  
  
## <a name="user-instance-capabilities"></a>使用者執行個體功能  
使用者執行個體對於在最低權限使用者帳戶 (LUA) 下執行 Windows 的使用者來說非常有用，因為每個使用者都具有其電腦上執行中執行個體的 SQL Server 系統管理員 (`sysadmin`) 權限，而不需要同時以 Windows 系統管理員身分執行。 在具備有限權限的使用者執行個體上執行的軟體，無法進行全系統變更，因為 SQL Server Express 的執行個體是在使用者的非系統管理員 Windows 帳戶下執行，而非以服務方式執行。 每個使用者執行個體都會與父執行個體，以及相同電腦上執行的所有其他使用者執行個體隔離。 在使用者執行個體上執行的資料庫只會以單一使用者模式開啟，而且無法讓多個使用者連線到在使用者執行個體上執行的資料庫。 複寫與分散式查詢也會針對使用者執行個體停用。  
  
如需詳細資訊，請參閱《SQL Server 線上叢書》的＜使用者執行個體＞。  
  
> [!NOTE]
>  使用者如果已經是其自有電腦上的系統管理員，或屬於涉及多個資料庫使用者的情況，則不需要使用者執行個體。  
  
## <a name="enabling-user-instances"></a>啟用使用者執行個體  
若要產生使用者執行個體，SQL Server Express 的父執行個體必須在執行中。 根據預設，在安裝 SQL Server Express 時會啟用使用者執行個體，也可以由系統管理員在父執行個體上執行 **sp_configure** 系統預存程序，而加以明確地啟用或停用。  
  
```sql
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
使用者執行個體的網路通訊協定必須是本機具名管道。 使用者執行個體無法在 SQL Server 的遠端執行個體上啟動，也不允許 SQL Server 登入。  
  
## <a name="connecting-to-a-user-instance"></a>連線到使用者執行個體  
`User Instance` 和 `AttachDBFilename`<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> 關鍵字可以讓 <xref:Microsoft.Data.SqlClient.SqlConnection> 連線至使用者執行個體。 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>`UserInstance` 與 `AttachDBFilename` 屬性也支援使用者執行個體。  
  
請注意下列與範例連接字串有關的資訊，如下所示：  
  
- `Data Source` 關鍵字會參考正在產生使用者執行個體之 SQL Server Express 的父執行個體。 預設的執行個體為 .\sqlexpress。  
  
- `Integrated Security` 設定為 `true`。 若要連線到使用者執行個體，需要 Windows 驗證；不支援 SQL Server 登入。  
  
- `User Instance` 設定為 `true`，這會叫用使用者執行個體。 (預設為 `false`。)  
  
- `AttachDbFileName` 連接字串關鍵字是用來附加主資料庫檔案 (.mdf)，這必須包含完整路徑名稱。 `AttachDbFileName` 也對應到 <xref:Microsoft.Data.SqlClient.SqlConnection> 連接字串內的「擴充屬性」與「初始檔案名稱」機碼相對應。  
  
- 管線符號中括住的 `|DataDirectory|` 替代字串會參考開啟連線之應用程式的資料目錄，並提供指出 .mdf 與 .ldf 資料庫與記錄檔位置的相對路徑。 如果您想要在其他位置尋找這些檔案，必須提供檔案的完整路徑。  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  您也可以使用 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder><xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> 與 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> 屬性，在執行階段建立連接字串。  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>使用 &#124;DataDirectory&#124; 替代字串  
`DataDirectory` 可與 `AttachDbFileName` 搭配使用以表示資料檔案的相對路徑，開發人員因此能根據資料來源的相對路徑建立連接字串，而不需指定完整路徑。  
  
`DataDirectory` 所指向的實體位置取決於應用程式的類型。 在此範例中，要附加的 Northwind.mdf 檔案位於應用程式的 \app_data 資料夾中。  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
使用 `DataDirectory` 時，在目錄結構中產生的檔案路徑不能高於替代字串所指向的目錄。 例如，如果完全展開的 `DataDirectory` 是 C:\AppDirectory\ app_data，上面顯示的範例連接字串可以運作，因為該字串位於 c:\AppDirectory 之下。 不過，嘗試將 `DataDirectory` 指定為 `|DataDirectory|\..\data`將會導致錯誤，原因為 \data 不是 \AppDirectory 的子目錄。  
  
如果連接字串具有格式不正確的替代字串，將會擲回 <xref:System.ArgumentException>。  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient> 會將替代字串解析為本機電腦檔案系統的完整路徑。 因此，不支援遠端伺服器、HTTP 與 UNC 路徑名稱。 如果伺服器不在本機電腦上，當連線開啟時，就會擲回例外狀況。  
  
當 <xref:Microsoft.Data.SqlClient.SqlConnection> 開啟時，系統會將該連線從預設 SQL Server Express 執行個體重新導向至以呼叫者的帳戶執行的執行個體所起始的執行階段。  
  
> [!NOTE]
>  可能需要增加 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> 值，因為使用者執行個體可能需要比一般執行個體更長的時間來載入。  
  
下列程式碼片段會開啟新的 `SqlConnection`、在主控台視窗中顯示連接字串，然後在結束 `using` 程式碼區塊時關閉連線。  
  
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
>  在 SQL Server 內部執行的通用語言執行平台 (CLR) 程式碼不支援使用者執行個體。 如果在連接字串中有 `User Instance=true` 的 <xref:Microsoft.Data.SqlClient.SqlConnection> 上呼叫 `Open`，會擲回 <xref:System.InvalidOperationException>。  
  
## <a name="lifetime-of-a-user-instance-connection"></a>使用者執行個體連線的存留期  
不同於以服務方式執行的 SQL Server 版本，SQL Server Express 執行個體不需要手動啟動及停止。 每次使用者登入並連線到使用者執行個體時，如果使用者執行個體尚未執行，就會啟動該執行個體。 使用者執行個體資料庫已設定 `AutoClose` 選項，因此資料庫會在一段時間沒有活動之後自動關閉。 在執行個體的最後一個連線關閉之後，已啟動的 sqlservr.exe 程序會繼續執行一段有限的逾時期間，因此，如果在逾時到期之前開啟另一個連線，就不需要重新啟動該處理序。 如果在該逾時期間到期之前未開啟任何新的連線，使用者執行個體會自動關閉。 父執行個體的系統管理員可以使用 **sp_configure** 來變更 **user instance timeout** 選項，藉此設定使用者執行個體的逾時期限持續期間。 預設值是 60 分鐘。  
  
> [!NOTE]
>  如果在連接字串中使用 `Min Pool Size`，且其值大於零，連接共用器一律會維護幾個已開啟的連線，而且使用者執行個體不會自動關閉。  
  
## <a name="how-user-instances-work"></a>使用者執行個體的運作方式  
初次針對每個使用者產生使用者執行個體時，會將 **master** 和 **msdb** 系統資料庫從 Template Data 資料夾複製到使用者的本機應用程式資料存放庫目錄下方專供使用者執行個體使用的路徑。 此路徑通常是 `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`。 當使用者執行個體啟動時，**tempdb**、記錄檔，以及追蹤檔案也會寫入至這個目錄。 為執行個體產生的名稱保證對每個使用者來說都是唯一的。  
  
根據預設，Windows Builtin\Users 群組的所有成員都會被授與在本機執行個體上連線的權限，以及在 SQL Server 二進位檔案上讀取及執行權限。 只要呼叫裝載使用者執行個體之使用者的認證通過驗證，該使用者就會成為該執行個體上的 `sysadmin`。 只有共用記憶體會針對使用者執行個體啟用，這表示只有本機電腦上的作業可以執行。  
  
使用者必須獲授與連接字串中所指定之 .mdf 與 .ldf 檔案的讀取及寫入權限。  
  
> [!NOTE]
>  .mdf 與 .ldf 檔案分別代表資料庫與記錄檔。 這兩個檔案是相符的集合，因此在備份及還原作業執行期間必須謹慎小心。 資料庫檔案包含記錄檔確切版本的相關資訊，因此如果資料庫與錯誤的記錄檔結合，該資料庫將無法開啟。  
  
為避免資料損毀，使用者執行個體中的資料庫會以獨佔存取權方式開啟。 如果兩個不同的使用者執行個體共用相同電腦上的相同資料庫，第一個執行個體上的使用者必須先關閉資料庫，然後才能在第二個執行個體中開啟。  
  
## <a name="user-instance-scenarios"></a>使用者執行個體案例  
使用者執行個體會向資料庫應用程式開發人員提供 SQL Server 資料存放區，且該存放區不會要求開發人員必須有其開發電腦上的系統管理帳戶。 使用者執行個體是以 Access/Jet 模型為基礎，其中資料庫應用程式只會連線到檔案，而使用者會自動擁有所有資料庫物件的完整權限，而不需要系統管理員介入以授與權限。 在使用者以最低權限使用者帳戶 (LUA) 執行、沒有伺服器或本機電腦的系統管理權限，而且還需要建立資料庫物件與應用程式的情況下，才適用這個情況。 使用者執行個體可讓使用者在執行階段建立執行個體，並在使用者自己的資訊安全內容下執行，而不是在具備更特殊權限之系統服務的資訊安全內容中執行。  
  
> [!IMPORTANT]
>  使用者執行個體應只在所有使用該執行個體的應用程式都完全受信任的情況下才使用。  
  
使用者執行個體案例包括：  
  
- 任何不需要共用資料的單一使用者應用程式。  
  
- ClickOnce 部署。 如果目標電腦上已安裝 .NET Framework 2.0 (或更新版本) 或 .NET Core 1.0 (或更新版本) 和 SQL Server Express，則非系統管理員的使用者也可以安裝及使用因採取 ClickOnce 動作而下載的安裝套件。 請注意，若 SQL Server Express 是安裝程式的一部分，則系統管理員必須加以安裝。 如需詳細資訊，請參閱 [Windows Forms 的 ClickOnce 部署](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms)。
  
- 使用 Windows 驗證的專用 ASP.NET 裝載。 單一 SQL Server Express 執行個體可以裝載在內部網路上。 應用程式會使用 ASPNET Windows 帳戶來連線，而不是使用模擬。 使用者執行個體不應用於協力廠商或共用裝載案例，其中所有應用程式都會共用相同的使用者執行個體，而且不會再互相保持隔離。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
