---
title: Python 到 SQL 的資料類型轉換
description: 在資料科學和機器學習解決方案中, 檢查 Python 和 SQL Server 之間的隱含和明確資料類型轉換。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 690126098bbbd3ab26add51a0484f735120351de
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715787"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python 和 SQL Server 之間的資料類型對應
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

針對在 SQL Server Machine Learning 服務的 Python 整合功能上執行的 Python 解決方案, 請參閱不支援的資料類型清單, 以及在 Python 與 SQL Server 之間傳遞資料時, 可能會隱含執行的資料類型轉換。

## <a name="python-version"></a>Python 版本

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
