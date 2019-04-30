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
ms.openlocfilehash: e40947dc4dbad0830444870ea7e2d0c663490b25
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188965"
---
# <a name="fixed-length-bookmarks"></a>固定長度書籤
如果 ODBC 3 *.x*驅動程式應該使用 ODBC 2。*x*應用程式會使用固定長度書籤，驅動程式必須支援下列：  
  
-   SQL_UB_ON 為 SQL_USE_BOOKMARKS 陳述式選項的值。 (在 ODBC 3 已被取代 SQL_UB_ON *.x*。)  
  
-   SQL_GET_BOOKMARK 陳述式選項中。
