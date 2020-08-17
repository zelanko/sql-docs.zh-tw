---
description: DELETE 陳述式限制
title: DELETE 子句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ffb3a6d0ab28fc2b8bc8785df586ac6bbc86aa0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340894"
---
# <a name="delete-statement-limitations"></a>DELETE 陳述式限制
Microsoft Excel 或 Text 驅動程式不支援 DELETE 子句。 請注意，Text 驅動程式支援 INSERT 語句。  
  
 DBASE 驅動程式不支援封裝資料表來移除「已刪除」的值。  
  
 若要從資料表中刪除資料列的 Paradox 驅動程式，資料表必須有唯一的索引， (Paradox primary key) 。
