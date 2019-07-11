---
title: 固定長度書籤 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21af6ef1be21e000d25582151650f274fe3561a4
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793376"
---
# <a name="fixed-length-bookmarks"></a>固定長度書籤
如果 ODBC *3.x*驅動程式應該使用 ODBC *2.x*應用程式會使用固定長度書籤，驅動程式必須支援下列：  
  
-   SQL_UB_ON 為 SQL_USE_BOOKMARKS 陳述式選項的值。 (在 ODBC 中已被取代 SQL_UB_ON *3.x*。)  
  
-   SQL_GET_BOOKMARK 陳述式選項中。
