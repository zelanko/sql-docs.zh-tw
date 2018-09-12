---
title: 在 SQL Server Machine Learning 中的 Python 程式庫和資料類型 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 384c8c94bdef65e41af999848c9bac63fc0c8d40
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888364"
---
# <a name="python-libraries-and-data-types"></a>Python 程式庫和資料類型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明隨附於 SQL Server Machine Learning 服務 （資料庫） 和 （獨立式） 安裝的 Python 程式庫。

這篇文章也會列出不支援的資料類型和清單的資料類型轉換的 Python 和 SQL Server 之間傳遞資料時可能會隱含地執行。

## <a name="python-version"></a>Python 版本

SQL Server 2017 Anaconda 4.2 發佈和 Python 3.6。

RevoScaleR 功能的子集 (rxLinMod，rxLogit，rxPredict，rxDTrees，rxBTrees，可能是其他一些) 使用 使用新的 Python 套件的 Python Api 來提供**revoscalepy**。 您可以使用此套件使用 Pandas 資料框架、 XDF 檔案或 SQL 資料查詢的資料搭配使用。

如需詳細資訊，請參閱 <<c0> [ 什麼是 revoscalepy？](what-is-revoscalepy.md)。

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



