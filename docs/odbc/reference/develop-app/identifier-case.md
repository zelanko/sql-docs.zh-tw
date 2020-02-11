---
title: 識別碼案例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70728908f081ab89e08cad1265f04394f29b66ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138967"
---
# <a name="identifier-case"></a>識別碼大小寫
在 SQL 語句和類別目錄函式引數中，識別碼和引號識別碼可以區分大小寫，而應用程式可以藉由使用 SQL_IDENTIFIER_CASE 和 SQL_QUOTED_IDENTIFIER_CASE 選項呼叫**SQLGetInfo**來判斷。  
  
 每個選項都有四個可能的傳回值：一個表示識別碼或引號識別碼的大小寫區分，而三個表示不區分。 不區分大小寫的三個值會進一步描述在系統目錄中儲存識別碼的情況。 識別碼在系統目錄中的儲存方式僅與顯示用途有關，例如當應用程式顯示目錄函數的結果時。它不會變更識別碼的區分大小寫。
