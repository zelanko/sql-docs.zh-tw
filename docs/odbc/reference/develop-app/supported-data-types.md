---
title: 支援的資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5ec0f3943fd52540f094a23e9b3f9f3886e1371
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114083"
---
# <a name="supported-data-types"></a>支援的資料類型
Dbms 支援的資料類型會有相當大的差異。 應用程式可以藉由呼叫**SQLGetTypeInfo**來判斷支援的資料類型的名稱和特性。 由於資料類型名稱的差異很大，因此應用程式必須使用**SQLGetTypeInfo**在**CREATE TABLE**語句中所傳回的資料類型名稱。 如需詳細資訊，請參閱[ODBC 中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。
