---
title: 轉換 Python 與 SQL 資料類型
description: 檢閱資料科學與機器學習解決方案中 Python 與 SQL Server 之間的隱含與明確資料類型轉換。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f22f838bc78d4791e73a1d107cd253aae314d205
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727513"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python 與 SQL Server 之間的資料類型對應
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

針對在 SQL Server 機器學習服務中 Python 整合功能上執行的 Python 解決方案，請檢閱不支援的資料類型清單，以及在 Python 與 SQL Server 之間傳遞資料時，可能隱含執行的資料類型轉換。

## <a name="python-version"></a>Python 版本

RevoScaleR 功能的子集 (rxLinMod、rxLogit、rxPredict、rxDTrees、rxBTrees，也許還有一些其他功能) 會透過 Python API，使用新的 Python 套件 **revoscalepy** 來提供。 您可以使用此套件，使用 Pandas 資料框架、XDF 檔案或 SQL 資料查詢來處理資料。

如需詳細資訊，請參閱 [SQL Server 中的 revoscalepy 模組](ref-py-revoscalepy.md)和 [revoscalepy 函數參考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) \(英文\)。

相較於 SQL Server，Python 支援的資料類型數量有限。 因此，每當您在 Python 指令碼中使用來自 SQL Server 的資料時，資料可能會隱含地轉換為相容的資料類型。 不過，通常無法自動執行精確的轉換，而且會傳回錯誤。

## <a name="python-and-sql-data-types"></a>Python 與 SQL 資料類型

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
