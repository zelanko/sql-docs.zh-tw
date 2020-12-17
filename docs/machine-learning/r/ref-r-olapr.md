---
title: olapR R 套件
description: olapR 為 Microsoft 的 R 套件，用於針對 SQL Server Analysis Services OLAP Cube 進行 MDX 查詢。 函式不支援所有 MDX 作業，但是您可以建置在維度上進行配量、切割、向下讚研、彙總和樞紐的查詢。 該套件包含在 SQL Server 機器學習服務與 SQL Server 2016 R Services 中。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: fc9c222bfb1229deea7ef734658b1d3b6b86149d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470799"
---
# <a name="olapr-r-package-in-sql-server-machine-learning-services"></a>olapR (SQL Server 機器學習服務中的 R 套件)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

**olapR** 為 Microsoft 的 R 套件，用於針對 SQL Server Analysis Services OLAP Cube 進行 MDX 查詢。 函式不支援所有 MDX 作業，但是您可以建置在維度上進行配量、切割、向下讚研、彙總和樞紐的查詢。 該套件包含在 [SQL Server 機器學習服務](../sql-server-machine-learning-services.md)與 [SQL Server 2016 R Services](sql-server-r-services.md) 中。

您可以使用此套件連線到所有支援 SQL Server 版本上的 Analysis Services OLAP Cube。 目前不支援連線到表格式模型。

## <a name="load-package"></a>載入套件

**olapR** 套件未預先載入 R 工作階段中。 請執行下列命令以載入套件。

```R
library(olapR)
```

## <a name="package-version"></a>套件版本

在所有僅限 Windows 產品，以及提供該套件的下載中，目前版本為 1.0.0。

## <a name="full-reference-documentation"></a>完整參考文件

**olapr** 套件分散在多個 Microsoft 產品中，但不論您是從 SQL Server 或其他產品中取得該套件，使用方式都相同。 由於函式相同，因此[個別 sqlrutils 函式的文件](/machine-learning-server/r-reference/olapr/olapr)只會發佈至 Microsoft Machine Learning Server [R 參考](/machine-learning-server/r-reference/introducing-r-server-r-package-reference)底下的一個位置。 若有任何產品特定行為存在，函式說明頁面中將會註明不一致之處。

## <a name="availability-and-location"></a>可用性和位置

下列產品以及 Azure 上的數個虛擬機器映像提供了此套件。 套件位置會隨之改變。

Products | Location |
--------|----------|
SQL Server 機器學習服務 (內含 R 整合) | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Program Files\Microsoft\R Client\R_SERVER\library |
資料科學虛擬機器 (在 Azure 上) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
SQL Server 虛擬機器 (在 Azure 上) <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> R 整合在 SQL Server 中是選擇性項目。 當您在 VM 組態期間新增機器學習或 R 功能時，即會安裝 olapR 套件。


## <a name="see-also"></a>另請參閱

[如何使用 olapR 建立 MDX 查詢](how-to-create-mdx-queries-using-olapr.md)