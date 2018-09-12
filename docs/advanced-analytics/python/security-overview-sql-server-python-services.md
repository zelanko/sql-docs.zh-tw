---
title: SQL Server Machine Learning 中適用於 Python 的安全性概觀 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a33701283635327fcaac4a9629cb02044b30dda8
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43890054"
---
# <a name="security-overview-for-python-in-sql-server-machine-learning"></a>SQL Server Machine Learning 中適用於 Python 的安全性概觀
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題描述用來連接的安全性架構[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]資料庫引擎和 Python 元件。 提供兩個常見案例的安全性程序的範例： 使用預存程序中，並與 SQL Server 作為遠端計算內容中執行 Python 的 SQL Server 中執行 Python。

## <a name="security-overview"></a>安全性概觀

A[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]登入或 Windows 使用者帳戶，才能在 SQL Server 中執行 Python 指令碼。 這些*安全性主體*所管理的執行個體和資料庫層級，在識別使用者具有使用權限來連接到資料庫、 讀取及寫入資料，或建立資料庫物件，例如資料表或預存程序。 此外，執行 Python 指令碼的使用者必須具有執行資料庫層級的外部指令碼的權限。

即使在外部工具中使用 Python 的使用者必須對應至登入或資料庫中的帳戶，如果使用者需要執行 Python 程式碼中的資料庫，或存取資料庫物件和資料。 Python 指令碼是否會從遠端資料科學用戶端傳送，或使用 T-SQL 預存程序啟動，不需要使用相同的權限。

例如，假設您建立您的膝上型電腦執行的 Python 指令碼，以及您想要執行該程式碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 您必須確認符合下列條件：

+ 該資料庫允許遠端連線。
+ 您用來進行資料庫存取權的 Windows 帳戶的 SQL 登入已加入至[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]執行個體層級。
+ 必須將執行外部指令碼的權限授與 SQL 登入或 Windows 使用者。 一般而言，只有資料庫管理員可以授與此權限。
+ SQL 登入或 Window 使用者必須新增為使用者，具有適當的權限，其中的 Python 指令碼會執行任何這些作業的每個資料庫中：
    + 擷取資料
    + 寫入或更新資料
    + 建立新物件，例如，資料表或預存程序

登入或 Windows 使用者帳戶已佈建並具有必要的權限之後，您可以執行 Python 程式碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]使用所提供的資料來源物件**revoscalepy**程式庫，或藉由呼叫預存包含 Python 指令碼的程序。

從啟動 Python 指令碼是每當[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，database engine 安全性取得啟動工作，及管理對應的使用者或登入安全性實體物件之使用者的安全性內容。

因此，從遠端用戶端起始的所有 Python 指令碼必須登入或使用者資訊指定為連接字串的一部分。

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>之間的互動[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]安全性與 Launchpad 安全性

內容中執行 Python 指令碼時[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]電腦，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服務從外部處理序，建立的背景工作帳戶集區取得可用的背景工作帳戶 （本機使用者帳戶），並使用該背景工作帳戶執行相關的工作。

例如，假設您以您的 Windows 網域認證啟動 Python 指令碼。 SQL Server 取得您的認證，並將工作對應至可用的 Launchpad 背景工作帳戶，例如*SQLRUser01*。

> [!NOTE]
> 無論您使用 R 或 Python 相同的工作者帳戶群組的名稱。 不過，每個執行個體，您可以在此啟用任何外部語言建立個別的群組。

對應到背景工作帳戶之後，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 會建立用來啟動處理序的使用者權杖。 

當所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 作業都完成之後，系統會將使用者背景工作帳戶標示為可用並返回到集區。

如需有關服務的詳細資訊，請參閱[Extensibility framework](../concepts/extensibility-framework.md)。

### <a name="implied-authentication"></a>隱含驗證

**隱含的驗證**是一詞用於程序所在的 SQL Server 取得的使用者認證，然後執行所有的外部指令碼工作，代表使用者，並假設使用者在資料庫中有正確的權限。 隱含的驗證是特別重要，如果 Python 指令碼需要進行 ODBC 呼叫 SQL Server 資料庫之外的位置。 比方說，程式碼可能會從試算表或其他來源擷取的因素較短的清單。

這類回送呼叫完成，包含背景工作帳戶，SQLRUserGroup 的群組必須有 「 允許本機登入 」 權限。 根據預設，此權限提供給所有新的本機使用者，，但在某些組織可能會強制執行更嚴格的群組原則。

![適用於 R 的隱含的驗證](media/implied-auth-python2.png)

## <a name="security-of-worker-accounts"></a>背景工作帳戶的安全性

外部 Windows 使用者或背景工作帳戶的有效 SQL 登入的對應無效，只針對存留期的 sql 預存程序時，才執行 Python 指令碼。

來自相同登入的平行查詢會對應到相同的使用者背景工作帳戶。

處理程序所使用的目錄由[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，且目錄的存取限制。 對於 Python，PythonLauncher 會執行這項工作。 每個個別的背景工作帳戶限制為自己的資料夾，且無法存取自己的層級上面的資料夾中的檔案。 不過，將背景工作帳戶可以讀取、 寫入或刪除已建立的工作階段工作資料夾下的子系。

如需如何變更的背景工作帳戶、 帳戶名稱或帳戶的密碼數目的詳細資訊，請參閱[修改 SQL Server 機器學習服務的使用者帳戶集區](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。


## <a name="security-isolation-for-multiple-external-scripts"></a>多個外部指令碼的安全性隔離

隔離機制是以實體使用者帳戶為基礎。 因為附屬處理序是針對特定語言執行階段而啟動，所以每個附屬工作都使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 所指定的背景工作帳戶。 如果工作需要多個附屬 (例如，在平行查詢的案例中)，單一背景工作帳戶會用於所有相關工作。

任何背景工作帳戶都不能看到或操作其他背景工作帳戶使用的檔案。

如果您是該電腦上的系統管理員，您可以檢視針對每個處理序所建立的目錄。 每個目錄是以其工作階段 GUID 來識別。

## <a name="see-also"></a>另請參閱

[架構概觀](../../advanced-analytics/python/architecture-overview-sql-server-python.md)
