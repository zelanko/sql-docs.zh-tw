---
description: 支援的資料類型
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
ms.openlocfilehash: 349636553112449485d99fed269a43069974fccf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385824"
---
# <a name="supported-data-types"></a>支援的資料類型
Dbms 所支援的資料類型會有相當大的差異。 應用程式可以藉由呼叫 **SQLGetTypeInfo**來判斷所支援資料類型的名稱和特性。 由於資料類型名稱的變化很大，因此應用程式必須使用**CREATE TABLE**語句中的**SQLGetTypeInfo**所傳回的資料類型名稱。 如需詳細資訊，請參閱 [ODBC 中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。
