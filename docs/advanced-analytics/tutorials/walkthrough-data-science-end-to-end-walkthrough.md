---
title: 適用於資料科學家使用 R 語言-SQL Server 機器學習的教學課程
description: 本教學課程示範如何建立在資料庫內分析的端對端 R 解決方案。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4b3beca0f9e9a8c714e60bde7a2e7ff067e2265e
ms.sourcegitcommit: 2e8783e6bedd9597207180941be978f65c2c2a2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2019
ms.locfileid: "54405728"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>教學課程：適用於 R 的資料科學家的 SQL 開發
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本教學課程適用於資料科學家，了解如何建置預測模型，根據 SQL Server 2016 或 SQL Server 2017 中的 R 功能支援的端對端解決方案。 本教學課程會使用[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)上 SQL Server 資料庫。 

您使用 R 程式碼、 組合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料和自訂 SQL 函數，來建立分類模型，以表示驅動程式可能會收到特定的計程車車程的小費的機率。 您也可以部署您的 R 模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並使用伺服器資料來產生以模型為基礎的分數。

此範例可以延伸至所有類型的實際問題，例如預測銷售活動，客戶回應，或預測的花費，或在活動的出席人數。 因為模型可以叫用預存程序，可以輕鬆地將它內嵌在應用程式。

因為本逐步解說旨在介紹 R 開發人員[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，可能的話，會使用 R。 不過，這不表示 R 一定是每個工作的最佳工具。 在許多情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以提供較佳效能，尤其是資料彙總和功能工程這類工作。  這類工作特別受益於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的新功能 (例如記憶體最佳化資料行存放區索引 )。 我們嘗試點出可能的最佳化過程。

## <a name="prerequisites"></a>先決條件

+ [SQL Server 2017 Machine Learning 服務與 R 整合](../install/sql-machine-learning-services-windows-install.md#verify-installation)或[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

+ [資料庫權限](../security/user-permission.md)和 SQL Server 資料庫使用者登入

+ [Transact-SQL](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [NYC 計程車示範資料庫](demo-data-nyctaxi-in-sql.md)

+ R IDE，例如 RStudio 或內建的 RGUI 工具隨附於 R

我們建議您此逐步解說中的用戶端工作站上。 您必須能夠連接，在相同的網路，到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟用的 R 語言與 SQL Server 的電腦。 如需有關工作站組態的指示，請參閱[設定適用於 R 開發的資料科學用戶端](../r/set-up-a-data-science-client.md)。

或者，您可以同時具有的電腦上執行本逐步解說[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 R 開發環境，但我們不建議此組態的實際執行環境。 如果您需要將用戶端和伺服器放在同一部電腦上，請務必安裝適用於從 「 遠端 」 的用戶端傳送 R 指令碼的 Microsoft R 程式庫的第二組。 請勿使用安裝程式檔案的 SQL Server 執行個體中的 R 程式庫。 具體來說，如果您使用一部電腦，您會需要 RevoScaleR 程式庫中的這些位置，以支援用戶端和伺服器作業。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>其他 R 套件

本逐步解說需要未預設安裝一部分的多個 R 程式庫[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 您開發方案，以及在上，您必須在用戶端上安裝這兩個套件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您用來部署解決方案的電腦。

### <a name="on-a-client-workstation"></a>用戶端工作站

在 R 環境中，將下列幾行複製，並在主控台視窗 （Rgui 或 IDE） 中執行程式碼。 有些套件也會安裝必要的套件。 總共大約 32 個套件會安裝。 您必須具有網際網路連線，才能完成此步驟。
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>在伺服器上

您有幾個選項在 SQL Server 上安裝套件。 例如，SQL Server 提供[R 套件管理](../r/install-additional-r-packages-on-sql-server.md)功能，可讓資料庫管理員建立套件存放庫，並將使用者指派的權限安裝自己的封裝。 不過，如果您是電腦的系統管理員，您可以在安裝新的套件使用 R，只要您將安裝到正確的程式庫。

> [!NOTE]
> 在伺服器上，**沒有**安裝到使用者程式庫，即使出現提示。 如果您安裝到使用者程式庫時，SQL Server 執行個體找不到或執行封裝。 如需詳細資訊，請參閱 < [SQL Server 上安裝新的 R 套件](../r/install-additional-r-packages-on-sql-server.md)。

1. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上，**以系統管理員身分**開啟 RGui.exe。  如果您已安裝 SQL Server R Services 使用的預設值，可以在 C:\Program Files\Microsoft SQL Server\MSSQL13 找到 Rgui.exe。MSSQLSERVER\R_SERVICES\bin\x64)。

2. 在 R 提示字元中，執行下列 R 命令：
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  此範例會使用 R grep 函數來搜尋可用路徑的向量，並尋找包含"Program Files"路徑。 如需詳細資訊，請參閱 < [ https://www.rdocumentation.org/packages/base/functions/grep ](https://www.rdocumentation.org/packages/base/functions/grep)。

  如果您認為已經安裝的套件，來檢查已安裝的封裝清單執行`installed.packages()`。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [瀏覽和彙總的資料](walkthrough-view-and-summarize-data-using-r.md)