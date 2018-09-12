---
title: SQL Server machine learning 及 R 的安全性 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c04670464d23f0951a957df945a2e81b817ae134
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889184"
---
# <a name="security-for-sql-server-machine-learning-and-r"></a>SQL Server machine learning 及 R 的安全性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明用來連接的整體安全性架構[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]資料庫引擎和 R 執行階段的相關的元件。 針對這些常見的案例，在企業環境中使用 R 提供的安全性程序的範例：

+ 從資料科學用戶端在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中執行 RevoScaleR 函數
+ 使用預存程序從 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 直接執行 R

## <a name="security-overview"></a>安全性概觀

A[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]登入或 Windows 使用者帳戶，才能執行 R 指令碼，使用 SQL Server 資料，或包含執行與 SQL Server 計算內容。 這項需求同時適用於[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]和 SQL Server 2017 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]。

登入或使用者帳戶識別*安全性主體*，可能需要多個層級的存取權，並根據 R 指令碼需求的使用者：

+ 若要存取已啟用 R 的資料庫的權限
+ 若要從受保護的物件，例如資料表讀取資料的權限
+ 能夠將新的資料寫入至資料表，例如模型或評分結果
+ 能夠建立新的物件，例如資料表、 預存程序，使用 R 指令碼，或自訂函式已使用 R 的工作
+ 若要安裝新套件的 SQL Server 電腦上使用 R 封裝提供給一群使用者權限。 

因此，每個人都可以執行 R 程式碼使用[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]與執行內容都必須對應至資料庫中的登入。 在 SQL Server 安全性是通常最簡單的方式建立角色，以管理集合的權限，並將使用者指派給這些角色，而不是個別設定 使用者權限。 

例如，假設您建立一些會在您的膝上型電腦執行的 R 程式碼，以及您想要執行該程式碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 只有符合這些條件時，您可以這麼做：

+ 該資料庫允許遠端連線。
+ 已在執行個體層級將具有用來執行 R 程式碼的名稱和密碼的 SQL 登入新增到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 或者，如果您是使用 Windows 整合式驗證，則必須將連接字串中指定的 Windows 使用者新增到執行個體。
+ SQL 登入或 Windows 使用者必須執行外部指令碼的權限。 一般而言，只有資料庫管理員可以授與此權限。
+ 必須在以 R 作業執行下列任一作業的每個資料庫中，將 SQL 登入或 Window 使用者新增為具有適當權限的使用者：
    + 擷取資料
    + 寫入或更新資料 
    + 建立新物件，例如，資料表或預存程序

登入或 Windows 使用者帳戶已佈建並具有必要的權限之後，您可以執行 R 程式碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]使用 R 資料來源物件，或藉由呼叫預存程序。 每當啟動 R 時從[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，database engine 安全性取得啟動 R 工作或執行預存程序，及管理對應的使用者或登入安全性實體物件之使用者的安全性內容。 

因此，從遠端用戶端起始的所有 R 作業必須都指定登入或使用者資訊的連接字串的一部分。

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>之間的互動[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]安全性與 Launchpad 安全性

當 R 指令碼是在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦的內容中執行時，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務會從針對外部處理序所建立的背景工作帳戶集區，取得可用的背景工作帳戶 (本機使用者帳戶)，並使用該背景工作帳戶來執行相關工作。 

例如，如果您在您的 Windows 網域認證之下啟動 R 作業，則您的帳戶應該會對應到 Launchpad 背景工作帳戶 *SQLRUser01*。

對應到背景工作帳戶之後，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 會建立用來啟動處理序的使用者權杖。 

當所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 作業都完成之後，系統會將使用者背景工作帳戶標示為可用並返回到集區。

如需有關服務的詳細資訊，請參閱[Extensibility framework](../concepts/extensibility-framework.md)。 

### <a name="implied-authentication"></a>隱含驗證

**隱含的驗證**是一詞用於程序所在的 SQL Server 取得的使用者認證，然後執行所有的外部指令碼工作，代表使用者，並假設使用者在資料庫中有正確的權限。 隱含的驗證是特別重要，如果 R 指令碼需要進行 ODBC 呼叫 SQL Server 資料庫之外的位置。 比方說，程式碼可能會從試算表或其他來源擷取的因素較短的清單。

這類回送呼叫完成，包含背景工作帳戶，SQLRUserGroup 的群組必須有 「 允許本機登入 」 權限。 根據預設，此權限提供給所有新的本機使用者，，但在某些組織可能會強制執行更嚴格的群組原則。

![適用於 R 的隱含的驗證](media/implied-auth-rsql.png)

## <a name="security-of-worker-accounts"></a>背景工作帳戶的安全性

外部 Windows 使用者或背景工作帳戶的有效 SQL 登入的對應只會針對 SQL 查詢執行 R 指令碼的存留期的存留期是有效的。

來自相同登入的平行查詢會對應到相同的使用者背景工作帳戶。

處理序所使用的目錄是由 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 使用 RLauncher 來管理，且目錄的存取權有所限制。 背景工作帳戶無法存取自身資料夾上層的任何檔案，但它可以讀取、寫入或刪除針對使用 R 指令碼之 SQL 查詢所建立的工作階段工作資料夾下的子項目。

如需如何變更的背景工作帳戶、 帳戶名稱或帳戶的密碼數目的詳細資訊，請參閱[修改 SQL Server 機器學習服務的使用者帳戶集區](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。

## <a name="security-isolation-for-multiple-external-scripts"></a>多個外部指令碼的安全性隔離

隔離機制是以實體使用者帳戶為基礎。 因為附屬處理序是針對特定語言執行階段而啟動，所以每個附屬工作都使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 所指定的背景工作帳戶。 如果工作需要多個附屬 (例如，在平行查詢的案例中)，單一背景工作帳戶會用於所有相關工作。

任何背景工作帳戶都不能看到或操作其他背景工作帳戶使用的檔案。
 
如果您是該電腦上的系統管理員，您可以檢視針對每個處理序所建立的目錄。 每個目錄是以其工作階段 GUID 來識別。

## <a name="see-also"></a>另請參閱

[適用於 SQL Server machine learning 的架構概觀](../../advanced-analytics/r/architecture-overview-sql-server-r.md)
