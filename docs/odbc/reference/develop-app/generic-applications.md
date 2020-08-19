---
description: 泛型應用程式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9980edcaf34182b4c7f43aa8e935d095f2345138
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476680"
---
# <a name="generic-applications"></a>泛型應用程式
一般應用程式有時會執行硬式編碼的工作，例如從資料庫抓取資料的試算表。 它們也可能會執行各種使用者定義的工作，例如可讓使用者輸入和執行 SQL 語句的一般查詢應用程式。 一般應用程式的常見情況是，它們必須使用各種不同的 Dbms，而且開發人員不會事先知道這些 Dbms 是什麼。  
  
 因此，一般應用程式必須具有高度互通性。 開發人員必須進行許多選擇、交易功能的互通性，而且必須撰寫程式碼來預期驅動程式支援各種功能。 雖然一般應用程式可能會調整以搭配熱門的 Dbms 使用，但很少會包含驅動程式特定或 DBMS 特定的程式碼。
