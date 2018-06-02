---
title: 在 SQL Server 機器學習和 R 服務的 R 指令碼錯誤 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0b695111849b234f6ca38fc89c538e905f187fb6
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "34709097"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server 中的 R 指令碼錯誤
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文記載數個 scriptin gerrors 在 SQL Server 中執行 R 程式碼時。 清單不完整。 有許多的封裝，而且錯誤可以區分相同封裝的版本之間。 我們建議上發佈指令碼錯誤[機器學習 Server 論壇](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)，可支援機器學習中 R 服務 （資料庫）、 Microsoft R 用戶端，與 Microsoft R Server 使用的元件。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>有效的指令碼失敗 T-SQL 中或預存程序

包裝之前 R 程式碼中的預存程序，最好在外部的 IDE，或其中一種 R 工具，例如 RTerm 或 RGui 執行 R 程式碼。 藉由使用這些方法，您可以測試和偵錯的程式藉由使用 r 會傳回詳細的錯誤訊息

不過，有時可完全外部 IDE 或公用程式中的程式碼可能無法在預存程序中執行，或在 SQL Server 計算內容。 如果發生這種情況，有各種問題之前，您可以假設封裝未搭配 SQL Server 中尋找。

1. 請檢查是否正在執行 [啟動列]。

2. 檢視訊息的輸入的資料或輸出資料是否包含具有不相容或不受支援的資料類型資料行。 例如，SQL database 的查詢通常會傳回 Guid 或 rowguids 的資料，都不支援。 如需詳細資訊，請參閱[R 程式庫和資料型別](r/r-libraries-and-data-types.md)。

3. 檢閱個別的 R 函數來判斷是否所有參數是否都支援 SQL Server 計算內容的 [說明] 頁。 ScaleR 的說明，請使用內嵌 R 說明命令，或參閱[封裝參考](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

如果 R 執行階段正常運作，但您的指令碼會傳回錯誤，我們建議您嘗試偵錯專用的 R 開發環境，例如 R Tools for Visual Studio 中的指令碼。

我們也建議您檢閱，並可稍微重寫指令碼來更正 R 和 database engine 之間移動資料時可能發生的資料類型的任何問題。 如需詳細資訊，請參閱[R 程式庫和資料型別](r/r-libraries-and-data-types.md)。

此外，您可以使用 sqlrutils 封裝來封裝您的 R 指令碼是做為預存程序更方便取用的格式。 如需詳細資訊，請參閱：
* [使用 sqlrutils 封裝產生 R 程式碼的預存程序](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
* [使用 sqlrutils 建立預存程序](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>指令碼會傳回不一致的結果

R 指令碼可以在 SQL Server 內容中，傳回不同值有數種原因：

- SQL Server 與 r 之間傳遞資料時，某些資料類型上, 自動執行隱含類型轉換如需詳細資訊，請參閱[R 程式庫和資料型別](r/r-libraries-and-data-types.md)。

- 判斷是否位元是一項因素。 例如，通常在很 32 位元和 64 位元的浮動點 libraries 的數學運算的結果中的差異。

- 決定是否在任何作業中產生 Nan。 這會使失效的結果。

- 擷取對等的近於零的數字時，可以幅度加大小差異。

- 累積的捨入錯誤，可能會造成這類事件時小於零時，而非零的值。

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>透過 ODBC 的遠端執行的隱含的驗證

如果您連接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]命令所使用的電腦來執行 R **RevoScaleR**函式，當您使用 ODBC 呼叫，將資料寫入到伺服器時，可能會發生錯誤。 只有當您使用 Windows 驗證時，就會發生此錯誤。

原因是針對 R 服務所建立的背景工作帳戶沒有權限可以連線到伺服器。 因此，無法代表您執行 ODBC 呼叫。 問題不會發生的 SQL 登入，因為具有 SQL 登入，認證會明確地從 R 用戶端至 ODBC SQL Server 執行個體，然後。 不過，使用 SQL 登入是安全性方面不如使用 Windows 驗證。

若要啟用您的 Windows 認證安全地傳遞已啟動遠端電腦上，SQL Server 指令碼必須模擬您的認證。 此程序稱為_隱含的驗證_。 若要這麼做，SQL Server 電腦執行 R 或 Python 指令碼的背景工作帳戶必須正確的權限。

1. 開啟[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]為您要執行 R 程式碼的執行個體的系統管理員。

2. 執行下列指令碼。 請務必編輯使用者群組名稱，如果您變更預設值，與電腦和執行個體名稱。

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>避免您在 SQL 計算內容中執行 R 時清除工作區

雖然您使用 R 主控台時，清除工作區是常見的它可以包含非預期的結果，在 SQL 計算內容。

`revoScriptConnection` 為包含從 SQL Server 呼叫 R 工作階段的相關資訊的 R 工作區中的物件。 不過，如果您的 R 程式碼會包含命令以清除工作區 (例如`rm(list=ls())`)，以及清除工作階段和 R 工作空間中的其他物件的所有資訊。

因應措施，避免任意清除變數和其他物件，您在 SQL Server 中執行 R 時。 您可以使用，以刪除特定變數**移除**函式：

```R
remove('name1', 'name2', ...)
```

如果有多個要刪除的變數，我們建議您將暫存變數的名稱儲存到清單，並在清單上執行定期記憶體回收。



## <a name="next-steps"></a>後續的步驟

[機器學習服務疑難排解和已知的問題](machine-learning-troubleshooting-faq.md)

[如需疑難排解機器學習的資料收集](data-collection-ml-troubleshooting-process.md)

[升級及安裝常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)

[疑難排解 database engine 連接](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
