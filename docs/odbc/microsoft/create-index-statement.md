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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6aa512ff789fcbd00f45f84fb194d4ab3f5da07
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280968"
---
# <a name="create-index-statement"></a>CREATE INDEX 陳述式
CREATE INDEX 語句的語法如下：  
  
 建立 [唯一] 索引*索引-* *資料表名稱*上的名稱（資料*行識別碼*[asc] [desc] [，資料*行識別碼*[asc] [desc] ...]）\<*索引選項清單*>  
  
 \<*索引選項清單*> 可以是：主要 &#124; 不允許 null &#124; 忽略 null  
  
 只有 Microsoft Access 驅動程式會使用 [不允許 Null] 和 [忽略 Null 索引] 選項。 DBASE 和 Paradox 驅動程式會接受語法，但忽略任一選項的存在。  
  
 使用 Paradox 驅動程式時，CREATE INDEX 語句會建立 Paradox 主要金鑰檔案和次要檔案。  
  
 Microsoft Excel 或文字驅動程式不支援此語句。
