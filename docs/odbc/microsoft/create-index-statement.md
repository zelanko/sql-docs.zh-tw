---
title: CREATE INDEX 陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61d1532e457748b432e5aa14a55e9e68b4486c9c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-index-statement"></a>CREATE INDEX 陳述式
CREATE INDEX 陳述式的語法為：  
  
 建立 [唯一] 索引*索引名稱*ON*資料表名稱*(*資料行識別碼*[ASC] [DESC] [，*資料行識別碼*[ASC][DESC]...])與\<*索引選項清單*>  
  
 其中\<*索引選項清單*> 可以是： 主要&#124;不允許 NULL&#124;忽略 NULL  
  
 Microsoft Access 驅動程式會使用不允許 NULL 和 NULL 忽略索引選項。 DBASE 和 Paradox 驅動程式接受語法，但略過的其中一個選項。  
  
 使用 Paradox 驅動程式時，CREATE INDEX 陳述式會建立 Paradox 主要金鑰檔案，然後次要檔案。  
  
 這個陳述式不支援的 Microsoft Excel 或文字的驅動程式。
