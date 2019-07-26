---
title: 使用安裝在使用者程式庫中的 R 套件的秘訣
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 07993b982b5c79e3814aa29730fb1849075f5667
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470078"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>在 SQL Server 中使用 R 套件的秘訣
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這篇文章針對 Dba 提供了不同的區段, 這些是不熟悉 R 和經驗豐富的 R 開發人員, 不熟悉 SQL Server 實例中的封裝存取。

## <a name="new-to-r"></a>R 新手

身為系統管理員第一次安裝 R 套件時, 瞭解 R 套件管理的一些基本概念可協助您開始著手。

### <a name="package-dependencies"></a>封裝相依性

R 封裝經常取決於多個其他套件, 其中有些封裝可能無法在實例所使用的預設 R 程式庫中使用。 有時候封裝需要已安裝的不同版本的相依套件。 封裝相依性會在封裝中內嵌的描述檔案中注明, 但有時不完整。 您可以使用名為[iGraph](https://igraph.org/r/)的套件來完整表達相依性圖形。

如果您需要安裝多個套件, 或想要確保組織中的每個人都能取得正確的套件類型和版本, 建議您使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)套件來分析完整的相依性鏈。 minicRAN 會建立可在多個使用者或電腦之間共用的本機存放庫。 如需詳細資訊, 請參閱[使用 MiniCRAN 建立本機套件存放庫](create-a-local-package-repository-using-minicran.md)。

### <a name="package-sources-versions-and-formats"></a>封裝來源、版本和格式

R 套件有多個來源, 例如[CRAN](https://cran.r-project.org/)和[Bioconductor](https://www.bioconductor.org/)。 R 語言的官方網站 (<https://www.r-project.org/>) 會列出其中的許多資源。 Microsoft 為其開放原始碼 R ([MRO](https://mran.microsoft.com/open)) 和其他套件的散發提供了[MRAN](https://mran.microsoft.com/) 。 許多套件都會發佈至 GitHub, 開發人員可以在其中取得原始程式碼。

R 封裝會在多個計算平臺上執行。 請確定您安裝的版本是 Windows 二進位檔。

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>知道您要安裝的媒體櫃, 以及已安裝的套件。

如果您先前已修改電腦上的 R 環境, 在安裝任何專案之前, 請確定 R 環境變數`.libPath`只會使用一個路徑。

這個路徑應該指向實例的 R_SERVICES 資料夾。 如需詳細資訊, 包括如何判斷已安裝哪些套件, 請參閱[SQL Server 中的預設 R 和 Python 套件](../package-management/default-packages.md)。

## <a name="new-to-sql-server"></a>SQL Server 的新手

當 R 開發人員處理在 SQL Server 上執行的程式碼時, 保護伺服器的安全性原則會限制您控制 R 環境的能力。

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 使用者程式庫: SQL Server 不支援

需要安裝新 R 套件的 r 開發人員, 習慣在預設程式庫無法使用時, 或在開發人員不是電腦的系統管理員時, 使用私用的使用者程式庫來安裝套件。 例如, 在一般的 r 開發環境中, 使用者會將封裝的位置新增至 R 環境變數`libPath`, 或參考完整的封裝路徑, 如下所示:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

在 SQL Server 中執行 R 方案時, 這不適用, 因為 R 封裝必須安裝到與實例相關聯的特定預設程式庫。 當封裝無法在預設程式庫中使用時, 您會在嘗試呼叫封裝時收到此錯誤:

*程式庫中的錯誤 (xxx): 沒有名為 ' package-name ' 的套件*

### <a name="avoid-package-not-found-errors"></a>避免「找不到封裝」錯誤

+ 排除對使用者程式庫的相依性。 

    將必要的 R 套件安裝到自訂使用者程式庫是不正確的開發做法, 因為如果有另一位無法存取程式庫位置的使用者執行解決方案, 可能會導致錯誤。

    此外, 如果封裝安裝在預設程式庫中, R 執行時間會從預設程式庫載入封裝, 即使您在 R 程式碼中指定不同的版本也一樣。

+ 修改您的程式碼, 以在共用環境中執行。

+ 避免將套件安裝為解決方案的一部分。 如果您沒有安裝封裝的許可權, 程式碼將會失敗。 即使您有安裝套件的許可權, 還是應該與您要執行的其他程式碼分開。

+ 檢查您的程式碼，以確保不會呼叫已解除安裝的封裝。

+ 更新您的程式碼, 以移除 R 封裝或 R 程式庫路徑的直接參考。 

+ 知道哪個封裝程式庫與實例相關聯。 如需詳細資訊, 請參閱[SQL Server 中的預設 R 和 Python 封裝](../package-management/default-packages.md)。

## <a name="see-also"></a>另請參閱

+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)