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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 638bae6491c020519a0123ff56fe31e9a9ca1cf7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303429"
---
# <a name="drop-index-statement"></a>DROP INDEX 陳述式
當使用 Microsoft Access、dBASE 或 Paradox 驅動程式時，DROP INDEX 語句的語法是「DROP INDEX a on b」，其中 "a" 是索引的名稱，"b" 是資料表的名稱（不是 DROP INDEX 的*索引名稱*）。  
  
 使用 Paradox 驅動程式時，DROP INDEX 語句會刪除 Paradox 次要索引檔案。  
  
 Microsoft Excel 或文字驅動程式不支援 DROP INDEX 語句。
