---
title: 在 CREATE TABLE 陳述式中非 NULL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 808cddbd805db09d1b5c356d5b5af5734a5dcc16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086322"
---
# <a name="not-null-in-create-table-statements"></a>CREATE TABLE 陳述式中的 NOT NULL
某些資料庫和特別桌面的資料庫，不支援**NOT NULL**中的資料行條件約束**CREATE TABLE**陳述式。 如需詳細資訊，請參閱中的 SQL_NON_NULLABLE_COLUMNS 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。
