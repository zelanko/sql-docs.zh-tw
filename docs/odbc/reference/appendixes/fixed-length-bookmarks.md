---
title: 固定長度的書籤 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b90454f8ecfa48081d17a71c63cc9f4ae670b4ff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="fixed-length-bookmarks"></a>固定長度的書籤
如果 ODBC 3 *.x*驅動程式應該可以搭配 ODBC 2。*x*應用程式會使用固定長度的書籤，驅動程式必須支援下列：  
  
-   SQL_UB_ON SQL_USE_BOOKMARKS 陳述式選項的值。 (在 ODBC 3 已被取代 SQL_UB_ON *.x*。)  
  
-   SQL_GET_BOOKMARK 陳述式選項。
