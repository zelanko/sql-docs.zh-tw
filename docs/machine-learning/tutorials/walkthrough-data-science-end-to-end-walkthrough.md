---
title: R 教學課程：SQL 中的開發模型
description: 了解如何根據 SQL Server 2016 或 SQL Server 2017 中的 R 功能支援，建置預測性模型的端對端解決方案。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/11/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cc423acd1e8c703b5890984df556b65f46cf5d4a
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179745"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>教學課程：適用 R 資料科學家的 SQL 開發
[!INCLUDE [SQL Server 2016](../../includes/applies-to-version/sqlserver2016.md)]

在這個適用資料科學家的教學課程中，瞭解如何根據 SQL Server 2016 或 SQL Server 2017 中的 R 功能支援，建置預測性模型的端對端解決方案。 本教學課程使用 SQL Server 上的 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 資料庫。 

您將組合使用 R 程式碼、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料和自訂 SQL 函數來建立分類模型，以表示計程車司機在特定車程時獲得小費的機率。 您也會將 R 模型部署至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並使用伺服器資料以根據模型來產生分數。

此範例可以擴充至所有類型的真實生活問題，例如預測銷售活動的客戶回應，或預測對事件的花費或出席情況。 因為可以從預存程序叫用模型，所以您可以輕鬆地將它內嵌在應用程式中。

由於此逐步解說是針對 R 開發人員介紹 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 所設計，因此會儘量使用 R。 不過，這並不代表 R 一定是每項工作的最適用工具。 在許多情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以提供較佳效能，尤其是資料彙總和功能工程這類工作。  這類工作特別受益於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的新功能 (例如記憶體最佳化資料行存放區索引 )。 我們將在過程中嘗試指出可能的最佳化做法。

## <a name="prerequisites"></a>Prerequisites

+ [R 整合的 SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md#verify-installation)或 [SQL Server 2016 R 服務](../install/sql-r-services-windows-install.md)

+ [資料庫權限](../security/user-permission.md) 和 SQL Server 資料庫使用者登入

+ [Transact-SQL](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [紐約市計程車示範資料庫](demo-data-nyctaxi-in-sql.md)

+ R IDE，例如 RStudio 或 R 包含的內建 RGUI.EXE 工具

我們建議您在用戶端工作站上執行此逐步解說。 您必須能夠連接到相同網路上已啟用 SQL Server 和 R 語言的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。 如需工作站設定的指示，請參閱 [設定 R 開發的資料科學用戶端](../r/set-up-a-data-science-client.md)。

或者，您也可以在同時具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 開發環境的電腦上執行逐步解說，但我們不建議在生產環境中使用此設定。 如果您需要將用戶端和伺服器放在同一部電腦上，請務必安裝第二組 Microsoft R 程式庫，以便從「遠端」用戶端傳送 R 指令碼。 請勿使用在 SQL Server 執行個體的程式檔案中安裝的 R 程式庫。 尤其是，如果您使用一台電腦，則在這兩個位置都需要 RevoScaleR 程式庫，以便支援用戶端和伺服器作業。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

> [!NOTE]
> 如果您使用 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/) 或 [資料科學虛擬機器](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/)，而不是 R 用戶端，則 RevoScaleR 的路徑是 C:\Program Files\Microsoft\ML Server\R_SERVER\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>其他 R 套件

這個逐步解說需要一些預設不會安裝為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 一部份的 R 程式庫。 您必須將套件安裝在您要開發解決方案的用戶端上，以及您要部署解決方案的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上。

### <a name="on-a-client-workstation"></a>在用戶端工作站上

在您的 R 環境中，複製下列幾行，然後在主控台視窗 (Rgui.exe 或 IDE) 中執行程式碼。 有些套件也會安裝必要的套件。 總共安裝大約 32 個套件。 您必須連接網際網路，才能完成此步驟。
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>在伺服器上

在 SQL Server 上安裝套件有幾個選項。 例如，SQL Server 提供 [R 套件管理](../package-management/install-additional-r-packages-on-sql-server.md)功能，可供資料庫管理員建立套件存放庫，並將安裝自己套件的權限指派給使用者。 不過，如果您是電腦上的系統管理員，只要安裝到正確的程式庫，您就可以使用 R 安裝新的套件。

> [!NOTE]
> 在伺服器上，即使出現提示，也**不要**安裝至使用者程式庫。 如果您安裝至使用者程式庫，SQL Server 執行個體會找不到或無法執行套件。 如需詳細資訊，請參閱[在 SQL Server 上安裝新的 R 套件](../package-management/install-additional-r-packages-on-sql-server.md)。

1. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上，**以系統管理員身分**開啟 RGui.exe。  如果您已使用預設值來安裝 SQL Server R Services，則可以在 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64 中找到 Rgui.exe。

2. 在 R 提示字元中，執行下列 R 命令：
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  這個範例會使用 R grep 函數來搜尋可用路徑的向量，並尋找包含 "Program Files" 的路徑。 如需詳細資訊，請參閱 [https://www.rdocumentation.org/packages/base/functions/grep](https://www.rdocumentation.org/packages/base/functions/grep)。

  如果您認為已經安裝套件，請執行 `installed.packages()` 檢查已安裝的套件清單。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [探索和摘要資料](walkthrough-view-and-summarize-data-using-r.md)
