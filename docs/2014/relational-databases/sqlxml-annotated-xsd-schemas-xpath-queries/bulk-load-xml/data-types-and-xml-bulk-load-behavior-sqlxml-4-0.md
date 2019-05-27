---
title: 資料型別和 XML 大量載入行為 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d2eb9af2b353760f5b195b95d6a9f9d5d1efc9b
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013420"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>資料類型與 XML 大量載入行為 (SQLXML 4.0)
  除了在下列情況下之外，在對應結構描述 (XSD 或 XDR 類型和 `sql:datatype`) 中指定的資料類型通常會遭到忽略：  
  
 在 XSD 中：  
  
-   如果類型為 `dateTime` 或 `time`，您必須指定 `sql:datatype`，因為 XML 大量載入會在將資料傳送到 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前，先執行資料轉換。  
  
-   當您大量載入的資料行`uniqueidentifier`中輸入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，而且 XSD 值是 GUID，其中包含大括號 （{和}），您必須指定**sql: datatype ="uniqueidentifier"** 移除大括號之前的值是插入資料行。 如果未指定 `sql:datatype`，值會跟著大括號傳送出去，而且插入動作會失敗。  
  
 如需詳細資訊`sql:datatype`，請參閱 <<c2> [ 資料類型強制型轉和 sql: datatype 註解&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。</c2>  
  
 在 XDR 中：  
  
-   如果 `dt:type` 為 `datetime`、`time`、`dateTime.tz` 或 `time.tz`，您必須同時指定 `dt:type` 和 `sql:datatype` 資料類型，因為 XML 大量載入會在將資料傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前，先執行資料轉換。  
  
-   如果 XML 資料型別的`uuid`，`sql:datatype`必須指定;**dt: type ="uuid"** 也是必要項，除非資料是字串資料。 如果您沒有指定 `dt:uuid`，XML 大量載入會接受包含大括號的字串 (並在需要時移除)。  
  
-   如果 XML 資料是 `bin.base64` 或 `bin.hex`，您必須使用 `dt:type` 指定 XML 資料類型。 接著，XML 大量載入會將資料載入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，做為資料的十六進位表示法。  
  
  
