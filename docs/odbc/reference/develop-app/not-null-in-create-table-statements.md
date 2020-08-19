---
description: CREATE TABLE 陳述式中的 NOT NULL
title: CREATE TABLE 語句中的 NOT Null |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92d066ebb4bd6b712acaa71e0e752b3f0f27a3df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429220"
---
# <a name="not-null-in-create-table-statements"></a>CREATE TABLE 陳述式中的 NOT NULL
某些資料庫（尤其是桌面資料庫）不支援**CREATE TABLE**語句中的**not Null**資料行條件約束。 如需詳細資訊，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函數描述中的 SQL_NON_NullABLE_COLUMNS 選項。
