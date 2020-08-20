---
description: 識別碼大小寫
title: 識別碼案例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ccac9b10e6a32c7265cd5f591944735454b85f80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461440"
---
# <a name="identifier-case"></a>識別碼大小寫
在 SQL 語句和目錄函式引數中，識別碼和引號識別碼可以區分大小寫，而應用程式可以藉由呼叫 **SQLGetInfo** 與 SQL_IDENTIFIER_CASE 和 SQL_QUOTED_IDENTIFIER_CASE 選項來判斷。  
  
 這些選項中的每一個都有四個可能的傳回值：一個表示識別碼或引號識別碼區分大小寫，而三個則表示不區分大小寫。 不區分大小寫的三個值會進一步描述識別碼儲存在系統目錄中的情況。 識別碼儲存在系統目錄中的方式僅與顯示用途相關，例如當應用程式顯示目錄函式的結果時：它不會變更識別碼的區分大小寫。
