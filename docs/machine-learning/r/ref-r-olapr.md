---
title: olapR R 函式程式庫
description: SQL Server 2016 R Services 和 SQL Server 機器學習服務 (使用 R) 中的 olapR 函式程式庫簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 507bd04140880a3c15f1e72eed49c29ade56769c
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117411"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (SQL Server 中的 R 程式庫)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapR** 是 R 函數的 Microsoft 程式庫，用來針對 SQL Server Analysis Services OLAP Cube 進行 MDX 查詢。 函式不支援所有 MDX 作業，但是您可以建置在維度上進行配量、切割、向下讚研、彙總和樞紐的查詢。 

此套件未預先載入 R 工作階段中。 請執行下列命令來載入該程式庫。

```R
library(olapR)
```

您可以使用此程式庫連線到所有受支援 SQL Server 版本上的 Analysis Services OLAP Cube。 目前不支援連線到表格式模型。

## <a name="package-version"></a>套件版本

在所有僅限 Windows 的產品和提供此程式庫的下載項目中，目前版本都是 1.0.0。

## <a name="full-reference-documentation"></a>完整參考文件

**olapr** 程式庫散佈在多個 Microsoft 產品中，但不論您是在 SQL Server 還是在另一個產品中取得此程式庫，其使用方式都相同。 由於函式相同，因此[個別 sqlrutils 函式的文件](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)只會發佈至 Microsoft Machine Learning Server [R 參考](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)底下的一個位置。 若有任何產品特定行為存在，函式說明頁面中將會註明不一致之處。

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

<sup>1</sup> R 整合在 SQL Server 中是選擇性項目。 當您在 VM 設定期間新增機器學習或 R 功能時，就會安裝 olapR 程式庫。


## <a name="see-also"></a>另請參閱

[如何使用 olapR 建立 MDX 查詢](how-to-create-mdx-queries-using-olapr.md)
