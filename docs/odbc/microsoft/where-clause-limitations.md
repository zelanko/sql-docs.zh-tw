---
description: WHERE 子句限制
title: WHERE 子句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b6b9e72176f447c71daccfbd0393f414558d49d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466280"
---
# <a name="where-clause-limitations"></a>WHERE 子句限制
WHERE 子句中的子句數目上限為40。  
  
 LONGVARBINARY 和 LONGVARCHAR 資料行可以與長度最多為255個字元的常值進行比較，但無法使用參數進行比較。
