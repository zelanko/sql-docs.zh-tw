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
manager: craigg
ms.openlocfilehash: 2a8848bad9d27dfd9318b725b77203706d3dfd5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149091"
---
# <a name="supported-data-types"></a>支援的資料類型
支援的 Dbms 的資料類型的變化相當大。 應用程式可以藉由呼叫判斷名稱和支援的資料類型的特性**SQLGetTypeInfo**。 由於資料型別名稱中的各種變化，應用程式必須使用所傳回的資料類型名稱**SQLGetTypeInfo**中**CREATE TABLE**陳述式。 如需詳細資訊，請參閱 < [ODBC 中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。
