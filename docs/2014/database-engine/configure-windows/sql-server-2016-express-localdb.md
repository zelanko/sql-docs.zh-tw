---
title: SQL Server 2014 Express LocalDB | Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757000"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` 執行模式[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]專供程式開發人員。 `LocalDB` 安裝會複製檔案啟動所需的最小集合[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 一次`LocalDB`是安裝，開發人員起始的連線使用特殊連接字串。 連接時，就會自動建立及啟動必要的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基礎結構，應用程式不需複雜或耗時的組態工作即可開始使用資料庫。 Developer Tools 為開發人員提供 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，讓他們撰寫和測試 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，而不需要管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的完整伺服器執行個體。 執行個體[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB`由`SqlLocalDB.exe`公用程式。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB` 應該用於取代[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]使用者執行個體功能已被取代。  
  
## <a name="installing-localdb"></a>安裝 LocalDB  
 安裝的主要方法`LocalDB`是使用 SqlLocalDB.msi 程式。 `LocalDB` 安裝的任何 SKU 時[!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]。 選取 `LocalDB`上**特徵選取**頁面上，安裝期間[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 可以有一份`LocalDB`每個主要的二進位檔[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]版本。 多個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理序可以啟動，而且全部都會使用相同的二進位檔案。 執行個體[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]啟動為`LocalDB`具有相同的限制 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>描述  
 `LocalDB`安裝程式使用 SqlLocalDB.msi 程式來安裝必要的檔案，在電腦上。 安裝之後，`LocalDB`的執行個體[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]可建立及開啟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 資料庫的系統資料庫檔案儲存在使用者本機上通常處於隱藏狀態的 AppData 路徑。 例如 **C:\Users\\<使用者\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**。 使用者資料庫檔案儲存在使用者指定的位置，通常是在 **C:\Users\\<使用者\>\Documents\\** 資料夾中的某個位置。  
  
 如需詳細資訊，包括`LocalDB`應用程式，請參閱[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]文件[本機資料概觀](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx)，[逐步解說：建立 SQL Server LocalDB 資料庫](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)，和[逐步解說：連接到 SQL Server LocalDB 資料庫 (Windows Form) 中的資料](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx)。  
  
 如需詳細資訊`LocalDB`API，請參閱 < [SQL Server Express LocalDB 執行個體 API 參考](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx)並[LocalDBStartInstance 函數](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx)。  
  
 SqlLocalDb 公用程式可以建立的新執行個體`LocalDB`、 啟動及停止的執行個體`LocalDB`，並包含選項，可協助您管理`LocalDB`。  如需 SqlLocalDb 公用程式的詳細資訊，請參閱 [SqlLocalDB 公用程式](../../tools/sqllocaldb-utility.md)。  
  
 執行個體定序`LocalDB`設定為 SQL_Latin1_General_CP1_CI_AS，且無法變更。 通常支援資料庫層級、資料行層級和運算式層級定序。 自主資料庫遵循 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)所定義的中繼資料和 tempdb 定序規則。  
  
### <a name="restrictions"></a>限制  
 `LocalDB` 無法為合併式複寫訂閱者。  
  
 `LocalDB` 不支援 FILESTREAM。  
  
 `LocalDB` Service Broker 只允許本機佇列。  
  
 執行個體`LocalDB`擁有的內建帳戶，例如 NT AUTHORITY\SYSTEM 可以有管理能力問題，因為 windows 檔案系統重新導向;改為使用一般 windows 帳戶的擁有者。  
  
### <a name="automatic-and-named-instances"></a>自動和具名執行個體  
 `LocalDB` 支援兩種類型的執行個體：自動執行個體和具名執行個體。  
  
-   自動執行個體`LocalDB`都是公用的。 這些執行個體會自動為使用者建立及管理，並且可供任何應用程式使用。 自動執行個體`LocalDB`存在於每個版本的`LocalDB`使用者的電腦上安裝。 自動執行個體`LocalDB`提供無縫式的執行個體管理。 無需建立執行個體，它就會運作。 這允許應用程式輕鬆安裝和移轉到另一部電腦。 如果目標電腦已安裝指定的 `LocalDB` 版本，該目標電腦可以使用此版本的 `LocalDB` 自動執行個體。 自動執行個體`LocalDB`執行個體名稱採用屬於保留命名空間的特殊模式。 這可防止名稱衝突的具名執行個體`LocalDB`。 自動執行個體的名稱是 **MSSQLLocalDB**。  
  
-   具名執行個體`LocalDB`私用。 這些執行個體是由負責建立及管理該執行個體的單一應用程式所擁有。 具名執行個體與其他執行個體隔離，並透過減少與其他資料庫使用者的資源競爭來提高效能。 必須明確地建立具名的執行個體，由使用者透過`LocalDB`管理 API 或隱含地透過 app.config 檔案的受管理的應用程式 （雖然受管理的應用程式也可以使用 API，如有需要）。 每個具名執行個體`LocalDB`都有相關聯`LocalDB`版本，指向各自組`LocalDB`二進位檔。 執行個體名稱`LocalDB`是`sysname`資料類型，可以包含最多可有 128 個字元。 (這不同於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一般具名執行個體，其名稱限制為 16 個 ASCII 字元的一般 NetBIOS 名稱)。執行個體的名稱`LocalDB`可以包含任何合法的檔案名稱內的 Unicode 字元。  使用自動執行個體名稱的具名執行個體會成為自動執行個體。  
  
 電腦的不同使用者可有同名的執行個體。 每個執行個體都是以不同使用者身分執行的不同處理序。  
  
