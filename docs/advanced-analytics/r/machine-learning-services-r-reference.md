---
title: "SQL Server 機器學習服務的 API 參考 |Microsoft 文件"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9267a2f0740f92f023f94fea3a26ca42de134b2c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="api-reference-for-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的 API 參考

本文章提供機器學習 SQL Server 所使用的應用程式開發介面的參考文件的連結。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

大部分的情況下，SQL Server 會使用 Microsoft R Server 和 Microsoft 機器學習 Server 中提供的相同 R，並將 Python 程式庫。 

> [!NOTE]
> 適用於所有 Api 的文件衍生自原始碼，而且無法編輯。 如果您看到錯誤，請新增註解中的應用程式開發介面參考文件。 

## <a name="r"></a>R

+ [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

    支援遠端運算內容以及多個資料來源的可擴充演算法。

+ [MicrosoftML](https://docs.microsoft.com/machine-learning-serverr-reference/microsoftml/microsoftml-package)

    快速且可擴充的機器學習演算法和轉換為 r 需要 RevoScaleR。

+ [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)

   讀取的 OLAP 資料來源結構描述，並執行 MDX 查詢。

+ [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)

    從 R 程式碼產生格式正確的預存程序的 helper 函式。

+ [mrsdeploy](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)

   主控台應用程式中建立遠端工作階段以及發行及管理 web 服務，使用 R 或 Python 程式碼的函式。

## <a name="python"></a>Python

+ [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)

    RevoScaleR 封裝，R 語言的 Python 對應項。 支援相同的計算內容和資料來源。

+ [Python Microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)

    MicrosoftML Python 相當於相同的計算內容和資料來源，如。 支援封裝，並包含快速、 可擴充演算法和 microsoft 的轉換。 

## <a name="related-apis"></a>相關的應用程式開發介面

+ [RevoPEMAR 函式參考](https://docs.microsoft.com/machine-learning-server/r-reference/revopemar/pemar)

    支援的平行演算法的開發

+ [RevoUtils](https://docs.microsoft.com/machine-learning-server/r-reference/revoutils/revoutils)

    RevoScaleR 環境搭配使用的公用程式函式

## <a name="other"></a>其他

「 如何 」 主題以及特定的這些 R 或 SQL Server 中的 Python 應用程式開發介面使用的彙總可以在這裡找到：

+ [使用 SQL Server scaleR 函數](scaler-functions-for-working-with-sql-server-data.md)
+ [產生使用 sqlrutils 預存程序](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
+ [使用 olapR R 讀取 MDX 資料](how-to-create-mdx-queries-using-olapr.md)
