---
title: 使用 R 套件安裝在使用者程式庫-SQL Server Machine Learning 服務的秘訣
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: bb354e1a0a7f7f22a39b690fdd0c0f4ae7778b8f
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140506"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>SQL Server 中使用 R 套件的秘訣
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章有不熟悉 R 和有經驗的 R 開發人員不熟悉的套件存取 SQL Server 執行個體的 Dba 另一節。

## <a name="new-to-r"></a>不熟悉 R

以系統管理員身分安裝 R 封裝第一次，了解 R 封裝管理相關的一些基本概念可協助您立即開始。

### <a name="package-dependencies"></a>封裝相依性

R 套件通常取決於多個其他封裝，其中有些可能無法使用的執行個體所使用的預設 R 程式庫中。 有時候封裝需要不同版本的已安裝的相依套件。 封裝相依性會內嵌在封裝中，說明檔中所述，但有時並不完整。 您可以使用套件，稱為[iGraph](https://igraph.org/r/)來完全清楚表達相依性圖形。

如果您要安裝多個封裝，或想要確保您的組織中的每個人取得正確的套件類型和版本，我們建議您使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)封裝来分析的完整相依性鏈結。 minicRAN 建立本機儲存機制，可在多個使用者或電腦之間共用。 如需詳細資訊，請參閱 <<c0> [ 建立本機套件儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="package-sources-versions-and-formats"></a>套件來源、 版本和格式

有多個來源的 R 套件的這類[CRAN](https://cran.r-project.org/)並[Bioconductor](https://www.bioconductor.org/)。 R 語言的官方網站 (<https://www.r-project.org/>) 列出許多這些資源。 Microsoft 提供了[MRAN](https://mran.microsoft.com/)其分佈的開放原始碼 R ([MRO](https://mran.microsoft.com/open)) 和其他套件。 許多套件會發佈到 GitHub，開發人員可以在哪裡取得原始程式碼。

在多個運算平台上，執行 R 套件。 請務必在您安裝的版本是 Windows 二進位檔。

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>了解您安裝到哪一個程式庫，並已安裝的套件。

如果您先前已修改 R 環境的電腦上，安裝任何項目之前，確定 R 環境變數`.libPath`會使用一個路徑。

這個路徑應該指向的執行個體的 R_SERVICES 資料夾。 如需詳細資訊，包括如何判斷已安裝的套件，請參閱 < [SQL Server 中的預設 R 和 Python 套件](../package-management/default-packages.md)。

## <a name="new-to-sql-server"></a>SQL server

身為使用 SQL Server 上執行的程式碼的 R 開發人員，保護伺服器的安全性原則會限制您能夠控制 R 環境。

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 使用者程式庫： 不支援 SQL Server

想要安裝新的 R 套件的 R 開發人員習慣安裝套件位置，使用私用、 使用者程式庫時的預設程式庫不提供，或開發人員並不在電腦上的系統管理員。 比方說，在一般的 R 開發環境，使用者會將封裝的位置給 R 環境變數`libPath`，或參考完整的封裝路徑，就像這樣：

```R
library("c:/Users/<username>/R/win-library/packagename")
```

這無法運作時執行的 R 解決方案，在 SQL Server，因為必須安裝 R 套件，以執行個體相關聯的特定預設程式庫。 封裝無法使用時的預設程式庫中，您收到這個錯誤，當您嘗試呼叫封裝：

*（xxx） 中的錯誤： 沒有名為 ' 封裝-name' 的封裝*

### <a name="avoid-package-not-found-errors"></a>避免發生 「 找不到套件 」 錯誤

+ 排除在使用者程式庫的相依性。 

    因為若方案由另一位使用者沒有存取程式庫位置執行，它會導致錯誤，則必要的 R 套件安裝到自訂的使用者程式庫，是不正確的開發做法。

    此外，如果封裝已安裝預設文件庫中，R 執行階段載入封裝從預設程式庫，即使您在 R 程式碼中指定不同的版本。

+ 修改您的程式碼，在共用環境中執行。

+ 避免安裝套件作為解決方案的一部分。 如果您沒有權限才能安裝封裝，程式碼將會失敗。 即使您沒有權限才能安裝封裝，您應該從其他您想要執行的程式碼因此分開進行。

+ 檢查您的程式碼，以確保不會呼叫已解除安裝的封裝。

+ 更新您的程式碼，若要移除的 R 套件或 R 程式庫路徑的直接參考。 

+ 知道哪一個套件程式庫的執行個體相關聯。 如需詳細資訊，請參閱 < [SQL Server 中的預設 R 和 Python 套件](../package-management/default-packages.md)。

## <a name="see-also"></a>另請參閱

+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)