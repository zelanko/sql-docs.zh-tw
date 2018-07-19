---
title: 使用安裝 SQL Server 上的使用者文件庫中的 R 封裝的秘訣 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e52a6f4a9a3830aab01e54819804785a7069c9d2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708466"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>SQL Server 中使用 R 封裝的秘訣
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章針對 Dba 人員不熟悉 R 與經驗豐富的 R 開發人員不熟悉的封裝之存取的 SQL Server 執行個體中有另一節。

## <a name="new-to-r"></a>R 的新手

身為系統管理員安裝 R 封裝第一次，了解幾個 R 封裝管理基本概念可協助您快速入門。

### <a name="package-dependencies"></a>封裝的相依性

R 封裝經常會相依於其他的多個封裝，其中有些可能無法使用執行個體所使用的預設 R 程式庫中。 有時封裝需要相依的套件已經安裝不同版本。 封裝的相依性會內嵌在封裝中，說明檔中註明，但是可能不完整。 您可以使用稱為封裝[iGraph](http://igraph.org/r/)至相依性圖形會完整說明。

如果您需要安裝多個封裝，或想要確保您的組織中每個人都取得正確的封裝類型和版本，我們建議您使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)封裝来分析的完整相依性鏈結。 minicRAN 建立可以在多個使用者或電腦間共用的本機儲存機制。 如需詳細資訊，請參閱[建立本機封裝儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="package-sources-versions-and-formats"></a>封裝來源、 版本和格式

有多個來源取得 R 封裝的這類[CRAN](https://cran.r-project.org/)和[Bioconductor](https://www.bioconductor.org/)。 R 語言的官方網站 (<https://www.r-project.org/>) 會列出許多資源。 Microsoft 提供[MRAN](https://mran.microsoft.com/)其分佈的開放原始碼 R ([MRO](https://mran.microsoft.com/open)) 和其他封裝。 許多封裝會發佈到 GitHub，開發人員可以在這裡取得原始程式碼。

在多個運算平台上，執行 R 封裝。 請確定您所安裝的版本是 Windows 二進位檔案。

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>知道您要安裝哪一個程式庫，以及已安裝的封裝。

如果您先前已修改 R 環境的電腦上，安裝任何項目之前，請確定 R 環境變數`.libPath`會使用單一路徑。

這個路徑應該指向 R_SERVICES 資料夾執行個體。 如需詳細資訊，包括如何判斷已安裝的封裝，請參閱[在 SQL Server 中的預設 R，並將 Python 封裝](installing-and-managing-r-packages.md)。

## <a name="new-to-sql-server"></a>新的 SQL server

身為使用 SQL Server 上執行的程式碼的 R 開發人員，保護伺服器的安全性原則會限制您可以控制的 R 環境。

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 使用者程式庫： 不支援 SQL Server

R 開發人員需要安裝新的 R 封裝習慣安裝封裝，在每次您的預設程式庫就無法使用，或當開發人員不是在電腦上的系統管理員使用私用，使用者程式庫。 例如，在一般的 R 開發環境，使用者會將封裝的位置 R 環境變數`libPath`，或參考完整的封裝路徑，就像這樣：

```R
library("c:/Users/<username>/R/win-library/packagename")
```

這不會運作，執行 SQL Server 中的 R 解決方案時因為安裝 R 封裝，至特定的預設文件庫的執行個體相關聯。 封裝無法使用時的預設程式庫中，您收到這個錯誤，當您嘗試呼叫封裝：

*Library(xxx) 時發生錯誤： 沒有名為 ' 封裝 name' 的封裝*

### <a name="avoid-package-not-found-errors"></a>避免發生 「 找不到封裝 」 錯誤

+ 排除使用者程式庫的相依性。 

    若要安裝必要的 R 封裝至自訂使用者文件庫中，不正確的開發作法是因為若方案由另一個使用者沒有存取程式庫位置執行，它會導致錯誤。

    此外，如果封裝已安裝預設文件庫中，R 執行階段從載入封裝的預設程式庫中，即使您指定了不同版本的 R 程式碼中。

+ 修改您的程式碼在共用環境中執行。

+ 避免安裝封裝，做為方案的一部分。 如果您沒有權限才能安裝封裝，程式碼將會失敗。 即使您沒有權限才能安裝封裝，您應該做因此分別從您想要執行其他程式碼。

+ 檢查您的程式碼，以確保不會呼叫已解除安裝的封裝。

+ 更新您的程式碼，以便移除直接參考的 R 封裝或 R 程式庫路徑。 

+ 了解哪些封裝程式庫是與執行個體相關聯。 如需詳細資訊，請參閱[在 SQL Server 中的預設 R，並將 Python 封裝](installing-and-managing-r-packages.md)。

## <a name="see-also"></a>另請參閱

+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)