---
title: 在 SQL Server Machine Learning 及 R Services 的 R 指令碼錯誤 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 941a8bbc5e7326d87dcdba8c822fb2c3f2190900
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51695436"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server 中的 R 指令碼錯誤
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 SQL Server 中執行 R 程式碼時，這篇文章會說明數個 scriptin gerrors。 清單不完整。 有許多套件，而錯誤可能不同相同套件的版本。 我們建議您張貼的指令碼錯誤[Machine Learning Server 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR)，其支援的機器學習服務 R Services （資料庫內）、 Microsoft R Client，與 Microsoft R Server 所使用的元件。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 Machine Learning 服務


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>在 T-SQL 或預存程序中的有效的指令碼失敗

之前在預存程序中包裝 R 程式碼，它是個不錯的主意，若要執行 R 程式碼，在外部的 IDE 中，或其中一種 R 工具，例如 RTerm 或 RGui。 您可以藉由使用這些方法，測試和偵錯的程式碼，藉由使用由。 詳細的錯誤訊息

不過，有時候順暢執行外部的 IDE 或公用程式中的程式碼可能無法在預存程序中執行，或在 SQL Server 計算內容。 如果發生這種情況，有各種尋找之前您可以假設套件不適用於 SQL Server 的問題。

1. 請檢查是否正在執行 [啟動列]。

2. 檢視訊息的輸入的資料 」 或 「 輸出資料是否包含具有不相容或不受支援的資料類型資料行。 例如，在 SQL database 上的查詢通常會傳回 Guid 或 rowguids 的資料，這兩者都是不受支援。 如需詳細資訊，請參閱 < [R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

3. 檢閱個別的 R 函數來判斷是否所有參數是否都支援 SQL Server 計算內容的 [說明] 頁。 如需 ScaleR 的說明，請使用內嵌 R 說明命令，或參閱[套件參考](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

如果 R 執行階段正常運作，但您的指令碼會傳回錯誤，建議您試著偵錯專用的 R 開發環境，例如適用於 Visual Studio R 工具中的指令碼。

我們也建議您檢閱，並稍微重新撰寫指令碼以修正任何問題，R 和資料庫引擎之間移動資料時可能發生的資料類型。 如需詳細資訊，請參閱 < [R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

此外，您可以使用 sqlrutils 套件來封裝您的 R 指令碼是做為預存程序更方便取用的格式。 如需詳細資訊，請參閱：
* [使用 sqlrutils 套件以產生 R 程式碼的預存程序](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
* [使用 sqlrutils 建立預存程序](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>指令碼會傳回不一致的結果

R 指令碼可以在 SQL Server 內容中，傳回不同的值有幾個原因：

- SQL Server 和 r 之間傳遞資料時，在某些資料類型，自動執行隱含類型轉換如需詳細資訊，請參閱 < [R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

- 判斷位元是一項因素。 比方說，通常在很 32 位元和 64 位元浮點數的點程式庫的數學運算的結果中的差異。

- 決定是否在任何作業中產生 Nan。 這可以使其失效的結果。

- 當您幾乎為零的數字的倒數，可能會擴大小差異。

- 累積的捨入錯誤，可能會導致等項目都小於零而不是零的值。

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>透過 ODBC 的遠端執行的隱含的驗證

如果您連接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用的電腦來執行 R 命令**RevoScaleR**函式中，當您使用 ODBC 呼叫，將資料寫入至伺服器時，可能會發生錯誤。 只有在您使用 Windows 驗證時，才會發生這個錯誤。

原因是針對 R Services 所建立的背景工作帳戶沒有連接到伺服器的權限。 因此，無法代表您執行 ODBC 呼叫。 問題不會發生與 SQL 登入，因為具有 SQL 登入，認證會明確地從 R 用戶端到 SQL Server 執行個體，再到 ODBC。 不過，使用 SQL 登入也是安全性方面不如使用 Windows 驗證。

若要啟用您的 Windows 認證，來安全地傳遞已啟動遠端電腦上，SQL Server 指令碼必須模擬您的認證。 此程序，則稱為_隱含的驗證_。 若要這麼做，SQL Server 電腦執行 R 或 Python 指令碼的背景工作帳戶必須具有正確的權限。

1. 開啟[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]成為您要執行 R 程式碼的執行個體的系統管理員。

2. 執行下列指令碼。 請務必編輯使用者群組名稱，如果您變更預設值，以及電腦和執行個體名稱。

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>避免 SQL 計算內容中執行 R 時，清除工作區

雖然清除工作區是常見的當您使用 R 主控台，它可以有非預期的結果，在 SQL 計算內容。

`revoScriptConnection` 是包含稱為 「 從 SQL Server 的 R 工作階段的相關資訊的 R 工作區中的物件。 不過，如果您的 R 程式碼包含清除工作區的命令 (例如`rm(list=ls())`)，也會清除工作階段和 R 工作區中的其他物件的所有資訊。

SQL Server 中執行 R 時，因應措施，避免任意清除變數和其他物件。 您可以使用，以刪除特定的變數**移除**函式：

```R
remove('name1', 'name2', ...)
```

如果有多個要刪除的變數，我們建議您將儲存於暫存變數名稱的清單，然後再執行清單上的 定期記憶體回收。



## <a name="next-steps"></a>後續步驟

[機器學習服務疑難排解和已知的問題](machine-learning-troubleshooting-faq.md)

[疑難排解 機器學習服務的資料收集](data-collection-ml-troubleshooting-process.md)

[升級及安裝常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)

[疑難排解 database engine 連接](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
