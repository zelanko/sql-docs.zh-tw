---
title: 轉換 Python 與 SQL 資料類型
description: 檢閱資料科學與機器學習解決方案中 Python 與 SQL Server 之間的隱含與明確資料類型轉換。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/06/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: da92713dbf514e2500d0d5f8eb3e776523830041
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891348"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python 與 SQL Server 之間的資料類型對應
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

本文會列出在 SQL Server 機器學習服務中使用 Python 整合功能時，所支援資料類型及所執行的資料類型轉換。

相較於 SQL Server，Python 支援的資料類型數量有限。 因此，每當在 Python 指令碼中使用 SQL Server 的資料時，SQL 資料可能會隱含地轉換為合規的 Python 資料類型。 不過，通常無法自動執行精確的轉換，且會傳回錯誤。

## <a name="python-and-sql-data-types"></a>Python 與 SQL 資料類型

下表列出所提供的隱含轉換。 不支援其他資料類型。

| SQL 類型             | Python 類型 | 描述 |
|----------------------|-------------|-------------|
| **bigint**           | `float64`   |
| **binary**           | `bytes`     |
| **bit**              | `bool`      |
| **char**             | `str`       |
| **date**             | `datetime`  |
| **datetime**         |`datetime`   | 支援 SQL Server 2017 CU6 和更新版本 (具有 `datetime.datetime` 或 **Pandas** `pandas.Timestamp` 類型的**NumPy** 陣列)。 `sp_execute_external_script` 現在支援使用小數秒數的 `datetime` 類型。|
| **float**            | `float64`   |
| **nchar**            | `str`       |
| **nvarchar**         | `str`       |
| **nvarchar(max)**    | `str`       |
| **real**             | `float64`   |
| **smalldatetime**    | `datetime`  |
| **smallint**         | `int32`     |
| **tinyint**          | `int32`     |
| **uniqueidentifier** | `str`       |
| **varbinary**        | `bytes`     |
| **varbinary(max)**   | `bytes`     |
| **varchar(n)**       | `str`       |
| **varchar(max)**     | `str`       |

## <a name="see-also"></a>另請參閱

+ [R 與 SQL Server 之間的資料類型對應](../r/r-libraries-and-data-types.md)
