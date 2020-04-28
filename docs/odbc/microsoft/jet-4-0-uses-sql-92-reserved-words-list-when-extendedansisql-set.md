---
title: 當 ExtendedAnsiSQL_Set 時，Jet 4.0 會使用 SQL-92 保留字清單 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6988e0da1ecb881e0f6e88e35b66f1a6284f9b7a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299958"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisql_set"></a>Jet 4.0 在 ExtendedAnsiSQL_Set 時使用 SQL-92 保留字清單
當 ExtendedAnsiSQL 旗標開啟時，Jet 4.0 會使用 SQL-92 保留字清單。 嘗試使用 SQL-92 保留字當做未加引號的物件名稱時，將會產生語法錯誤。 當 ExtendedAnsiSQL 旗標關閉時，新的保留字可以像之前一樣用來當做物件名稱。
