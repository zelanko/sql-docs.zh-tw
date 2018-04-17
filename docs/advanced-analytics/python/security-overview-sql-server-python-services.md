---
title: Python SQL Server 中的安全性概觀 |Microsoft 文件
ms.custom: ''
ms.date: 11/03/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: c8695dce528e84b1761d67abd99f94dc91c01538
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="security-overview-for-python-in-sql-server"></a>Python SQL Server 中的安全性概觀
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題描述用來連接的安全性架構[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]資料庫引擎和 Python 元件。 提供兩個常見案例的安全性程序的範例： 使用預存程序，並與 SQL Server 做為遠端計算內容中執行 Python 的 SQL Server 中執行 Python。

## <a name="security-overview"></a>安全性概觀

A[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]登入或 Windows 使用者帳戶，才能在 SQL Server 中執行 Python 指令碼。 這些*安全性主體*所管理的執行個體和資料庫層級，以及識別使用者有權限可連接到資料庫、 讀取及寫入資料，或建立資料庫物件，例如資料表或預存程序。 此外，執行 Python 指令碼的使用者必須擁有執行外部指令碼，在資料庫層級的權限。

在 [外部工具] 中使用 Python 的使用者必須對應到登入或資料庫中的帳戶，如果使用者需要執行 Python 程式碼中的資料庫，或存取資料庫物件和資料。 Python 指令碼是否會從遠端資料科學用戶端傳送，或使用 T-SQL 預存程序啟動，則需要使用相同的權限。

例如，假設您建立您的膝上型電腦執行的 Python 指令碼，而且想要在執行該程式碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 您必須確認符合下列條件：

+ 該資料庫允許遠端連線。
+ SQL 登入或您用來進行資料庫存取的 Windows 帳戶已新增至[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]執行個體層級。
+ 必須將執行外部指令碼的權限授與 SQL 登入或 Windows 使用者。 一般而言，只有資料庫管理員可以授與此權限。
+ SQL 登入或使用者視窗必須以具有適當的權限，其中 Python 指令碼會執行任何一項作業的每個資料庫中的使用者，加入：
    + 擷取資料
    + 寫入或更新資料
    + 建立新物件，例如，資料表或預存程序

登入或 Windows 使用者帳戶已佈建及提供必要的權限之後，您可以執行 Python 程式碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]使用所提供的資料來源物件**revoscalepy**程式庫，或藉由呼叫預存包含 Python 指令碼的程序。

每當從啟動的 Python 指令碼[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，資料庫引擎安全性取得開始工作，及管理使用者或登入的安全物件的對應之使用者的安全性內容。

因此，所有從遠端用戶端起始的 Python 指令碼必須指定登入或使用者的資訊做為連接字串的一部分。

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>之間的互動[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]安全性和啟動列的安全性

內容中執行 Python 指令碼時[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]電腦[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服務取得從外部處理序，建立背景工作帳戶的集區的可用工作者帳戶 （本機使用者帳戶），並使用該背景工作帳戶執行相關的工作。

例如，假設您啟動 Windows 網域認證的 Python 指令碼。 SQL Server 取得您的認證，並將工作對應至可用的啟動列背景工作帳戶，例如*SQLRUser01*。

> [!NOTE]
> 背景工作帳戶的名稱是群組的不論您群組的使用 R 或 Python 相同。 不過，每個執行個體，您啟用任何外部語言建立個別的群組。

對應到背景工作帳戶之後，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 會建立用來啟動處理序的使用者權杖。 

當所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 作業都完成之後，系統會將使用者背景工作帳戶標示為可用並返回到集區。

如需有關[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，請參閱[支援 Python 整合 SQL Server 中的元件](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md)。

### <a name="implied-authentication"></a>隱含驗證

**隱含的驗證**是一詞用於程序的 SQL Server 取得的使用者認證，然後執行 代表使用者，並假設使用者在資料庫中具有正確的權限的所有外部指令碼工作。 隱含的驗證是特別重要，如果 Python 指令碼需要 SQL Server 資料庫外部的 ODBC 呼叫。 例如，程式碼可能會從試算表或其他來源擷取的因素較短的清單。

對這類回送的呼叫成功，群組包含的背景工作帳戶，SQLRUserGroup 必須要有 「 允許本機登入 」 權限。 根據預設，此權限提供給所有新的本機使用者，但是在某些組織可能會強制執行更嚴格的群組原則。

![R 的隱含的驗證](media/implied-auth-python2.png)

## <a name="security-of-worker-accounts"></a>背景工作帳戶的安全性

外部的 Windows 使用者或背景工作帳戶的有效 SQL 登入的對應無效，只會針對存留期的 SQL 預存程序執行 Python 指令碼。

來自相同登入的平行查詢會對應到相同的使用者背景工作帳戶。

用於處理序的目錄由管理[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，和目錄的存取限制。 對於 Python PythonLauncher 會執行這項工作。 每個個別的背景工作帳戶限制為它自己的資料夾，而無法存取它自己的層級上面的資料夾中的檔案。 不過，背景工作帳戶可以讀取、 寫入或刪除已建立的工作階段工作資料夾底下的子系。

如需如何變更的背景工作帳戶，帳戶名稱或帳戶的密碼數目的詳細資訊，請參閱[修改使用者帳戶集區，SQL Server 機器學習](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。


## <a name="security-isolation-for-multiple-external-scripts"></a>多個外部指令碼的安全性隔離

隔離機制根據實體的使用者帳戶。 因為附屬處理序是針對特定語言執行階段而啟動，所以每個附屬工作都使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 所指定的背景工作帳戶。 如果工作需要多個附屬 (例如，在平行查詢的案例中)，單一背景工作帳戶會用於所有相關工作。

任何背景工作帳戶都不能看到或操作其他背景工作帳戶使用的檔案。

如果您是該電腦上的系統管理員，您可以檢視針對每個處理序所建立的目錄。 每個目錄是以其工作階段 GUID 來識別。

## <a name="see-also"></a>另請參閱

[架構概觀](../../advanced-analytics/python/architecture-overview-sql-server-python.md)
