---
title: olapR R 函數程式庫
description: 簡介 SQL Server 2016 R Services 中的 olapR 函式程式庫和使用 R 的 SQL Server 2017 Machine Learning Services。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 674e4ed4d1967452093e81e7bb4f5518d9237cf6
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469981"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (SQL Server 中的 R 程式庫)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapR**是 R 函數的 Microsoft 程式庫, 用於針對 SQL Server Analysis Services OLAP CUBE 的 MDX 查詢。 函式不支援所有 MDX 作業, 但是您可以在維度上建立配量、骰子、明細、匯總和資料透視的查詢。 

此套件未預先載入 R 會話中。 執行下列命令以載入程式庫。

```R
library(olapR)
```

您可以使用此程式庫連接到所有支援的 SQL Server 版本上的 Analysis Services OLAP Cube。 目前不支援連接到表格式模型。

## <a name="package-version"></a>套件版本

目前的版本在所有僅限 Windows 的產品和提供程式庫的下載中都是1.0.0。

## <a name="full-reference-documentation"></a>完整參考檔

**Olapr**程式庫是散發在多個 Microsoft 產品中, 但不論您是在 SQL Server 或其他產品中取得程式庫, 使用方式都相同。 因為函式相同, 所以[個別 sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)函式的檔集只會發佈到[R 參考](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的一個位置, 以供 Microsoft Machine Learning Server。 若有任何產品特定行為存在, 則函式說明頁面中會注明不一致的情況。

## <a name="availability-and-location"></a>可用性和位置

下列產品提供此套件, 以及 Azure 上的數個虛擬機器映射。 套件位置也會隨之改變。

產品 | Location |
--------|----------|
SQL Server 2017 Machine Learning 服務 (使用 R 整合) | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R 伺服器) | C:\Program Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Program Files\Microsoft\R Client\R_SERVER\library |
資料科學虛擬機器 (在 Azure 上) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
SQL Server 虛擬機器 (在 Azure 上) <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup>在 SQL Server 中, R 整合是選擇性的。 當您在 VM 設定期間新增 Machine Learning 或 R 功能時, 將會安裝 olapR 程式庫。


## <a name="see-also"></a>另請參閱

[如何使用 olapR 建立 MDX 查詢](how-to-create-mdx-queries-using-olapr.md)
