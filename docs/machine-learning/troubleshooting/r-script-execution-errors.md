---
title: 常見的 R 指令碼錯誤
description: 本文說明在 SQL Server 中執行 R 程式碼時可能會遇到的幾個常見指令碼錯誤。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 05/31/2018
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ebcedf2adc48fad6668b30d9c34d21b7557879dc
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87253665"
---
# <a name="common-r-scripting-errors-in-sql-server"></a>SQL Server 中常見的 R 指令碼錯誤
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

本文說明在 SQL Server 中執行 R 程式碼時遇到的幾個常見指令碼錯誤。 這份清單並不是完整清單。 因為有很多套件，所以相同套件的各個版本之間可能會有不同錯誤。

如果遇到此處未涵蓋的指令碼錯誤，請將其張貼在 [Machine Learning Server 論壇](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR) 上。 此論壇支援用於各種 SQL 機器學習產品的機器學習元件。

## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>有效的指令碼在 T-SQL 或預存程序中失敗

在預存程序中包裝 R 程式碼之前，最好先在外部 IDE 或其中一個 R 工具 (例如 RTerm 或 Rgui.exe) 中執行 R 程式碼。 藉由使用這些方法，您就可以使用 R 傳回的詳細錯誤訊息來測試和偵錯工具代碼。

不過，有時候在外部 IDE 或公用程式中完美運作的程式碼，可能無法在預存程序或 SQL Server 計算內容中執行。 如果發生這種情況，在您可以假設封裝無法在 SQL Server 中運作 之前，需要尋找各種問題。

1. 查看 Launchpad 主機是否在執行中。

2. 檢閱訊息以查看輸入資料或輸出資料是否包含具有不相容或不受支援資料類型的資料行。 例如，SQL 資料庫上的查詢通常會傳回都不支援的 GUID 或 RowGUID。 如需詳細資訊，請參閱 [R 程式庫和資料類型](../r/r-libraries-and-data-types.md)。

3. 請檢閱個別 R 函式的說明頁面，以判斷 SQL Server 計算內容是否支援所有參數。 如需 ScaleR 說明，請使用內嵌 R 說明命令，或參閱[套件參考](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

如果 R 執行階段正常運作，但您的指令碼傳回錯誤，建議您嘗試在專用的 R 開發環境 (例如 Visual Studio R 工具) 中嘗試對指令碼偵錯。

我們也建議您檢查並稍微重寫指令碼，以更正在 R 和資料庫引擎之間移動資料時，可能會引發的任何資料類型問題。 如需詳細資訊，請參閱 [R 程式庫和資料類型](../r/r-libraries-and-data-types.md)。

此外，您可以使用 sqlrutils 封裝，以比較容易作為預存程序取用的格式來與您的 R 指令碼組合使用。 如需詳細資訊，請參閱
* [sqlrutils 封裝](../r/ref-r-sqlrutils.md)
* [使用 sqlrutils 建立預存程序](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>指令碼傳回不一致的結果

R 指令碼可能會在 SQL Server 內容中傳回不同的值，原因如下：

- 在 SQL Server 和 R 之間傳遞資料時，會在某些資料類型上自動執行隱含類型轉換。如需詳細資訊，請參閱 [R 程式庫和資料類型](../r/r-libraries-and-data-types.md)。

- 判斷位元是否是因數。 例如，32 位元和 64 位元浮點程式庫的數學運算結果中通常會有一些差異。

- 判斷在任何作業中是否產生 NaNs。 這可能會使結果失效。

- 當您採用接近零的倒數時，可能會將小差異放大。

- 累積的舍入錯誤可能會導致小於零的值，而不是零。

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>透過 ODBC 進行遠端執行的隱含驗證

如果您連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦以使用 **RevoScaleR** 函式來執行 R 命令，可能會在使用將資料寫入伺服器的 ODBC 呼叫時發生錯誤。 只有當您使用 Windows 驗證時，才會發生此錯誤。

原因是針對 R 服務所建立的工作者帳戶沒有連線伺服器的許可權。 因此，ODBC 呼叫可能無法代表您執行。 SQL 登入不會發生此問題，因為在 SQL 登入中，認證會明確地從 R 用戶端傳遞至 SQL Server 執行個體，然後傳送至 ODBC。 不過，使用 SQL 登入的安全性也低於使用 Windows 驗證。

若要讓您的 Windows 認證從自遠端起始的指令碼安全地傳遞，SQL Server 就必須模擬您的認證。 此處理程序稱為「相互驗證」。 若要完成此工作，在 SQL Server 電腦上執行 R 或 Python 指令碼的工作者帳戶必須具備正確的許可權。

1. 在您想要執行 R 程式碼的執行個體上，將 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 開啟為系統管理員。

2. 執行下列指令碼。 如果已變更預設值，以及電腦和執行個體名稱，請務必編輯使用者群組名稱。

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>當您在 SQL 計算內容中執行 R 時，請避免清除工作區

雖然在 R 主控台內工作時清除工作區很常見，但它可能在 SQL 計算內容中造成意想不到的結果。

`revoScriptConnection` 是 R 工作區的物件，包含從 SQL Server 呼叫的 R 工作階段的相關資訊。 不過，如果 R 程式碼包含清除工作區的命令 (例如 `rm(list=ls())`)，也會清除 R 工作區中和工作階段與其他物件有關的所有資訊。

因應措施是，避免在 SQL Server 中執行 R 時任意清除變數和其他物件。 您可以使用 **remove** 函式刪除特定變數：

```R
remove('name1', 'name2', ...)
```

如有多個變數要刪除，建議您請將暫存變數名稱儲存至清單，然後在清單上執行定期記憶體回收。



## <a name="next-steps"></a>後續步驟

[機器學習服務疑難排解和已知問題](machine-learning-troubleshooting-overview.md)

[用於針對機器學習進行疑難排解所收集的資料](data-collection-ml-troubleshooting-process.md)

[升級及安裝常見問題集](upgrade-and-installation-faq-sql-server-r-services.md)

[針對資料引擎連線進行疑難排解](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
