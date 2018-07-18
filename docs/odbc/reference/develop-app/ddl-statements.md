---
title: DDL 陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d077c86fb7a87658bc62d9530e9019e9f25da987
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909173"
---
# <a name="ddl-statements"></a>DDL 陳述式
資料定義語言 (DDL) 陳述式而異 Dbms 極大的差異。 ODBC SQL 定義陳述式中的最常見的資料定義作業： 建立和卸除資料表、 索引和檢視。改變資料表。授與及撤銷權限。 所有其他 DDL 陳述式是資料來源專用。 因此，可互通的應用程式無法執行某些資料定義作業。 一般情況下，這不是問題，因為這類作業通常高度 DBMS 的特定最左邊，專屬資料庫管理軟體隨附大部分 Dbms 或安裝程式隨附的驅動程式。  
  
 在資料定義中的另一個問題是該名稱可大幅異 Dbms 的資料類型。 而不是定義標準的資料型別名稱，並強制驅動程式將它們轉換成特定 DBMS 的名稱， **SQLGetTypeInfo**提供方法，讓應用程式可以探索 DBMS 專屬資料型別名稱。 互通的應用程式應該使用 SQL 陳述式中這些名稱來建立和變更資料表。所列的名稱[附錄 c: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)，和[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)，只是範例。
