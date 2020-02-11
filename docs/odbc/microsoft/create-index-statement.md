---
title: CREATE INDEX 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad15ad436b0f34f00acbd75e371e998183f22d2f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081914"
---
# <a name="create-index-statement"></a>CREATE INDEX 陳述式
CREATE INDEX 語句的語法如下：  
  
 建立 [唯一] 索引*索引-* *資料表名稱*上的名稱（資料*行識別碼*[asc] [desc] [，資料*行識別碼*[asc] [desc] ...]）\<*索引選項清單*>  
  
 \<*索引選項清單*> 可以是：主要 &#124; 不允許 null &#124; 忽略 null  
  
 只有 Microsoft Access 驅動程式會使用 [不允許 Null] 和 [忽略 Null 索引] 選項。 DBASE 和 Paradox 驅動程式會接受語法，但忽略任一選項的存在。  
  
 使用 Paradox 驅動程式時，CREATE INDEX 語句會建立 Paradox 主要金鑰檔案和次要檔案。  
  
 Microsoft Excel 或文字驅動程式不支援此語句。
