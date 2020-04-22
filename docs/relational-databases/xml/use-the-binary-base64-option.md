---
title: 使用 BINARY BASE64 選項 | Microsoft 文件
description: 了解如何在 SQL 查詢中使用 BINARY BASE64 選項，以使用 base64 編碼格式傳回二進位資料。
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: RothJa
ms.author: jroth
ms.openlocfilehash: fffd3833256ee6afa9dd3731d5cf02e99913e565
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388351"
---
# <a name="use-the-binary-base64-option"></a>使用 BINARY BASE64 選項

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

若查詢中指定 BINARY BASE64 選項，就會以 Base64 編碼格式傳回二進位資料。

若未在查詢中指定 BINARY BASE64 選項，則依預設 AUTO 模式可支援 URL 編碼的二進位資料。 將會傳回資料庫之虛擬根目錄的相對 URL 參考。 此參考會指向執行查詢所在的資料庫。 所傳回參考可用來存取後續作業中的實際二進位資料。 這項存取動作是使用 SQLXML ISAPI dbobject 查詢來達成。 此查詢必須提供足夠的資訊才能識別影像。 這類資訊可能包含主索引鍵資料行。

## <a name="column-alias"></a>資料行別名

當您查詢檢視並使用 FOR XML AUTO 模式時，請勿使用二進位資料行的別名。 若您使用別名，則會以二進位資料的 URL 編碼傳回別名。 在後續作業中，該別名不具任何意義。 無意義的別名和 URL 編碼無法用來擷取影像。

### <a name="cast-to-a-blob"></a>轉換成 BLOB

在 SELECT 查詢中，將任何資料行轉換成二進位大型物件 (BLOB) 可使資料行成為暫存實體。 BLOB 會暫時失去其相關聯的資料表名稱和資料行名稱。 這項轉換動作會使得 AUTO 模式查詢產生錯誤，因為系統不知道要將此值放入 XML 階層中的哪個位置。

例如，請考慮下表及其中一個資料列。

```sql
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)
INSERT INTO MyTable VALUES (1, 0x7);
```

下列查詢會產生錯誤，這是由於轉換成二進位大型物件 (BLOB) 所造成：

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO;
```

解決方法是將 BINARY BASE64 選項加入 FOR XML 子句中。 若將轉換移除，則查詢會產生良好的結果。

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO, BINARY BASE64;
```

預期會有下列良好的結果：

```console
<MyTable Col1="1" Col2="Bw==" />
```

## <a name="see-also"></a>另請參閱

[搭配 FOR XML 使用 AUTO 模式](../../relational-databases/xml/use-auto-mode-with-for-xml.md)
