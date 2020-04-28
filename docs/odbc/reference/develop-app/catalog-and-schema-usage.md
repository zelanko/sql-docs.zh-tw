---
title: 目錄和架構使用方式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 245bd007f070a94689283830ba7a1362e31353e6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306249"
---
# <a name="catalog-and-schema-usage"></a>目錄和結構描述的使用方式
資料來源不一定支援目錄和架構名稱，做為所有 SQL 語句中的物件名稱識別碼。 資料來源可能支援下列一或多個 SQL 語句類別中的目錄和架構名稱：資料操作語言（DML）語句、程序呼叫、資料表定義語句、索引定義語句和許可權定義語句。 為了判斷可以使用目錄和架構名稱的 SQL 語句類別，應用程式會使用 SQL_CATALOG_USAGE 和 SQL_SCHEMA_USAGE 選項來呼叫**SQLGetInfo** 。
