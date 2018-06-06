---
title: 與 SQL Server Machine Learning Python 交互操作性 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3ad52bb3774c1534ac745e1dc93d18c75260723c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="python-interoperability-with-sql-server"></a>Python 與 SQL Server 的互通性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如果您啟用此功能會安裝 Python 元件**機器學習服務 （資料庫）**並選取 Python 語言。

## <a name="python-components"></a>Python 元件

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 不會修改 Python 可執行檔。 Python 執行階段安裝獨立 SQL 工具，並執行的外部[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]程序。

具有特定相關聯之發佈[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]執行個體位於執行個體相關聯的資料夾。

例如，如果您使用預設執行個體上的 [Python] 選項安裝機器學習服務，查看底下：

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

安裝 SQL Server 2017 機器學習服務加入 Python Anaconda 的發佈。 具體來說，會使用 Anaconda 3 安裝程式，根據 Anaconda 4.3 分支。 SQL Server 2017 預期的 Python 層級是 Python 3.5。

## <a name="new-python-packages-in-this-release"></a>在此版本中新的 Python 封裝

支援 Anaconda 發佈的封裝清單，請參閱 Continuum analytics 網站： [Anaconda 封裝清單](https://docs.continuum.io/anaconda/pkg-docs)

在 SQL Server 2017 機器學習服務也包含新**revoscalepy** Python 程式庫。

此程式庫提供同等的功能**RevoScaleR**封裝成 Microsoft。換句話說，它支援建立遠端計算內容，以及各種的可調整的機器學習模型，例如**rxLinMod**。 如需 RevoScaleR 的詳細資訊，請參閱[分散式和平行計算與 ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)。

[Python microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) Python 加入您的安裝時，將會安裝為 SQL Server 機器學習服務一部分的封裝。 此套件包含許多機器學習演算法，已經過最佳化的速度和精確度，以及內嵌文字和影像所使用的轉換。 如需詳細資訊，請參閱[搭配 SQL Server 使用 MicrosoftML 封裝](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package)。

緊密結合 Microsoftml 和 revoscalepy;microsoftml 中使用資料來源定義為 revoscalepy 物件。 計算 microsoftml revoscalepy 傳輸的內容限制。 也就是所有功能都都可供本機作業，但遠端計算內容切換，需要 RxInSqlServer。

## <a name="using-python-in-sql-server"></a>SQL Server 中使用 Python

您匯入**revoscalepy**到您的 Python 程式碼，然後從模組的呼叫函式的模組會像任何其他的 Python 函式。

Python 的輸入的資料必須是表格式。 必須的形式傳回所有 Python 結果**熊**資料框架。

您可以藉由在預存程序中內嵌指令碼執行內 T-SQL 的 Python 程式碼。

或者，從本機的 Python IDE 執行程式碼，並且有執行的 SQL Server 電腦上，藉由定義遠端計算內容的指令碼。

您可以使用本機資料、 從 SQL Server 或其他 ODBC 資料來源取得資料，或使用 XDF 檔案格式來交換資料與其他來源，或 R 解決方案。

**如需詳細資訊**

+ 支援的函數：[何謂 revoscalepy](what-is-revoscalepy.md) 
+ 支援的 Python 資料類型： [Python 程式庫和資料類型](python-libraries-and-data-types.md)
+ 支援的資料來源： ODBC 資料庫、 SQL Server 和 XDF 檔案
+ 支援的計算內容： 本機或 SQL Server

### <a name="licensing"></a>授權

使用 Python 的機器學習服務安裝的一部分，您必須同意 GNU Public License 中的條款。

## <a name="see-also"></a>另請參閱

[Python 程式庫和資料類型](python-libraries-and-data-types.md)
