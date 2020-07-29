---
title: 使用 R 套件的祕訣
description: 針對不熟悉 R 或 SQL Server 使用者，了解有關在 SQL Server 中使用 R 套件的實用秘訣。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/06/2019
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: ad2650317958ffd43b0f4b910585d429249115b3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730541"
---
# <a name="tips-for-using-r-packages"></a>使用 R 套件的祕訣

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

本文提供有關在 SQL Server 中使用 R 套件的實用秘訣。 這些秘訣適用於不熟悉 R 的 DBA，以及不熟悉 SQL Server 執行個體中之套件存取的有經驗 R 開發人員。

## <a name="if-youre-new-to-r"></a>如果您不熟悉 R

身為第一次安裝 R 套件的系統管理員，了解有關 R 套件管理的一些基本知識可協助您開始著手。

### <a name="package-dependencies"></a>套件相依性

R 套件經常依存於多個其他套件，其中有些可能在執行個體所使用的預設 R 程式庫中並未提供。 有時，套件所需的相依套件版本與已安裝的套件版本不同。 套件相依性會在內嵌於套件的 DESCRIPTION 檔案中註明，但有時並不完整。 您可以使用稱為 [iGraph](https://igraph.org/r/) 的套件來完整表達相依性關係圖。

如果您需要安裝多個套件，或想要確保組織中的每個人都取得正確的套件類型與版本，建議您使用 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 套件來分析完整的相依性鏈結。 minicRAN 會建立可在多個使用者或電腦之間共用的本機存放庫。 如需詳細資訊，請參閱[使用 miniCRAN 建立本機套件存放庫](create-a-local-package-repository-using-minicran.md)。

### <a name="package-sources-versions-and-formats"></a>套件來源、版本及格式

R 套件有多個來源，例如 [CRAN](https://cran.r-project.org/) 和 [Bioconductor](https://www.bioconductor.org/)。 R 語言的官方網站 (<https://www.r-project.org/>) 這當中列出許多資源。 Microsoft 提供 [MRAN](https://mran.microsoft.com/) 來散發其開放原始碼 R ([MRO](https://mran.microsoft.com/open)) 及其他套件。 許多套件都發佈到 GitHub，開發人員可從該處取得原始程式碼。

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
R 套件可在多個運算平台上執行。 請確定您安裝的版本是 Windows 二進為檔。
::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
R 套件可在多個運算平台上執行。 請確定您安裝的版本是 Linux 二進為檔。
::: moniker-end

### <a name="know-which-library-youre-installing-to-and-which-packages-are-already-installed"></a>了解您要安裝至哪一個程式庫及已經安裝哪些套件

如果您先前已修改電腦上的 R 環境，在安裝任何項目之前，請確保 R 環境變數 `.libPath` 僅使用一個路徑。

此路徑應指向執行個體的 R_SERVICES 資料夾。 如需詳細資訊 (包括如何判斷已經安裝哪些套件)，請參閱[取得 R 套件資訊](../package-management/r-package-information.md)。

## <a name="if-youre-new-to-sql-server"></a>如果您不熟悉 SQL Server

身為處理在 SQL Server 上執行之程式碼的 R 開發人員，保護伺服器的安全性原則會限制您控制 R 環境的能力。 下列秘訣說明一般情況，並提供在此環境中工作的建議。

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 使用者程式庫：SQL Server 上不支援

需要安裝新 R 套件的 R 開發人員已習慣隨意安裝套件，每當無法使用預設程式庫，或當開發人員不是電腦上的系統管理員時，便使用私人使用者程式庫。 例如，在一般的 R 開發環境中，使用者會將套件的位置新增至 R 環境變數 `libPath`，或參考完整套件路徑，就像這樣：

```R
library("c:/Users/<username>/R/win-library/packagename")
```

此做法在於 SQL Server 中執行 R 解決方案時行不通，因為 R 套件必須安裝至與執行個體相關聯的特定預設程式庫中。 當預設程式庫中沒有套件可用時，如果您嘗試呼叫套件，就會收到此錯誤：

*程式庫(xxx) 中發生錯誤: 沒有名為 'package-name' 的套件*

如需有關如何在 SQL Server 中安裝 R 套件的資訊，請參閱[在 SQL Server 機器學習服務或 SQL Server R Services 上安裝新的 R 套件](install-additional-r-packages-on-sql-server.md)。

### <a name="how-to-avoid-package-not-found-errors"></a>如何避免「找不到套件」錯誤

使用下列指導方針將可幫助您避免「找不到套件」錯誤。

+ 消除對使用者程式庫的相依性。

    將所需的 R 套件安裝至自訂使用者程式庫是不良的開發做法。 如果解決方案的執行者是另一位沒有程式庫位置存取權的使用者，就可能導致錯誤。

    此外，如果套件安裝在預設程式庫中，則即使您在 R 程式碼中指定不同的版本，R 執行階段仍是會從預設程式庫載入套件。

+ 確定您的程式碼能夠在共用環境中執行。

+ 避免將套件安裝成解決方案的一部分。 如果您無權安裝套件，程式碼將會失敗。 即使您有權安裝套件，您也應該將該作業與其他想要執行的程式碼個別處理。

+ 檢查您的程式碼，以確保不會呼叫已解除安裝的封裝。

+ 更新您的程式碼，以移除對 R 套件或 R 程式庫之路徑的直接參考。

+ 了解哪一個套件程式庫與執行個體相關聯。 如需詳細資訊，請參閱[取得 R 套件資訊](../package-management/r-package-information.md)。

## <a name="see-also"></a>另請參閱

::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
+ [使用 R 工具來安裝套件](install-r-packages-standard-tools.md)
::: moniker-end
::: moniker range=">sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
+ [使用 sqlmlutils 來安裝新的 R 套件](install-additional-r-packages-on-sql-server.md)
::: moniker-end
