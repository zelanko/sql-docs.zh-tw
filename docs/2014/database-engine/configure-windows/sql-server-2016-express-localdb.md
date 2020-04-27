---
title: SQL Server 2014 Express LocalDB |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 224facf54b0cde09f97010be472e3cc28754e94b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62757000"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]是以程式開發人員[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]為目標的執行模式。 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` `LocalDB`安裝會複製啟動所[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]需的最小檔案集合。 安裝`LocalDB`之後，開發人員會使用特殊的連接字串來起始連接。 連接時，就會自動建立及啟動必要的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基礎結構，應用程式不需複雜或耗時的組態工作即可開始使用資料庫。 Developer Tools 為開發人員提供 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，讓他們撰寫和測試 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，而不需要管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的完整伺服器執行個體。 的實例[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB`是使用`SqlLocalDB.exe`公用程式來管理。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB`應該用來取代已被取代[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]的使用者實例功能。  
  
## <a name="installing-localdb"></a>安裝 LocalDB  
 安裝`LocalDB`的主要方法是使用 SqlLocalDB .msi 程式。 `LocalDB`是安裝的[!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]任何 SKU 時的選項。 在`LocalDB`安裝期間，于 [**特徵選取**] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]頁面上選取。 每個主要`LocalDB` [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]版本只能有一個二進位檔案安裝。 多個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理序可以啟動，而且全部都會使用相同的二進位檔案。 當做[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]啟動的實例與`LocalDB`具有相同的限制[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>描述  
 `LocalDB`安裝程式會使用 SqlLocalDB 程式在電腦上安裝必要的檔案。 安裝之後， `LocalDB`就是可建立[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]及開啟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫的實例。 資料庫的系統資料庫檔案儲存在使用者本機上通常處於隱藏狀態的 AppData 路徑。 例如 **C:\Users\\<使用者\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**。 使用者資料庫檔案儲存在使用者指定的位置，通常是在 **C:\Users\\<使用者\>\Documents\\** 資料夾中的某個位置。  
  
 如需在應用程式`LocalDB`中包含的詳細資訊， [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]請參閱檔[本機資料總覽](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx)、[逐步解說：建立 SQL Server LocalDB 資料庫](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)和[逐步解說：連接到 SQL Server localdb 資料庫中的資料（Windows Forms）](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx)。  
  
 如需有關 API 的`LocalDB`詳細資訊，請參閱[SQL SERVER EXPRESS LocalDB 實例 API 參考](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx)和[LocalDBStartInstance](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx)函式。  
  
 SqlLocalDb 公用程式可以建立的`LocalDB`新實例、啟動和停止的實例`LocalDB`，並包含可協助您管理`LocalDB`的選項。  如需 SqlLocalDb 公用程式的詳細資訊，請參閱 [SqlLocalDB 公用程式](../../tools/sqllocaldb-utility.md)。  
  
 的實例定序`LocalDB`設定為 SQL_Latin1_General_CP1_CI_AS，而且無法變更。 通常支援資料庫層級、資料行層級和運算式層級定序。 自主資料庫遵循 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)所定義的中繼資料和 tempdb 定序規則。  
  
### <a name="restrictions"></a>限制  
 `LocalDB`不可以是合併式複寫訂閱者。  
  
 `LocalDB`不支援 FILESTREAM。  
  
 `LocalDB`僅允許 Service Broker 的本機佇列。  
  
 內建帳戶`LocalDB` （例如 NT AUTHORITY\SYSTEM）所擁有的實例，可能因為 windows 檔案系統重新導向而有管理性問題。改為使用一般 windows 帳戶作為擁有者。  
  
### <a name="automatic-and-named-instances"></a>自動和具名執行個體  
 `LocalDB`支援兩種類型的實例：自動實例和已命名的實例。  
  
-   的自動實例`LocalDB`是公用的。 這些執行個體會自動為使用者建立及管理，並且可供任何應用程式使用。 在使用者電腦上`LocalDB` `LocalDB`安裝的每個版本都有一個自動實例。 自動實例可`LocalDB`提供無縫的實例管理。 無需建立執行個體，它就會運作。 這允許應用程式輕鬆安裝和移轉到另一部電腦。 如果目標電腦已安裝指定的 `LocalDB` 版本，該目標電腦可以使用此版本的 `LocalDB` 自動執行個體。 的`LocalDB`自動實例具有屬於保留命名空間之實例名稱的特殊模式。 這可避免與的`LocalDB`已命名實例發生名稱衝突。 自動執行個體的名稱是 **MSSQLLocalDB**。  
  
-   的命名實例`LocalDB`是私用的。 這些執行個體是由負責建立及管理該執行個體的單一應用程式所擁有。 具名執行個體與其他執行個體隔離，並透過減少與其他資料庫使用者的資源競爭來提高效能。 已命名的實例必須由使用者透過`LocalDB`管理 API 明確建立，或透過 managed 應用程式的 app.config 檔案以隱含的方式建立（雖然如有需要，受控應用程式也可以使用 API）。 的`LocalDB`每一個實例都有相關`LocalDB`聯的版本，指向各自的`LocalDB`一組二進位檔。 的實例名稱`LocalDB`是`sysname`資料類型，最多可以有128個字元。 （這不同于的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一般命名實例，其會將名稱限制為16個 ASCII 字元的一般 NetBIOS 名稱）。實例的名稱`LocalDB`可以包含檔案名中合法的任何 Unicode 字元。  使用自動執行個體名稱的具名執行個體會成為自動執行個體。  
  
 電腦的不同使用者可有同名的執行個體。 每個執行個體都是以不同使用者身分執行的不同處理序。  
  
