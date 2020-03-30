---
title: Teradata 資料類型支援 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f83f028772a93dbd2104d9f449fcd7aa3b1be0d8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74543006"
---
# <a name="data-type-support"></a>資料類型支援

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

SSIS 元件會使用 Teradata Parallel Transporter API (TPT API) 從 Teradata 資料庫來回載入和傳輸資料，因此只有 TPT API 支援的資料類型可用於 SSIS。

> [!NOTE]
>
> Teradata 中的 TIME、TIMESTAMP 和 INTERVAL 資料類型是由 TPT API 作為固定大小的字元字串來處理。 Teradata 的 SSIS 元件會將它們作為字串處理。

## <a name="data-type-mapping"></a>資料類型對應

下表顯示 Teradata 資料庫資料類型，以及其 SSIS 資料類型的預設對應。 它也會顯示不支援的 Teradata 資料類型。

|SQL 資料類型|SSIS 資料類型|
|:-|:-|
|DECIMAL/NUMERIC|DT_NUMERIC|
|BYTEINT|DT_I1|
|SMALLINT|DT_I2|
|INTEGER|DT_I4|
|FLOAT/REAL/DOUBLE PRECISION|DT_R8|
|日期|DT_DBDATE|
|TIME<br>TIME(n)|DT_STR|
|timestamp<br>TIMESTAMP (n)|DT_STR|
|TIME WITH TIMEZONE<br>TIME(n) WITH TIMEZONE|DT_STR|
|TIMESTAMP WITH TIMEZONE<br>TIMESTAMP(n) WITH TIMEZONE|DT_STR|
|INTERVAL YEAR<br>INTERVAL YEAR (n)|DT_STR|
|INTERVAL YEAR TO MONTH<br>INTERVAL YEAR (n) TO MONTH|DT_STR|
|INTERVAL MONTH<br>INTERVAL MONTH (n)|DT_STR|
|INTERVAL DAY<br>INTERVAL DAY (n)|DT_STR|
|INTERVAL DAY TO HOUR<br>INTERVAL DAY (n) TO HOUR|DT_STR|
|INTERVAL DAY TO MINUTE<br>INTERVAL DAY (n) TO MINUTE|DT_STR|
|INTERVAL DAY TO SECOND<br>INTERVAL DAY (n) TO SECOND<br>INTERVAL DAY TO SECOND (m)<br>INTERVAL DAY (n) TO SECOND (m)|DT_STR|
|INTERVAL HOUR<br>INTERVAL HOUR (n)|DT_STR|
|INTERVAL HOUR TO MINUTE<br>INTERVAL HOUR (n) TO MINUTE|DT_STR
|INTERVAL HOUR TO SECOND<br>INTERVAL HOUR (n) TO SECOND<br>INTERVAL HOUR TO SECOND (m)<br>INTERVAL HOUR (n) TO SECOND (m)|DT_STR|
|INTERVAL MINUTE<br>INTERVAL MINUTE (n)|DT_STR|
|INTERVAL MINUTE TO SECOND<br>INTERVAL MINUTE (n) TO SECOND<br>INTERVAL MINUTE TO SECOND (m)<br>INTERVAL MINUTE (n) TO SECOND (m)|DT_STR|
|INTERVAL SECOND<br>INTERVAL SECOND (n)<br>INTERVAL SECOND (n,m)|DT_STR|
|PERIOD(DATE)|DT_STR|
|PERIOD(TIME)|DT_STR|
|NUMBER|DT_STR|
|CHARACTER|DT_STR|
|VARCHAR|DT_STR (DT_WSTR 用於 Unicode 字元集)<br>**注意**：<br> 支援的 VARCHAR 長度上限為 32000。 <br> 允許的 DT_STR 長度上限為 8000 個字元，DT_WSTR 為 4000 個字元。 如果超過，資料就會被截斷。|
|LONG VARCHAR|不支援|
|CLOB|不支援|
|BYTE|DT_BYTES<br>**注意**：允許的最大長度是 8000 位元組。 如果超過，資料就會被截斷。|
|VARBYTE|DT_BYTES<br>**注意**：允許的最大長度是 8000 位元組。 如果超過，資料就會被截斷。|
|BLOB|不支援|

## <a name="next-steps"></a>後續步驟

- 設定 [Teradata 連線管理員](teradata-connection-manager.md)
- 設定 [Teradata 來源](teradata-source.md)
- 設定 [Teradata 目的地](teradata-destination.md)
- 如有任何疑問，請瀏覽[技術社群](https://aka.ms/AA6iwdw)。
