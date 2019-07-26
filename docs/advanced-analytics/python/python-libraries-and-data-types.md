---
title: Python 到 SQL 的資料類型轉換
description: 請參閱資料科學和機器學習服務解決方案中的 Python 和 SQL Server 之間的隱含和明確資料類型 converstions。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8aea7e67f6560aa750e67601b5b6a41f7d68b47d
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470341"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python 和 SQL Server 之間的資料類型對應
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

針對在 SQL Server Machine Learning 服務的 Python 整合功能上執行的 Python 解決方案, 請參閱不支援的資料類型清單, 以及在 Python 與 SQL Server 之間傳遞資料時, 可能會隱含執行的資料類型轉換。

## <a name="python-version"></a>Python 版本

SQL Server 2017 Anaconda 4.2 散發和 Python 3.6。

RevoScaleR 功能的子集 (rxLinMod、rxLogit、rxPredict、rxDTrees、rxBTrees 等) 是使用 Python Api (使用新的 Python 套件**revoscalepy**) 所提供。 您可以使用此封裝, 使用 Pandas 資料框架、XDF 檔案或 SQL 資料查詢來處理資料。

如需詳細資訊, 請參閱 SQL Server 和[revoscalepy 函數參考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)[中的 revoscalepy 模組](ref-py-revoscalepy.md)。

與 SQL Server 相比, Python 支援的資料類型數量有限。 因此, 每當您在 Python 腳本中使用來自 SQL Server 的資料時, 資料可能會隱含地轉換成相容的資料類型。 不過, 通常無法自動執行精確的轉換, 而且會傳回錯誤。

## <a name="python-and-sql-data-types"></a>Python 和 SQL 資料類型

下表列出所提供的隱含轉換。 不支援其他資料類型。

|SQLtype|Python 類型|
|-------|-----------|
|**bigint**|`numeric`|
|**binary**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float32`|
|**smallint**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|

## <a name="see-also"></a>另請參閱

