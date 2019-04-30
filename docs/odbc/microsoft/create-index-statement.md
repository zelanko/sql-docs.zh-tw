---
title: CREATE INDEX Statement | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 93ddc3881796aee3194ec5268afc68ecbab1a487
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232994"
---
# <a name="create-index-statement"></a>CREATE INDEX 陳述式
CREATE INDEX 陳述式的語法是：  
  
 建立 [UNIQUE] 的索引*的索引名稱*ON*資料表名稱*(*資料行識別碼*[ASC] [DESC] [，*資料行識別碼*[ASC][DESC]...])具有\<*索引選項清單*>  
  
 何處\<*的索引選項清單*> 可以是：PRIMARY &#124; DISALLOW NULL &#124; IGNORE NULL  
  
 Microsoft Access 驅動程式會使用不允許 NULL] 和 [略過空值的索引選項。 DBASE 和 Paradox 驅動程式接受的語法，但忽略的其中一個選項存在。  
  
 使用 Paradox 驅動程式時，CREATE INDEX 陳述式會建立 Paradox 的主要金鑰檔案，然後次要檔案。  
  
 Microsoft Excel 或文字驅動程式不支援此陳述式。
