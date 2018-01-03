---
title: "泛型應用程式 |Microsoft 文件"
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
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 471cceb31dfec36cde45185d3d472aba3100b4da
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="generic-applications"></a>泛型應用程式
泛型應用程式有時會執行硬式編碼工作，例如試算表從資料庫擷取資料。 它們也可能會執行各種不同的使用者定義的工作，例如允許使用者輸入並執行 SQL 陳述式的一般查詢應用程式。 什麼泛型應用程式具有共通點是，它們必須使用各種不同的 Dbms 和，開發人員不知道事先這些 Dbms 將會。  
  
 因此，泛型應用程式必須具備高度互通性。 開發人員必須許多的選擇來換取互通性功能，而必須撰寫程式碼預期驅動程式支援各種不同的功能。 雖然泛型應用程式可能會調整為使用熱門 Dbms，它們很少會包含特定驅動程式或 DBMS 專屬的程式碼。
