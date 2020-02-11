---
title: DROP INDEX 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DROP INDEX [ODBC]
- SQL grammar [ODBC], DROP INDEX
ms.assetid: cd0ff767-9254-413b-bd1a-bed26c6774f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23823e53e516324832c79706e6171b48a9c5297c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071865"
---
# <a name="drop-index-statement"></a>DROP INDEX 陳述式
當使用 Microsoft Access、dBASE 或 Paradox 驅動程式時，DROP INDEX 語句的語法是「DROP INDEX a on b」，其中 "a" 是索引的名稱，"b" 是資料表的名稱（不是 DROP INDEX 的*索引名稱*）。  
  
 使用 Paradox 驅動程式時，DROP INDEX 語句會刪除 Paradox 次要索引檔案。  
  
 Microsoft Excel 或文字驅動程式不支援 DROP INDEX 語句。
