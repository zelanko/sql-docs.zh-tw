---
description: LIKE 述詞逸出字元
title: LIKE 述詞 Escape 字元 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5304068e21dd6faf0e737a94add0cce177c4dabc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476550"
---
# <a name="like-predicate-escape-character"></a>LIKE 述詞逸出字元
在 **LIKE** 述詞中，百分比符號 (% ) 符合任何字元的零或多個字元，而底線 (_) 符合任何一個字元。 若要比對 **LIKE** 述詞中的實際百分比符號或底線，則 escape 字元必須在百分比符號或底線之前。 定義 **LIKE** 述詞 escape 字元的 escape 序列為：  
  
 **{escape '** *escape-character* **'}**  
  
 其中， *escape 字元* 是資料來源所支援的任何字元。  
  
 如需類似 escape 順序的詳細資訊，請參閱附錄 C： SQL 文法中的 [Like Escape sequence](../../../odbc/reference/appendixes/like-escape-sequence.md) 。  
  
 例如，下列 SQL 語句會建立一組以字元 "% AAA" 開頭之客戶名稱的相同結果集。 第一個語句使用 escape 序列語法。 第二個語句使用 Microsoft®存取的原生語法，而且無法互通。 請注意，每個 **LIKE** 述詞中的第二個百分比字元是符合任何字元零或多個字元的萬用字元。  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 為了判斷資料來源是否支援 **LIKE** 述詞 escape 字元，應用程式會使用 SQL_LIKE_ESCAPE_CLAUSE 選項來呼叫 **SQLGetInfo** 。
