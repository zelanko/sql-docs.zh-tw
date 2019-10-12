---
title: 使用 R 語言的資料科學家教學課程
description: 示範如何針對資料庫內分析建立端對端 R 解決方案的教學課程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/11/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ad7f5a500f740e4a302f814ec9523dfb33ecc68b
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278272"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>教學課程：適用于 R 資料科學家的 SQL 開發
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在適用于資料科學家的本教學課程中，瞭解如何根據 SQL Server 2016 或 SQL Server 2017 中的 R 功能支援，建立預測性模型的端對端解決方案。 本教學課程使用 SQL Server 上的[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)資料庫。 

您可以使用 R 程式碼、@no__t 0 資料和自訂 SQL 函式的組合來建立分類模型，以指出驅動程式可能會在特定計程車行程上取得秘訣的機率。 您也會將 R 模型部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並使用伺服器資料來根據模型產生分數。

這個範例可以延伸到所有類型的實際問題，例如預測銷售活動的客戶回應，或預測事件的支出或出席。 因為可以從預存程式叫用模型，所以您可以輕鬆地將它內嵌在應用程式中。

因為本逐步解說的設計是要向 R 開發人員介紹 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，所以會盡可能使用 R。 不過，這並不表示 R 一定是每個工作的最佳工具。 在許多情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以提供較佳效能，尤其是資料彙總和功能工程這類工作。  這類工作特別受益於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的新功能 (例如記憶體最佳化資料行存放區索引 )。 我們嘗試在過程中指出可能的優化。

## <a name="prerequisites"></a>必要條件

+ [使用 r 整合 SQL Server Machine Learning 服務，](../install/sql-machine-learning-services-windows-install.md#verify-installation)或[SQL Server 2016 R 服務](../install/sql-r-services-windows-install.md)

+ [資料庫許可權](../security/user-permission.md)和 SQL Server 資料庫使用者登入

+ [Transact-SQL](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [NYC 計程車示範資料庫](demo-data-nyctaxi-in-sql.md)

+ R IDE，例如 RStudio 或包含在 R 中的內建 RGUI.EXE 工具

我們建議您在用戶端工作站上執行此逐步解說。 您必須能夠在相同網路上連接到已啟用 SQL Server 和 R 語言的 @no__t 0 電腦。 如需工作站設定的指示，請參閱[設定適用于 R 開發的資料科學用戶端](../r/set-up-a-data-science-client.md)。

或者，您也可以在同時具有 @no__t 0 和 R 開發環境的電腦上執行逐步解說，但我們不建議在生產環境中使用此設定。 如果您需要將用戶端和伺服器放在同一部電腦上，請務必安裝第二組 Microsoft R 程式庫，以便從「遠端」用戶端傳送 R 腳本。 請勿使用安裝在 SQL Server 實例之程式檔案中的 R 程式庫。 具體而言，如果您使用一部電腦，則在這兩個位置都需要 RevoScaleR 程式庫，以支援用戶端和伺服器作業。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

> [!NOTE]
> 如果您使用[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)或[資料科學虛擬機器](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/)，而不是 R 用戶端，則 RevoScaleR 的路徑為 C:\Program Files\Microsoft\ML Server\R_SERVER\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>其他 R 套件

此逐步解說需要數個預設不會安裝為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 一部分的 R 程式庫。 您必須在開發解決方案的用戶端，以及部署解決方案的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上安裝套件。

### <a name="on-a-client-workstation"></a>在用戶端工作站上

在您的 R 環境中，複製下列幾行，然後在主控台視窗（Rgui.exe 或 IDE）中執行程式碼。 某些套件也會安裝必要的套件。 在 [全部] 中，會安裝大約32套件。 您必須具有網際網路連線，才能完成此步驟。
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>在伺服器上

您有數個選項可以在 SQL Server 上安裝套件。 例如，SQL Server 提供[R 封裝管理](../r/install-additional-r-packages-on-sql-server.md)功能，可讓資料庫管理員建立封裝存放庫，並將安裝自己套件的許可權指派給使用者。 不過，如果您是電腦上的系統管理員，只要安裝到正確的程式庫，您就可以使用 R 安裝新的套件。

> [!NOTE]
> 在伺服器上，即使出現提示，**也不要安裝**到使用者程式庫。 如果您將安裝至使用者程式庫，SQL Server 實例就找不到或無法執行封裝。 如需詳細資訊，請參閱[在 SQL Server 上安裝新的 R 套件](../r/install-additional-r-packages-on-sql-server.md)。

1. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上，**以系統管理員身分**開啟 RGui.exe。  如果您已使用預設值安裝 SQL Server R Services，您可以在 C:\Program Files\Microsoft SQL Server\MSSQL13. 中找到 Rgui.exe。MSSQLSERVER\R_SERVICES\bin\x64).

2. 在 R 提示字元中，執行下列 R 命令：
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  這個範例會使用 R grep 函數來搜尋可用路徑的向量，並尋找包含 "Program Files" 的路徑。 如需詳細資訊，請參閱[https://www.rdocumentation.org/packages/base/functions/grep](https://www.rdocumentation.org/packages/base/functions/grep)。

  如果您認為已經安裝封裝，請執行 `installed.packages()` 來檢查已安裝的套件清單。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [探索和摘要資料](walkthrough-view-and-summarize-data-using-r.md)
