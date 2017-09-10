---
title: "Python 程式庫 |Microsoft 文件"
ms.custom: 
ms.date: 03/30/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ec0e006a71bb8634b77b83551c9ad82bdb41b246
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="python-libraries-and-data-types"></a>Python 程式庫和資料類型

本主題描述與下列產品包含 Python 程式庫：

+ SQL Server 機器學習服務 （資料庫）
+ Microsoft 的機器學習伺服器 （獨立）

本主題也會列出不支援的資料類型和清單的資料類型轉換的 Python 和 SQL Server 之間傳遞資料時可能會隱含地執行。

## <a name="python-version"></a>Python 版本

SQL Server 2017 CTP 2.0 包含 Anaconda 發佈和 Python 3.6 的一部分。

RevoScaleR 功能子集 (rxLinMod，rxLogit，rxPredict，rxDTrees，rxBTrees，可能只有幾個其他項目) 會使用的 API Python，使用新的 Python 封裝提供**RevoScalePy**。 若要使用的資料使用熊資料框架，，您可以使用此套件。SQL 資料查詢或 XDF 檔案。

如需詳細資訊，請參閱[何謂 revoscalepy？](what-is-revoscalepy.md)。

## <a name="python-and-sql-data-types"></a>Python 和 SQL 資料類型

Python 支援有限的數目的資料類型，相較於 SQL Server。

如此一來，每當您使用的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Python 指令碼中的資料可能會隱含地轉換成相容的資料類型。 不過，通常完全無法執行轉換，而且會傳回錯誤。

下表列出所提供的隱含轉換。 不支援其他資料型別。

|SQLtype|Python 類型|
|-|-|
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




