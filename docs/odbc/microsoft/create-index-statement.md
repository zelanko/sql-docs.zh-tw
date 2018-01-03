---
title: "CREATE INDEX 陳述式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ca556e41216bd2f9418c2ed31369347b51efd4a9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="create-index-statement"></a>CREATE INDEX 陳述式
CREATE INDEX 陳述式的語法為：  
  
 建立 [唯一] 索引*索引名稱*ON*資料表名稱*(*資料行識別碼*[ASC] [DESC] [，*資料行識別碼*[ASC][DESC]...])與\<*索引選項清單*>  
  
 其中\<*索引選項清單*> 可以是： 主要檔案群組 &#124;不允許 NULL &#124;忽略 NULL  
  
 Microsoft Access 驅動程式會使用不允許 NULL 和 NULL 忽略索引選項。 DBASE 和 Paradox 驅動程式接受語法，但略過的其中一個選項。  
  
 使用 Paradox 驅動程式時，CREATE INDEX 陳述式會建立 Paradox 主要金鑰檔案，然後次要檔案。  
  
 這個陳述式不支援的 Microsoft Excel 或文字的驅動程式。
