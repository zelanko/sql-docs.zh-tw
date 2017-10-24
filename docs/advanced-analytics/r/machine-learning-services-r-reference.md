---
title: "SQL Server 機器學習服務的 API 參考 |Microsoft 文件"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c776c43d66d01a2f721b5d3d8bc540741bf8b13
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---

# <a name="api-reference-for-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的 API 參考

本文章提供機器學習 SQL Server 所使用的應用程式開發介面的參考文件的連結。 

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

大部分的情況下，SQL Server 會使用 Microsoft R Server 和 Microsoft 機器學習 Server 中提供的相同 R，並將 Python 程式庫。 

> [!NOTE]
> 適用於所有 Api 的文件衍生自原始碼，而且不是後置編輯。

## <a name="r"></a>R

+ [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

    支援遠端運算內容以及多個資料來源的可擴充演算法。

+ [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    快速且可擴充的機器學習演算法和轉換為 r 需要 RevoScaleR。

+ [olapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr)

   讀取的 OLAP 資料來源結構描述，並執行 MDX 查詢。

+ [sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils)

    從 R 程式碼產生格式正確的預存程序的 helper 函式。

+ [mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)

   主控台應用程式中建立遠端工作階段以及發行及管理 web 服務，使用 R 或 Python 程式碼的函式。

## <a name="python"></a>Python

+ [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

    RevoScaleR 封裝，R 語言的 Python 對應項。 支援相同的計算內容和資料來源。

+ [Python Microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

    MicrosoftML Python 相當於相同的計算內容和資料來源，如。 支援封裝，並包含快速、 可擴充演算法和 microsoft 的轉換。

## <a name="related-apis"></a>相關的應用程式開發介面

+ [RevoPEMAR 函式參考](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

    支援的平行演算法的開發

+ [RevoUtils](https://docs.microsoft.com/r-server/r-reference/revoutils/revoutils)

    RevoScaleR 環境搭配使用的公用程式函式

## <a name="other"></a>其他

「 如何 」 主題以及特定的這些 R 或 SQL Server 中的 Python 應用程式開發介面使用的彙總可以在這裡找到：

+ [使用 SQL Server scaleR 函數](scaler-functions-for-working-with-sql-server-data.md)
+ [產生使用 sqlrutils 預存程序](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
+ [使用 olapR R 讀取 MDX 資料](how-to-create-mdx-queries-using-olapr.md)

