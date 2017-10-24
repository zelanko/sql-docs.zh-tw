---
title: "安全性概觀 (SQL Server R Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8388d7c9d22a49a49a1a45a6fa6b479107f9ccae
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview-sql-server-r-services"></a>安全性概觀 (SQL Server R Services)

本主題描述用於將 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料庫引擎和相關元件連接到 R 執行階段的整體安全性架構。 以下提供兩個將 R 用於企業環境之常見案例的安全性程序範例：

+ 從資料科學用戶端在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中執行 RevoScaleR 函數
+ 使用預存程序從 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 直接執行 R

## <a name="security-overview"></a>安全性概觀

A[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]登入或 Windows 使用者帳戶，才能執行 R 指令碼，使用 SQL Server 資料或透過 SQL Server 當成計算內容執行的。 這個需求同時適用於[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]和 SQL Server 2017 機器學習服務。 

登入或使用者帳戶識別*安全性主體*，可能需要多個層級的存取權，視 R 指令碼需求而定：
+ 其中 R 啟用的資料庫的存取權限
+ 若要從受保護的物件，例如資料表讀取資料的權限
+ 資料表，例如模型，或計分結果寫入新資料的能力
+ 能夠建立新的物件，例如資料表、 預存程序，使用 R 指令碼，或自訂函式已使用 R 的工作
+ 若要使用 R 封裝提供給一群使用者的 SQL Server 電腦上安裝新的封裝權限。 

因此，每個人都可以執行 R 程式碼使用[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]與執行內容必須對應到登入資料庫。 在 SQL Server 安全性會通常最簡單的方式建立角色，以管理集合的權限，並將使用者指派給這些角色，而不是個別設定使用者權限。 

例如，假設您建立一些在您的膝上型電腦執行的 R 程式碼，而且想要在執行該程式碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 唯有符合這些條件，您可以這樣做：

+ 該資料庫允許遠端連線。
+ 已在執行個體層級將具有用來執行 R 程式碼的名稱和密碼的 SQL 登入新增到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 或者，如果您是使用 Windows 整合式驗證，則必須將連接字串中指定的 Windows 使用者新增到執行個體。
+ SQL 登入或 Windows 使用者必須有執行外部指令碼的權限。 一般而言，只有資料庫管理員可以授與此權限。
+ 必須在以 R 作業執行下列任一作業的每個資料庫中，將 SQL 登入或 Window 使用者新增為具有適當權限的使用者：
    + 擷取資料
    + 寫入或更新資料 
    + 建立新物件，例如，資料表或預存程序

登入或 Windows 使用者帳戶已佈建及提供必要的權限之後，您可以執行 R 程式碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]使用 R 資料來源物件，或藉由呼叫預存程序。 每當從啟動 R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，資料庫引擎安全性取得的安全性內容的使用者啟動 R 工作或執行預存程序，並管理使用者或登入的安全物件的對應。 

因此，從遠端用戶端起始的所有 R 工作必須登入或使用者資訊指定為連接字串的一部分。

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安全性與 LaunchPad 安全性的互動

當 R 指令碼是在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦的內容中執行時，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務會從針對外部處理序所建立的背景工作帳戶集區，取得可用的背景工作帳戶 (本機使用者帳戶)，並使用該背景工作帳戶來執行相關工作。 

例如，如果您在您的 Windows 網域認證之下啟動 R 作業，則您的帳戶應該會對應到 Launchpad 背景工作帳戶 *SQLRUser01*。

對應到背景工作帳戶之後，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 會建立用來啟動處理序的使用者權杖。 

當所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 作業都完成之後，系統會將使用者背景工作帳戶標示為可用並返回到集區。

如需 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 的詳細資訊，請參閱 [SQL Server 中支援 R 整合的新元件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md)。

> [!NOTE]
為了讓 Launchpad 管理背景工作帳戶並執行 R 作業，包含背景工作帳戶的群組 (SQLRUserGroup) 必須有「允許本機登入」權限，否則 R Services 可能無法運作。 根據預設，系統會為所有新的本機使用者授與此權限，但某些組織中可能執行更嚴格的群組原則，而使背景工作帳戶無法連線到 SQL Server 執行 R 作業。  

## <a name="security-of-worker-accounts"></a>背景工作帳戶的安全性

外部的 Windows 使用者或背景工作帳戶的有效 SQL 登入的對應無效，只會針對執行 R 指令碼的 SQL 查詢的存留期的存留期。 

來自相同登入的平行查詢會對應到相同的使用者背景工作帳戶。

處理序所使用的目錄是由 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 使用 RLauncher 來管理，且目錄的存取權有所限制。 背景工作帳戶無法存取自身資料夾上層的任何檔案，但它可以讀取、寫入或刪除針對使用 R 指令碼之 SQL 查詢所建立的工作階段工作資料夾下的子項目。

如需變更背景工作帳戶的數目、帳戶名稱或帳戶密碼的詳細資訊，請參閱[修改 SQL Server R Services 的使用者帳戶集區](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。


## <a name="security-isolation-for-multiple-external-scripts"></a>多個外部指令碼的安全性隔離

隔離機制是以實體使用者帳戶為基礎。 因為附屬處理序是針對特定語言執行階段而啟動，所以每個附屬工作都使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 所指定的背景工作帳戶。 如果工作需要多個附屬 (例如，在平行查詢的案例中)，單一背景工作帳戶會用於所有相關工作。

任何背景工作帳戶都不能看到或操作其他背景工作帳戶使用的檔案。
 
如果您是該電腦上的系統管理員，您可以檢視針對每個處理序所建立的目錄。 每個目錄是以其工作階段 GUID 來識別。

## <a name="see-also"></a>另請參閱
[架構概觀](../../advanced-analytics/r-services/architecture-overview-sql-server-r.md)

