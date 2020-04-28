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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d19cde2d531819a60229dd7a780181571e169503
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307779"
---
# <a name="supported-data-types"></a>支援的資料類型
Dbms 支援的資料類型會有相當大的差異。 應用程式可以藉由呼叫**SQLGetTypeInfo**來判斷支援的資料類型的名稱和特性。 由於資料類型名稱的差異很大，因此應用程式必須使用**SQLGetTypeInfo**在**CREATE TABLE**語句中所傳回的資料類型名稱。 如需詳細資訊，請參閱[ODBC 中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。