## <a name="shared-instances-of-localdb"></a>LocalDB 的共用執行個體  
 若要支援多個使用者的電腦需要連線到的單一執行個體的案例`LocalDB`，`LocalDB`支援執行個體共用。 執行個體擁有者可以選擇允許電腦上的其他使用者連接到他的執行個體。 自動和具名執行個體`LocalDB`可以共用。 若要共用 `LocalDB` 執行個體，使用者必須為它選取共用名稱 (別名)。 因為電腦上的所有使用者都可以看到共用名稱，此共用名稱在電腦上必須是唯一的。 執行個體的共用的名稱`LocalDB`具有相同格式的具名執行個體`LocalDB`。  
  
 只有在電腦上的系統管理員可以建立的共用執行個體`LocalDB`。 共用執行個體`LocalDB`可以是由系統管理員，或共用執行個體的擁有者取消共用`LocalDB`。 共用及取消共用的執行個體`LocalDB`，使用`LocalDBShareInstance`並`LocalDBUnShareInstance`方法`LocalDB`API，或共用及取消共用的選項 SqlLocalDb 公用程式。  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>啟動 LocalDB 以及連接到 LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>連接到自動執行個體  
 若要使用的最簡單方式`LocalDB`是連接到自動執行個體所使用的連接字串中目前使用者所擁有 **"Server = (localdb) \MSSQLLocalDB;Integrated 安全性 = true"**。 若要使用檔案名稱來連接到特定的資料庫，請使用類似於 **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"** 的連接字串進行連接。  
  
> [!NOTE]  
>  第一次在電腦上的使用者嘗試連線到`LocalDB`，自動執行個體必須同時建立並啟動。 建立執行個體所需的額外時間可能會導致連接嘗試失敗並顯示逾時訊息。 發生這種情況時，請等候幾秒鐘，讓建立程序完成，然後再重新連接。  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>建立及連接到具名執行個體  
 除了自動執行個體，`LocalDB`也支援具名執行個體。 使用 SqlLocalDB.exe 程式來建立、 啟動及停止的具名執行個體`LocalDB`。 如需 SqlLocalDB.exe 的詳細資訊，請參閱 [SqlLocalDB 公用程式](../../tools/sqllocaldb-utility.md)。  
  
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
|Version|\<目前版本>|  
|共用名稱|""|  
|[擁有者]|"\<您的 Windows 使用者>"|  
|自動建立|否|  
|State|執行中|  
|上次啟動時間|\<日期和時間>|  
|執行個體管道名稱|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  如果您的應用程式使用.NET 4.0.2 之前的版本您必須直接連接到的具名管道`LocalDB`。 執行個體管道名稱值是管道的具名執行個體`LocalDB`正在接聽。 之後 LOCALDB # 會變更每個執行個體管道名稱的部分時間的執行個體`LocalDB`已啟動。 若要連接到的執行個體`LocalDB`利用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，輸入執行個體管道名稱**伺服器名稱**方塊**連接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]**   對話方塊。 從您的自訂程式中，您可以建立執行個體的連線`LocalDB`使用類似的連接字串 `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>連接到 LocalDB 的共用執行個體  
 若要連接到的共用執行個體`LocalDB`新增 **。\\** （點 + 反斜線） 來參考保留給共用執行個體的命名空間的連接字串。 例如，若要連接到的共用執行個體`LocalDB`名為`AppData`使用的連接字串，例如`(localdb)\.\AppData`為連接字串的一部分。 連接到的共用執行個體的使用者`LocalDB`，不是他們擁有必須有 Windows 驗證或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入。  
  
## <a name="troubleshooting"></a>疑難排解  
 如需疑難排解資訊`LocalDB`，請參閱 <<c2> [ 疑難排解 SQL Server 2012 Express LocalDB](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)。  
  
## <a name="permissions"></a>Permissions  
 執行個體[!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]`LocalDB`是供其使用使用者所建立的執行個體。 在電腦上的任何使用者可以建立資料庫，使用的執行個體`LocalDB`、 在其使用者設定檔之下儲存檔案，並在其認證之下處理序執行。 根據預設，存取執行個體`LocalDB`只限其擁有者。 中包含的資料`LocalDB`受到資料庫檔案的檔案系統存取權。 如果使用者資料庫檔案儲存在共用位置，可以開啟資料庫至該位置的檔案系統存取權的任何人使用的執行個體`LocalDB`他們所擁有。 如果資料庫檔案位於受保護的位置，例如使用者資料夾，則只有該使用者和擁有該資料夾存取權的任何系統管理員才可以開啟資料庫。 `LocalDB`檔案只能開啟一個執行個體的`LocalDB`一次。  
  
> [!NOTE]  
>  `LocalDB` 一律使用者安全性內容下執行;也就是`LocalDB`絕對不會執行使用的認證從本機系統管理員群組。 這表示所有資料庫所使用的檔案`LocalDB`執行個體必須能夠使用擁有使用者的 Windows 帳戶，而不必考量本機系統管理員群組的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [SqlLocalDB 公用程式](../../tools/sqllocaldb-utility.md)  
  
  
