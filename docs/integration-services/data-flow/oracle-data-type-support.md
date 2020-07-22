---
title: Microsoft Connector for Oracle 資料類型支援 | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: abbcea42546421fb7c0d3fef9824ef8ef56d2a0c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913784"
---
# <a name="microsoft-connector-for-oracle-data-type-support"></a>Microsoft Connector for Oracle 資料類型支援

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Oracle 的 SSIS 元件不支援所有 Oracle 資料類型。 在 SSDT 中設計套件時，具有不支援之資料類型的資料行將出現警告，而且將會從對應資料行中刪除。 無法將資料載入具有不支援之資料類型的資料行。

## <a name="data-type-mapping"></a>資料類型對應

下表顯示 Oracle 資料庫資料類型，以及其 SSIS 資料類型的預設對應。 它也會顯示不支援的 Oracle 資料類型。

|Oracle 資料庫資料類型|SSIS 資料類型|註解|
|:-|:-|:-|
|VARCHAR2|DT_STR||
|NVARCHAR2|DT_WSTR||
|CHAR|DT_STR||
|NUMBER|DT_R8|您可以使用特定的有效位數與小數位數，將此變更為 DT_NUMERIC。 有效位數與小數位數是由使用者根據需求來定義的。 輸出將會是具有固定有效位數與小數位數的資料行資料。|
|NUMBER(P, S)| 當小數位數為 0 時，根據有效位數 (P) <li> DT_I1 <Li> DT_I2 <Li> DT_I4 <Li> DT_NUMBERIC(P,0)||
||DT_NUMERIC(P,S)||
|日期|DT_DBTIMESTAMP||
|<li>timestamp <li>TIMESTAMP WITH TIME ZONE <li>INTERVAL YEAR TO MONTH <li>INTERVAL DAY TO SECOND <li>TIMESTAMP WITH LOCAL TIME ZONE|DT_STR||
|RAW|DT_BYTES||
|CLOB|DT_TEXT|只有陣列模式才支援 CLOB、NCLOB 與 BLOB 資料類型，快速載入模式中不支援。|
|NCLOB|DT_NTEXT||
|BLOB|DT_IMAGE||
|UROWID|不支援||
|REF|不支援||
|BFILE|不支援||
|LONG|不支援||
|LONG RAW|不支援||
|ROWID|不支援||
|使用者定義型別 (物件類型、VARRAY、巢狀表格)|不支援||

## <a name="next-steps"></a>後續步驟

- 設定 [Oracle 連線管理員](oracle-connection-manager.md)。
- 設定 [Oracle 來源](oracle-source.md)。
- 設定 [Oracle 目的地](oracle-destination.md)。
- 如有任何疑問，請瀏覽 [TechCommunity](https://aka.ms/AA5u35j) \(英文\)。
