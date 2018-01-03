---
title: "固定長度的書籤 |Microsoft 文件"
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
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0b12009618489863c856d9b29433ff5146210ea
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="fixed-length-bookmarks"></a>固定長度的書籤
如果 ODBC 3*.x*驅動程式應該可以搭配 ODBC 2。*x*應用程式會使用固定長度的書籤，驅動程式必須支援下列：  
  
-   SQL_UB_ON SQL_USE_BOOKMARKS 陳述式選項的值。 (在 ODBC 3 已被取代 SQL_UB_ON*.x*。)  
  
-   SQL_GET_BOOKMARK 陳述式選項。
