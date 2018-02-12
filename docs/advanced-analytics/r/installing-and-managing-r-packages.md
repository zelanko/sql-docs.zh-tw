---
title: "與 SQL Server 一起安裝的 R 封裝 |Microsoft 文件"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 082aea3b1cde3c335dd7fa51b8ef219fc30f7efd
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="r-packages-installed-with-sql-server"></a>與 SQL Server 一起安裝的 R 封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如果您安裝並啟用機器學習功能與 SQL Server 一起安裝的 R 封裝。 本文也說明如何管理和檢視現有的封裝，或新增封裝到 SQL Server 執行個體。

**適用於：** SQL Server 2017 機器學習服務 （資料庫）、 SQL Server 2016 R 服務 （資料庫）

## <a name="what-is-the-instance-library-and-where-is-it"></a>什麼是執行個體文件庫，以及在哪裡可以找到？

任何 SQL Server 中執行的 R 解決方案可以使用安裝在執行個體相關聯的預設 R 程式庫中的封裝。 當您安裝 R 功能在 SQL Server 中時，R 封裝程式庫位於執行個體資料夾底下。

+ 預設執行個體*MSSQLSERVER* 

    SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQL Server 2016: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ 具名執行個體*已 MyNamedInstance* 

    SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQL Server 2016: `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

您可以執行下列陳述式來確認目前的 R 執行個體的預設程式庫。

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

您可以使用新的 Alternatiely，物[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函式中，如果執行預存程序\_執行\_外部\_直接在目標電腦上的指令碼。 此函式不能傳回遠端連接程式庫的路徑。

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
```

> [!NOTE]
> 如果您使用繫結來升級執行個體中的 R 元件，可以變更執行個體文件庫的路徑。 請務必確認 SQL Server 正在使用哪一個程式庫。

## <a name="r-packages-installed-with-sql-server"></a>與 SQL Server 一起安裝的 R 封裝

根據預設 R**基底**已安裝的套件。 基底套件包含這類封裝所提供的核心功能`stats`和`utils`。

安裝 SQL Server 2016 中 SQL Server 2017 R 永遠包含**RevoScaleR**封裝，相關的增強的封裝和提供者，可支援遠端計算內容資料流中，平行執行 rx 函式，並許多其他功能。 若要升級的 RevoScaleR 封裝，請使用繫結來升級機器學習服務元件，或修補或升級至較新版的 SQL Server 執行個體。

+ 如需增強的 R 功能的概觀，請參閱[需機器學習伺服器](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ 若要下載到用戶端電腦上的 RevoScaleR 程式庫，安裝[Microsoft R 用戶端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>安裝 R 封裝所需的權限

在 SQL Server 2016 中，系統管理員必須安裝新的 R 封裝的執行個體層級為基礎。 

SQL Server 2017 導入套件安裝和管理新的功能：

+ 您可以使用 R 命令從遠端用戶端安裝套件使用私用或共用的範圍。 這項功能需要[Microsoft R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install)或[Server 機器學習](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，以及執行個體上的 dbo 權限。
+ 新資料庫已加入功能以支援套件管理資料庫管理員而不需要使用 T-SQL。 在未來，這些功能會提供 Dba 的能力委派的權限的使用者進行封裝管理大部分 facet。

本節描述安裝及管理每個版本的封裝時所需的權限。

+ SQL Server 2016 R 服務 （資料庫）

    若要執行的電腦上安裝新的 R 封裝[!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)]，您必須擁有電腦的系統管理權限。 它是資料庫管理員或其他伺服器上的系統管理員，以確保上已安裝的所有必要的封裝工作[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]執行個體。

    如果您沒有系統管理權限的電腦上裝載[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]執行個體，您可以提供給系統管理員資訊有關如何安裝 R 封裝，並提供存取至安全的封裝儲存機制，封裝所要求的使用者可以取得。

+ SQL Server 2017 Machine Learning 服務

    如果您是在 SQL Server 執行個體上的系統管理員，您可以安裝在新的封裝。 只是一定要使用的執行個體相關聯的預設文件庫。 從預存程序呼叫時，無法執行封裝安裝到其他位置。 使用 SQL Server 計算內容也需要執行個體文件庫中的封裝可供執行任何 R 程式碼。

    此版本也包含一些新功能，目的是要支援更容易進行封裝管理 Dba 的下一個版本。 現在，我們建議您繼續安裝執行個體層級為基礎的 R 封裝。

+ R Server (Standalone)

    您需要系統管理權限才能安裝新的 R 封裝的電腦。

+ 其他用戶端的環境

    如果您正作為 R 工作站的電腦上安裝新的 R 封裝，而且該電腦**不**擁有執行個體[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]安裝，您仍然需要電腦的系統管理權限安裝封裝。 安裝封裝之後，您就可以在本機執行封裝。

## <a name="managing-or-viewing-installed-packages"></a>管理或檢視已安裝封裝

有多種方法，您可以取得目前安裝的套件的完整清單。 如需詳細資訊，請參閱[判斷 SQL Server 上已安裝哪些封裝](determine-which-packages-are-installed-on-sql-server.md)。
