---
title: 執行目錄函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9c50bbb813c0aad7ae8d9a531458b2999dcae86f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="executing-catalog-functions"></a>執行目錄函數
目錄函式建立結果集，因為它相當於執行任何結果集 – 產生 SQL 陳述式。 事實上，目錄函數通常會執行預先定義的 SQL 陳述式或呼叫預先定義的程序所隨附的驅動程式或 DBMS 實作。 幾乎所有項目，適用於建立結果集的 SQL 陳述式也適用於目錄函數。 例如，SQL_ATTR_MAX_ROWS 陳述式屬性會限制類別目錄函式所傳回的資料列數目就如同它會限制傳回的資料列數目**選取**陳述式。  
  
 若要執行目錄函數，應用程式只會呼叫此函式。  
  
 如需目錄函數的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。