## <a name="shared-instances-of-localdb"></a>LocalDB 的共用執行個體  
 為了支援電腦的多個使用者需要連接到單一實例的`LocalDB`案例， `LocalDB`支援實例共用。 執行個體擁有者可以選擇允許電腦上的其他使用者連接到他的執行個體。 可以共用的自動和已`LocalDB`命名的實例。 若要共用 `LocalDB` 執行個體，使用者必須為它選取共用名稱 (別名)。 因為電腦上的所有使用者都可以看到共用名稱，此共用名稱在電腦上必須是唯一的。 實例的共用名稱與的命名`LocalDB`實例具有相同的格式`LocalDB`。  
  
 只有電腦上的系統管理員可以建立的共用實例`LocalDB`。 的共用實例`LocalDB`可由系統管理員或共用實例的擁有者取消共用`LocalDB`。 若要共用和取消共用的`LocalDB`實例，請`LocalDBShareInstance`使用`LocalDBUnShareInstance` `LocalDB` API 的和方法，或 SqlLocalDb 公用程式的共用和取消共用選項。  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>啟動 LocalDB 以及連接到 LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>連接到自動執行個體  
 使用`LocalDB`的最簡單方式是使用連接字串 **"Server = （localdb） \MSSQLLocalDB; 整合式安全性 = true"** 連接到目前使用者所擁有的自動實例。 若要使用檔案名稱來連接到特定的資料庫，請使用類似於 **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"** 的連接字串進行連接。  
  
> [!NOTE]  
>  第一次在電腦上的使用者嘗試連接到`LocalDB`時，必須同時建立和啟動自動實例。 建立執行個體所需的額外時間可能會導致連接嘗試失敗並顯示逾時訊息。 發生這種情況時，請等候幾秒鐘，讓建立程序完成，然後再重新連接。  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>建立及連接到具名執行個體  
 除了自動實例之外，也支援`LocalDB`已命名的實例。 使用 SqlLocalDB 程式來建立、啟動和停止的已命名實例`LocalDB`。 如需 SqlLocalDB.exe 的詳細資訊，請參閱 [SqlLocalDB 公用程式](../../tools/sqllocaldb-utility.md)。  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 以上最後一行傳回的資訊如下所示。  
  
|||  
|-|-|  
|名稱|"LocalDBApp1"|  
|版本|\<目前版本>|  
|共用名稱|""|  
|擁有者|"\<您的 Windows 使用者>"|  
|自動建立|否|  
|State|執行中|  
|上次啟動時間|\<日期和時間>|  
|執行個體管道名稱|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  如果您的應用程式在4.0.2 之前使用 .NET 版本，您必須直接連接到的具名管道`LocalDB`。 實例管道名稱值是實例`LocalDB`正在接聽的具名管道。 在 LOCALDB # 之後，實例管道名稱的部分將會在每次啟動實例`LocalDB`時變更。 若要[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]使用連接到的`LocalDB`實例，請在 [**連接到[!INCLUDE[ssDE](../../includes/ssde-md.md)] ** ] 對話方塊的 [**伺服器名稱**] 方塊中，輸入實例管道名稱。 從您的自訂程式，您可以使用類似于`LocalDB`的連接字串，建立與實例的連接。`SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>連接到 LocalDB 的共用執行個體  
 若要連接到連接字串的`LocalDB`共用**實例\\ （點**+ 反斜線），以參考保留給共用實例的命名空間。 例如，若要連接到`LocalDB`名為`AppData`的共用實例，請使用連接字串， `(localdb)\.\AppData`例如，做為連接字串的一部分。 連接到不在其擁有之共用`LocalDB`實例的使用者，必須具有 Windows 驗證或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入。  
  
## <a name="troubleshooting"></a>疑難排解  
 如需疑難排解`LocalDB`的相關資訊，請參閱[疑難排解 SQL Server 2012 Express LocalDB](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)。  
  
## <a name="permissions"></a>權限  
 的實例[!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB`是由使用者建立的實例，供其使用。 電腦上的任何使用者都可以使用的實例建立資料庫`LocalDB`、在其使用者設定檔下儲存檔案，並在其認證之下執行進程。 根據預設，對實例的`LocalDB`存取權僅限於其擁有者。 包含在中`LocalDB`的資料受到資料庫檔案之檔案系統存取的保護。 如果使用者資料庫檔案儲存在共用位置中，任何人都可以使用其擁有的實例`LocalDB` ，來開啟該位置的檔案系統存取權。 如果資料庫檔案位於受保護的位置，例如使用者資料夾，則只有該使用者和擁有該資料夾存取權的任何系統管理員才可以開啟資料庫。 `LocalDB`檔案一次只能由一個實例`LocalDB`開啟。  
  
> [!NOTE]  
>  `LocalDB`一律在使用者安全性內容下執行;也就是`LocalDB` ，絕對不會使用本機系統管理員群組的認證來執行。 這表示`LocalDB`實例所使用的所有資料庫檔案都必須可使用擁有使用者的 Windows 帳戶來存取，而不需要考慮本機 Administrators 群組的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [SqlLocalDB 公用程式](../../tools/sqllocaldb-utility.md)  
  
  
