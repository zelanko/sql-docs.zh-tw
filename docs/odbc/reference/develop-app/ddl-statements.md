---
description: DDL 陳述式
title: DDL 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 395abe3eed64f37c000ecff6f0b68a6e0cb1d076
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424730"
---
# <a name="ddl-statements"></a>DDL 陳述式
資料定義語言 (DDL) 語句在 Dbms 之間有極大的差異。 ODBC SQL 會針對最常見的資料定義作業定義語句：建立和卸載資料表、索引和視圖;改變數據表;以及授與及撤銷許可權。 所有其他 DDL 語句都是資料來源特有的。 因此，互通的應用程式無法執行某些資料定義作業。 一般來說，這並不是問題，因為這類作業通常是高度 DBMS 專屬的，而且最好留給隨附于大部分 Dbms 或驅動程式隨附之安裝程式的專屬資料庫管理軟體。  
  
 資料定義中的另一個問題是，資料類型名稱在 Dbms 之間有極大的差異。 **SQLGetTypeInfo**可讓應用程式探索 dbms 特定的資料類型名稱，而不是定義標準資料類型名稱，以及強制驅動程式將它們轉換成 dbms 特定的名稱。 互通的應用程式應該在 SQL 語句中使用這些名稱來建立和改變數據表; [附錄 C： SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)和 [附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)中所列的名稱僅為範例。
