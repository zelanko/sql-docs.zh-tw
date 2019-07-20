---
title: R 腳本錯誤和疑難排解
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 83029a9727a26c647d78c49501fde08f72d7694d
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343399"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server 中的 R 腳本錯誤
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文記載在 SQL Server 中執行 R 程式碼時的數個 .scriptin gerrors。 清單並不完整。 有許多套件, 而錯誤在相同套件的版本之間可能有所不同。 我們建議您在[Machine Learning Server 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR)上張貼腳本錯誤, 其支援 R Services (資料庫內)、Microsoft R Client 和 Microsoft r Server 中使用的機器學習元件。

**適用於：** SQL Server 2016 R Services, SQL Server 2017 Machine Learning 服務


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>T-sql 或預存程式中的有效腳本失敗

在預存程式中包裝 R 程式碼之前, 最好先在外部 IDE 或其中一個 R 工具 (例如 RTerm 或 Rgui.exe) 中執行 R 程式碼。 藉由使用這些方法, 您可以使用 R 傳回的詳細錯誤訊息來測試和偵錯工具代碼。

不過, 有時候在外部 IDE 或公用程式中完美運作的程式碼, 可能無法在預存程式或 SQL Server 計算內容中執行。 如果發生這種情況, 您可以先尋找各種問題, 然後再假設封裝無法在 SQL Server 中運作。

1. 查看啟動列是否正在執行。

2. 檢查訊息, 以查看輸入資料或輸出資料是否包含具有不相容或不受支援資料類型的資料行。 例如, SQL database 上的查詢通常會傳回 Guid 或 RowGUIDs, 這兩者都不受支援。 如需詳細資訊, 請參閱[R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

3. 請參閱個別 R 函數的說明頁面, 以判斷 SQL Server 計算內容是否支援所有參數。 如需 ScaleR 說明, 請使用內嵌 R help 命令, 或參閱[封裝參考](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

如果 R 執行時間正常運作, 但您的腳本傳回錯誤, 我們建議您嘗試在專用的 R 開發環境 (例如 Visual Studio R 工具) 中進行腳本的偵錯工具。

我們也建議您檢查並稍微重寫腳本, 以更正當您在 R 和 database engine 之間移動資料時可能會發生的任何資料類型問題。 如需詳細資訊, 請參閱[R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

此外, 您可以使用 sqlrutils 套件, 以較容易當做預存程式取用的格式來組合您的 R 腳本。 如需詳細資訊，請參閱：
* [sqlrutils 套件](r/ref-r-sqlrutils.md)
* [使用 sqlrutils 建立預存程式](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>腳本傳回不一致的結果

R 腳本可能會在 SQL Server 內容中傳回不同的值, 原因有好幾種:

- 在 SQL Server 和 R 之間傳遞資料時, 會在某些資料類型上自動執行隱含類型轉換。如需詳細資訊, 請參閱[R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

- 判斷位是否為因素。 例如, 32 位和64位浮點程式庫的數學運算結果通常會有差異。

- 判斷是否在任何作業中產生 Nan。 這可能會使結果失效。

- 當您採用接近零的數位時, 可能會放大小差異。

- 累積的舍入錯誤可能會導致小於零的值, 而不是零。

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>透過 ODBC 進行遠端執行的隱含驗證

如果您使用**RevoScaleR**函數[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]連接到電腦來執行 R 命令, 當您使用將資料寫入伺服器的 ODBC 呼叫時, 可能會收到錯誤。 只有當您使用 Windows 驗證時, 才會發生此錯誤。

原因是針對 R 服務所建立的工作者帳戶沒有連接到伺服器的許可權。 因此, 無法代表您執行 ODBC 呼叫。 SQL 登入不會發生此問題, 因為在 SQL 登入中, 認證會明確地從 R 用戶端傳遞至 SQL Server 實例, 然後傳送至 ODBC。 不過, 使用 SQL 登入的安全性也不如使用 Windows 驗證。

若要讓您的 Windows 認證從遠端起始的腳本安全地傳遞, SQL Server 必須模擬您的認證。 此程式稱為「_隱含驗證_」。 若要完成此工作, 在 SQL Server 電腦上執行 R 或 Python 腳本的工作者帳戶必須具備正確的許可權。

1. 在[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]您要執行 R 程式碼的實例上, 以系統管理員的身分開啟。

2. 執行下列指令碼。 如果您變更了預設值, 以及電腦和實例名稱, 請務必編輯使用者組名。

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>當您在 SQL 計算內容中執行 R 時, 避免清除工作區

雖然在 R 主控台中工作時, 清除工作區是常見的, 但在 SQL 計算內容中可能會產生非預期的結果。

`revoScriptConnection`是 R 工作區中的物件, 其中包含從 SQL Server 呼叫之 R 會話的相關資訊。 不過, 如果您的 R 程式碼包含清除工作區的命令 (例如`rm(list=ls())`), 則也會清除有關會話的所有資訊, 以及 R 工作區中的其他物件。

因應措施是在 SQL Server 中執行 R 時, 避免任意清除變數和其他物件。 您可以使用**remove**函式來刪除特定變數:

```R
remove('name1', 'name2', ...)
```

如果有多個要刪除的變數, 建議您將暫存變數的名稱儲存至清單, 然後在清單上執行定期垃圾收集。



## <a name="next-steps"></a>後續步驟

[Machine Learning Services 疑難排解和已知問題](machine-learning-troubleshooting-faq.md)

[用於疑難排解機器學習服務的資料收集](data-collection-ml-troubleshooting-process.md)

[升級及安裝常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)

[資料庫引擎連接疑難排解](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
