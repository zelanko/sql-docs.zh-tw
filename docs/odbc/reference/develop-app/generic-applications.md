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
ms.openlocfilehash: f6b1544f5562468db03a649c263993039a722a3c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139302"
---
# <a name="generic-applications"></a>泛型應用程式
一般應用程式有時會執行硬式編碼的工作，例如從資料庫中抓取資料的試算表。 它們也可能會執行各種使用者定義的工作，例如一般查詢應用程式，可讓使用者輸入和執行 SQL 語句。 一般應用程式常見的情況是，它們必須使用各種不同的 Dbms，而開發人員並不事先知道這些 Dbms 將會是什麼。  
  
 因此，泛型應用程式必須具有高度互通性。 開發人員必須進行許多選擇，並針對功能的互通性進行取捨，而且必須撰寫程式碼，以預期驅動程式支援各種功能。 雖然泛型應用程式可能會調整為使用熱門的 Dbms，但很少會包含驅動程式特定或 DBMS 特定的程式碼。
