---
title: olapR R 函式程式庫-SQL Server Machine Learning 服務
description: 在 SQL Server 2016 R Services 和 SQL Server 2017 Machine Learning 服務 olapR 函式程式庫簡介
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e5419900b8ba573ec0658a5022be68105b0b8607
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641852"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR （SQL Server 中的 R 程式庫）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**olapR**是 Microsoft 程式庫，用於對 SQL Server Analysis Services OLAP cube 的 MDX 查詢的 R 函數。 函式不支援所有 MDX 作業，但您可以建立查詢，該配量，骰子，向下鑽研、 彙總套件，並在維度上進行樞紐分析。 

此套件不會預先載入至 R 工作階段。 執行下列命令以載入程式庫。

```R
library(olapR)
```

您可以使用此程式庫連接到 Analysis Services OLAP cube 上所有支援的 SQL Server 版本上。 連接到表格式模型不支援這一次。

## <a name="package-version"></a>套件版本

目前版本為 1.0.0 中僅限 Windows 的所有產品，並下載提供的程式庫。

## <a name="full-reference-documentation"></a>完整的參考文件

**Olapr**程式庫會分散在多個 Microsoft 產品中，但不論您取得 SQL Server 或另一個產品中的程式庫使用方式都相同。 函式是相同的因為[個別 sqlrutils 函式文件](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)發行到下一個位置[R 參考](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的 Microsoft Machine Learning Server。 應該任何產品專屬行為存在時，差異會記錄在函式說明頁面。

## <a name="availability-and-location"></a>可用性和位置

此套件會提供在下列的產品，以及在 Azure 上的數個虛擬機器映像。 封裝位置隨之而異。

產品 | Location |
--------|----------|
SQL Server 2017 Machine Learning 服務 （使用 R 整合） | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Program Files\Microsoft\R Client\R_SERVER\library |
資料科學虛擬機器 （位於 Azure) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
SQL Server 虛擬機器 （位於 Azure) <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> R 整合是選擇性的 SQL Server。 當您將機器學習或 R 功能新增 VM 組態期間，將會安裝 olapR 程式庫。


## <a name="see-also"></a>另請參閱

[如何建立使用 olapR MDX 查詢](how-to-create-mdx-queries-using-olapr.md)
