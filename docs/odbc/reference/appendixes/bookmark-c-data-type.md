---
title: 書簽 C 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86488da93470a61a54638e9c60e6e1795a9da4dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125748"
---
# <a name="bookmark-c-data-type"></a>書籤 C 資料類型
書簽 C 資料類型可讓應用程式抓取書簽。 書簽 C 類型僅用來抓取可以是長度可變的書簽值;它們不應該轉換成其他資料類型。 應用程式會使用**SQLBulkOperations** （具有 SQL_ADD 的作業）、 **SQLFetch**、 **SQLFetchScroll**或**SQLGetData**，從結果集的資料行0抓取書簽。 如需詳細資訊，請參閱[書簽](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
 下表列出 [書簽 C] 資料類型的 [ *CType* ] 值、實作為 [書簽 c] 資料類型的 ODBC c 資料類型，以及 SQL 的這個資料類型的定義。H.  
  
> [!NOTE]
>  SQL_C_BOOKMARK 資料類型已被取代。 ODBC *3.x*應用程式不應該使用 SQL_C_BOOKMARK。 只有當 ODBC 3.x 驅動程式想要使用使用它*的 odbc 2.x* *應用程式時*，才需要支援 SQL_C_BOOKMARK。 當應用程式*搭配 ODBC 2.x 驅動程式運作*時，驅動程式管理員會將 SQL_C_VARBOOKMARK 對應至 SQL_C_BOOKMARK。  
  
|C 類型識別碼|ODBC C typedef|C 類型|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(已被取代)|書簽|不帶正負號的 long int|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|
