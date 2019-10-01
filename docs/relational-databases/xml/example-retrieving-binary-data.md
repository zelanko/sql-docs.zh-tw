---
title: 範例擷取二進位資料 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: c168c76d33ac90bc658fad86404aea45b322d037
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199466"
---
# <a name="example-retrieving-binary-data"></a>範例擷取二進位資料

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

下列查詢會傳回儲存在 **varbinary(max)** 類型資料行中的產品相片。 在查詢中指定 `BINARY BASE64` 選項，以便將二進位資料透過 Base64 編碼格式傳回。

## <a name="example"></a>範例

```sql
USE AdventureWorks2012;
GO
SELECT ProductPhotoID, ThumbNailPhoto
FROM Production.ProductPhoto
WHERE ProductPhotoID=1
FOR XML RAW, BINARY BASE64 ;
GO
```

預期會有下列結果：

```console
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>
```

## <a name="see-also"></a>另請參閱

[使用 FOR XML 的 RAW 模式](../../relational-databases/xml/use-raw-mode-with-for-xml.md)
