---
title: "安全性概觀 （SQL Server R 服務） | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# 安全性概觀 （SQL Server R 服務）

本主題描述用來連接的整體安全性架構 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料庫引擎和 R 的執行階段的相關的元件。 在企業環境中使用 R 的兩種常見的案例提供的安全性程序範例︰

+ 執行中的函式 RevoScaleR [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 從資料科學用戶端
+ 執行直接從 R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用預存程序

## 安全性概觀

A [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 登入或 Windows 使用者帳戶才能執行所有的 R 工作，以便利用 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]。 登入或使用者帳戶識別 *安全性主體*, ，又必須存取其中 R 在執行的資料庫的權限，來讀取受保護的物件，例如資料表、 資料或寫入新的資料，或加入新的物件，如果 R 作業所需的權限。

因此，它是嚴格要求，每個執行 R 程式碼的人對 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 必須對應至登入在資料庫中，不論該程式碼會傳送來自遠端資料科學的用戶端，使用 RevoScaleR 函式或使用 T-SQL 預存程序啟動。 

例如，假設您建立一些會在您的膝上型電腦執行的 R 程式碼，且您想要執行該程式碼 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 您必須確保符合下列條件︰

+ 資料庫會允許遠端連接。
+ SQL 登入名稱與您的 R 程式碼中使用的密碼已加入至 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體層級。 或者，如果您使用 Windows 整合式的驗證，必須將連接字串中指定 Windows 使用者加入執行個體上的使用者身分。
+ SQL 登入或 Windows 使用者必須具有權限來執行外部指令碼。 一般而言，此權限只能由資料庫管理員加入。
+ SQL 登入或使用者視窗中，都必須加入的使用者身分，其中 R 工作會執行任何一項作業的每個資料庫中的適當權限︰
    + 擷取資料
    + 寫入或更新資料 
    + 建立新的物件，例如資料表或預存程序

登入或 Windows 使用者帳戶已佈建並提供必要的權限之後，您可以執行 R 程式碼 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用 R 的資料來源物件，或呼叫預存程序。 每當從啟動 R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，database engine 安全性取得啟動 R 工作，及管理使用者或登入的安全物件的對應之使用者的安全性內容。 

因此，從遠端用戶端起始的所有 R 作業必須都指定登入或使用者資訊的連接字串的一部分。


## 之間的互動 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安全性和啟動列的安全性

R 指令碼的內容中執行時 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務從集區的工作者帳戶建立的外部處理序取得可用的工作者帳戶 （本機使用者帳戶），並使用該背景工作帳戶來執行相關的工作。 

例如，如果您啟動您的 Windows 網域認證 R 工作，您的帳戶可能會對應至啟動列背景工作帳戶 *SQLRUser01*。

對應至一個背景工作的帳戶之後, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 建立用來啟動處理序的使用者語彙基元。 

當所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 完成操作，會標示為任意使用者工作帳戶，並且將其傳回集區。

如需詳細資訊 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], ，請參閱 [支援 R 整合至 SQL Server 中的新元件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)。

## 背景工作帳戶的安全性
此對應的外部 Windows 使用者或背景工作帳戶的有效 SQL 登入僅都是有效的 SQL 查詢執行 R 指令碼的存留期的存留期。 

從相同的登入的平行查詢都會對應到相同的使用者工作帳戶。

處理程序所使用的目錄由 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 使用 RLauncher，和目錄都是限制存取。 背景工作帳戶無法存取，上述資料夾中的任何檔案，但它可以讀取、 寫入或刪除所建立的 SQL 查詢使用 R 指令碼工作階段工作資料夾下的子系。

如需如何變更數工作者帳戶，帳戶名稱或帳戶密碼的詳細資訊，請參閱 [修改使用者帳戶集區的 SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。


## 安全性隔離的多個外部指令碼

隔離機制根據實體的使用者帳戶。 附屬程序會啟動特定的語言執行平台，每個附屬工作會使用所指定的背景工作帳戶 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]。 如果工作需要多個附屬組件，例如，在平行查詢的情況單一背景工作帳戶用於所有相關的工作。

沒有背景工作的帳戶可以看到，或處理其他背景工作帳戶所使用的檔案。
 
如果您是電腦的系統管理員，您可以檢視每個處理序所建立的目錄。 其工作階段 GUID 來識別每個目錄。

## 另請參閱
[架構概觀](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)