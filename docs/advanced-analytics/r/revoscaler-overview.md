---
title: 在 SQL Server 機器學習中的 RevoScaleR 封裝 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ecca127e3b929772c465ae7e1f694b525cc7dd00
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201970"
---
# <a name="revoscaler"></a>RevoScaleR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 是 Microsoft 支援大規模的資料科學所提供的機器學習服務函數封裝。

+ 函數支援資料匯入、 資料轉換、 摘要、 視覺化和分析。

+ _大規模_表示作業會針對極大型資料集，以平行方式，執行，而且在分散式檔案系統。 演算法可在不適合在記憶體中，藉由使用區塊處理和 reassembling 結果完成作業時的資料集上操作。

+ RevoScaleR 透過開放原始碼 R 函式提供多項改良。 沒有對應到多個最受歡迎的基底 R 函數的 RevoScaleR 函式。 RevoScaleR 函數皆加註**rx**或**Rx**前置詞，使其更容易識別。

+ RevoScaleR 作為分散式的資料科學的平台。 比方說，您可以使用 RevoScaleR 計算內容和轉換中的圖案狀態演算法[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)。 您也可以使用[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)以平行方式執行基底 R 函數。

RevoScaleR 的作用中的範例，請參閱這些部落格： 

+ [建置和部署使用 R 和 SQL Server 的預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [機器學習伺服器每秒 100 萬個預測](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [預測使用 MicrosoftML 計程車秘訣](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [效能最佳化的 rxExec](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

## <a name="how-to-get-revoscaler"></a>如何取得 RevoScaleR

RevoScaleR 封裝，R 的免費安裝 Microsoft R 用戶端中。 如果您有機器學習 Server 或 SQL Server 中使用 R 時，預設會包含 RevoScaleR。

如果您使用 Python， [revoscalepy](../python/what-is-revoscalepy.md)套件提供對等功能。

> [!IMPORTANT]
> 無法下載或使用獨立的產品和服務，其提供的 RevoScaleR 封裝。

## <a name="use-revoscaler-in-sql-server"></a>在 SQL Server 中使用 RevoScaleR

這些教學課程和範例示範如何使用 RevoScaleR 函數來取得資料從 SQL Server、 建立模型，並將模型儲存至資料庫，以進行計分。

+ [了解如何使用的計算內容](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 開發人員的 R： 訓練並進行操作模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 產品範例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)

## <a name="learn-more-about-revoscaler"></a>深入了解 RevoScaleR

這些教學課程示範如何在支援的其他計算內容中使用 RevoScaleR [Server 機器學習](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，包括 Hadoop。

+ [什麼是 RevoScaleR？](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler)

+ [探索 RevoScaleR 25 函式中](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)

+ [RevoScaleR 封裝參考](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

