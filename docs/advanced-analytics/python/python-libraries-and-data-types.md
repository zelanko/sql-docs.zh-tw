---
title: Python 到 SQL 資料類型轉換為 SQL Server Machine Learning
description: 檢閱 Python 與 SQL Server 之間的資料科學和機器學習服務解決方案中隱含與明確的資料型別 converstions。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9578f81146f0dab42e7a607b9e8ab410313958d4
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431972"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>在 Python 和 SQL Server 之間的資料類型對應
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 SQL Server Machine Learning 服務中的 Python 整合功能上執行的 Python 解決方案，請檢閱不支援的資料類型和 Python 與 SQL Server 之間傳遞資料時可能會以隱含方式執行的資料類型轉換的清單。

## <a name="python-version"></a>Python 版本

SQL Server 2017 Anaconda 4.2 發佈和 Python 3.6。

RevoScaleR 功能的子集 (rxLinMod，rxLogit，rxPredict，rxDTrees，rxBTrees，可能是其他一些) 使用 使用新的 Python 套件的 Python Api 來提供**revoscalepy**。 您可以使用此套件使用 Pandas 資料框架、 XDF 檔案或 SQL 資料查詢的資料搭配使用。

如需詳細資訊，請參閱 < [SQL Server 中的 revoscalepy 模組](ref-py-revoscalepy.md)並[revoscalepy 函式參考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)。

Python 支援有限的數目的資料類型，相較於 SQL Server。 如此一來，每當您使用 Python 指令碼中的資料從 SQL Server 時，資料可能會隱含地轉換成相容的資料類型。 不過，通常的確切轉換無法自動執行，而且會傳回錯誤。

## <a name="python-and-sql-data-types"></a>Python 和 SQL 資料類型

下表列出所提供的隱含轉換。 不支援其他資料型別。

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

