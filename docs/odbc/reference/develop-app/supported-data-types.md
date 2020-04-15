---
title: 支援的資料型態 :微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307779"
---
# <a name="supported-data-types"></a>支援的資料類型
DBMS 支持的數據類型差異很大。 應用程式可以通過調用**SQLGetTypeInfo**來確定受支援的數據類型的名稱和特徵。 由於資料類型名稱差異很大,應用程式必須在**CREATE TABLE**語句中使用**SQLGetTypeInfo**傳回的資料類型名稱。 有關詳細資訊,請參閱[ODBC 中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。
