---
title: 一般應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59110f66c512845ff5ce1f2f246c05c63fa755b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751282"
---
# <a name="generic-applications"></a>泛型應用程式
一般應用程式有時會執行硬式編碼工作，例如從資料庫擷取資料的試算表。 它們可能也會執行各種不同的使用者定義的工作，例如允許使用者輸入並執行 SQL 陳述式的一般查詢應用程式。 什麼一般的應用程式的共通是它們必須使用各種不同的 Dbms 和，開發人員不事前不知道這些 Dbms 會有什麼。  
  
 因此，一般的應用程式必須要高度互通。 開發人員必須做出許多的選擇，互通性功能，來換取，因而必須寫程式碼預期驅動程式，以支援各種不同的功能。 雖然泛型應用程式可能會進行微調，以使用受歡迎的 Dbms，它們很少會包含特定驅動程式或 DBMS 專屬的程式碼。
