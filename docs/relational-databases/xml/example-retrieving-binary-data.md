---
title: 範例：擷取二進位資料 | Microsoft Docs
description: 請檢視搭配 FOR XML 子句使用 RAW 和 BINARY BASE64 選項來擷取二進位資料的 SQL 查詢範例。
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
author: RothJa
ms.author: jroth
ms.openlocfilehash: 08010e294b1b143c941774912d661a53c021a6ab
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632784"
---
# <a name="example-retrieving-binary-data"></a>範例：擷取二進位資料

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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

[搭配 FOR XML 使用 RAW 模式](../../relational-databases/xml/use-raw-mode-with-for-xml.md)
