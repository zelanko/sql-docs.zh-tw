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
ms.openlocfilehash: 6ddfc3ccb67d017dc618cfbb7e7680c0164f3a21
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview"></a>安全性概觀

本主題描述用來連接的安全性架構[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]資料庫引擎和 Python 元件。 提供兩個常見案例的安全性程序的範例： 使用預存程序，並與 SQL Server 做為遠端計算內容中執行 Python 的 SQL Server 中執行 Python。

## <a name="security-overview"></a>安全性概觀

A[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]登入或 Windows 使用者帳戶，才能在 SQL Server 中執行 Python 指令碼。 登入或使用者帳戶識別*安全性主體*，必須擁有存取資料擷取所在資料庫的權限。 根據是否 Python 指令碼會建立新的物件，或寫入新的資料，使用者可能需要建立資料表、 寫入資料，或建立自訂函式或預存程序的權限。

因此，它是嚴格的要求，每個執行 Python 程式碼的人員在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]必須對應至登入或資料庫中的帳戶。 這項限制適用於無論指令碼從遠端資料科學用戶端傳送，或使用 T-SQL 預存程序啟動。

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


## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安全性與 LaunchPad 安全性的互動

內容中執行 Python 指令碼時[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]電腦[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服務取得從外部處理序，建立背景工作帳戶的集區的可用工作者帳戶 （本機使用者帳戶），並使用該背景工作帳戶執行相關的工作。

例如，假設您啟動 Windows 網域認證的 Python 指令碼。 SQL Server 會取得您的認證，並對應至使用啟動控制板背景工作帳戶，例如*SQLRUser01*。

> [!NOTE]
> 背景工作帳戶的名稱是群組的不論您群組的使用 R 或 Python 相同。 不過，每個執行個體，您啟用任何外部語言建立個別的群組。

對應到背景工作帳戶之後，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 會建立用來啟動處理序的使用者權杖。 

當所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 作業都完成之後，系統會將使用者背景工作帳戶標示為可用並返回到集區。

如需有關[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，請參閱[支援 Python 整合 SQL Server 中的新元件](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md)。

> [!NOTE]
> 針對 [啟動列] 來管理背景工作帳戶和執行 Python 工作，包含背景工作帳戶的群組*SQLRUserGroup*，必須有 「 允許本機登入 」 權限; 否則 Python 執行階段可能不會啟動。 根據預設，此權限提供給所有新的本機使用者，但是在某些組織中更嚴格的群組原則可能會強制執行，這可以防止背景工作帳戶 Python 工作連接到 SQL Server。

## <a name="security-of-worker-accounts"></a>背景工作帳戶的安全性

外部的 Windows 使用者或背景工作帳戶的有效 SQL 登入的對應無效，只會針對存留期的 SQL 預存程序執行 Python 指令碼。

來自相同登入的平行查詢會對應到相同的使用者背景工作帳戶。

用於處理序的目錄由管理[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，和目錄的存取限制。 對於 Python PythonLauncher 會執行這項工作。 每個個別的背景工作帳戶限制為它自己的資料夾，而無法存取它自己的層級上面的資料夾中的檔案。 不過，背景工作帳戶可以讀取、 寫入或刪除已建立的工作階段工作資料夾底下的子系。

如需變更背景工作帳戶的數目、帳戶名稱或帳戶密碼的詳細資訊，請參閱[修改 SQL Server R Services 的使用者帳戶集區](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。


## <a name="security-isolation-for-multiple-external-scripts"></a>多個外部指令碼的安全性隔離

隔離機制是以實體使用者帳戶為基礎。 因為附屬處理序是針對特定語言執行階段而啟動，所以每個附屬工作都使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 所指定的背景工作帳戶。 如果工作需要多個附屬 (例如，在平行查詢的案例中)，單一背景工作帳戶會用於所有相關工作。

任何背景工作帳戶都不能看到或操作其他背景工作帳戶使用的檔案。

如果您是該電腦上的系統管理員，您可以檢視針對每個處理序所建立的目錄。 每個目錄是以其工作階段 GUID 來識別。

## <a name="see-also"></a>另請參閱

[架構概觀](../../advanced-analytics/python/architecture-overview-sql-server-python.md)

