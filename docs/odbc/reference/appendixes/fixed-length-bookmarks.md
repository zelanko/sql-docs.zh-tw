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
ms.openlocfilehash: 5877a6cb7a99803f854338321e333c87037c2e90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913578"
---
# <a name="fixed-length-bookmarks"></a>固定長度書籤
如果 ODBC *3.x*驅動程式應該使用 ODBC *2.x*應用程式會使用固定長度書籤，驅動程式必須支援下列：  
  
-   SQL_UB_ON 為 SQL_USE_BOOKMARKS 陳述式選項的值。 (在 ODBC 中已被取代 SQL_UB_ON *3.x*。)  
  
-   SQL_GET_BOOKMARK 陳述式選項中。
