---
title: R 和 SQL Server 的端對端資料科學逐步解說 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d4f38fd424c881392d48b0a6a24feb7f7e27ee0
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086500"
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>R 和 SQL Server 的端對端資料科學逐步解說
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本逐步解說中，您要開發 R 功能支援在 SQL Server 2016 或 SQL Server 2017 為基礎的預測模型的端對端解決方案。

本逐步解說是根據一組常用的公用資料，即紐約市計程車資料集。 您使用 R 程式碼、 組合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料和自訂 SQL 函數，來建立分類模型，以表示驅動程式可能會收到特定的計程車車程的小費的機率。 您也可以部署您的 R 模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並使用伺服器資料來產生以模型為基礎的分數。

此範例可以延伸至所有類型的實際問題，例如預測銷售活動，客戶回應，或預測的花費，或在活動的出席人數。 因為模型可以叫用預存程序，可以輕鬆地將它內嵌在應用程式。

因為本逐步解說旨在介紹 R 開發人員[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，可能的話，會使用 R。 不過，這不表示 R 一定是每個工作的最佳工具。 在許多情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以提供較佳效能，尤其是資料彙總和功能工程這類工作。  這類工作特別受益於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的新功能 (例如記憶體最佳化資料行存放區索引 )。 我們嘗試點出可能的最佳化過程。

## <a name="target-audience"></a>目標對象

本逐步解說適用於 R 或 SQL 開發人員。 它介紹如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 將 R 整合至企業工作流程。  您應該熟悉資料庫作業，例如建立資料庫和資料表、 匯入資料，以及執行查詢。

+ 包含的所有 SQL 和 R 指令碼。
+ 您可能需要修改指令碼，在您的環境中執行中的字串。 您可以使用任何程式碼編輯器中，這類[Visual Studio Code](https://code.visualstudio.com/Download)。

## <a name="prerequisites"></a>先決條件

我們建議您本逐步解說在膝上型電腦或另一台電腦已安裝的 Microsoft R 程式庫。 您必須能夠連接，在相同的網路，到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟用的 R 語言與 SQL Server 的電腦。

您可以同時具有的電腦上執行本逐步解說[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 R 開發環境，但我們不建議此組態的實際執行環境。

如果您想要從遠端電腦，例如膝上型電腦或其他網路的電腦上執行 R 命令，您必須安裝 Microsoft R Open 程式庫。 您可以安裝 Microsoft R Client 或 Microsoft R Server。 在遠端電腦必須能夠連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。

如果您需要將用戶端和伺服器放在同一部電腦上，請務必安裝一組個別的 Microsoft R 程式庫，用於從 「 遠端 」 的用戶端傳送 R 指令碼。 請勿使用已安裝的 R 程式庫使用 SQL Server 執行個體所針對此目的。

## <a name="add-r-to-sql-server"></a>將 R 新增至 SQL Server

您必須安裝 R 支援的 SQL Server 執行個體的存取。 本逐步解說原先已針對 SQL erver 2016 開發和測試在 2017 年，因此您應該能夠使用其中一個下列的 SQL Server 版本。 （有一些小差異 RevoScaleR 函式中的不同版本之間。）

+ [安裝 SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)
+ [安裝 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。

## <a name="install-an-r-development-environment"></a>安裝 R 開發環境

此逐步解說中，我們建議您使用 R 開發環境。 以下是一些建議：

- **適用於 Visual Studio R 工具**(RTVS) 是免費的外掛程式提供 Intellisense、 偵錯，以及 Microsoft。 您可以使用它搭配 R Server 與 SQL Server Machine Learning 服務的支援。 若要下載，請參閱 [適用於 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)。

- **Microsoft R Client**是輕量級開發工具，支援 R 中使用 RevoScaleR 封裝以進行開發。 若要取得它，請參閱 [開始使用 Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)。

- **RStudio** 是其中一個比較常見的 R 開發環境。 如需詳細資訊，請參閱 < [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/)。

    您無法完成此教學課程使用一般安裝的 RStudio 或其他環境中;您也必須安裝 R 封裝和連線程式庫的 Microsoft R Open。 如需詳細資訊，請參閱 [Set Up a Data Science Client](../r/set-up-a-data-science-client.md)(設定資料科學用戶端)。

- 當您安裝 R 在 SQL Server 或 R 用戶端時，預設也會安裝基本的 R 工具 (R.exe、 RTerm.exe、 RScripts.exe)。 如果您不想安裝 IDE，您可以使用這些工具。

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>取得 SQL Server 執行個體和資料庫上的權限

若要連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行指令碼，並上傳資料，您必須具有有效的登入的資料庫伺服器上。  您可以使用 SQL 登入或整合式 Windows 驗證。 詢問資料庫管理員來設定，您可以使用： 資料庫中的下列權限的帳戶

- 建立資料庫、資料表、函數和預存程序
- 將資料寫入至資料表
- 若要執行 R 指令碼的能力 (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

此逐步解說中，我們使用了 SQL 登入**RTestUser**。 我們通常建議使用 Windows 整合式的驗證，但使用 SQL 登入是供某些示範更簡單。

## <a name="next-steps"></a>後續步驟

[準備要使用 PowerShell 的資料](walkthrough-prepare-the-data.md)
