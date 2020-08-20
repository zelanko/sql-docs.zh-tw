---
description: 引號識別碼
title: 引號識別碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd317e5d92618d8b458d6d28fa870c6945e136fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465678"
---
# <a name="quoted-identifiers"></a>引號識別碼
在 SQL 語句中，包含特殊字元或符合關鍵字的識別碼必須以 *識別碼引號字元*括住;以這類字元括住的識別碼稱為 *引號識別碼* (在 SQL-92) 中也稱為 *分隔識別碼* 。 例如，在下列 **SELECT** 語句中，帳戶應付的識別碼會以引號括住：  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 引號識別碼的原因是讓語句剖析或是。 例如，如果在上一個語句中未將應付的帳戶加上引號，剖析器會假設有兩個數據表、帳戶和應付帳款，並傳回未以逗號分隔的語法錯誤。 識別碼引號字元是驅動程式專屬字元，並且會使用 **SQLGetInfo**中的 SQL_IDENTIFIER_QUOTE_CHAR 選項取出。 系統會使用 **SQLGetInfo**中的 SQL_SPECIAL_CHARACTERS 和 SQL_KEYWORDS 選項來抓取特殊字元和關鍵字的清單。  
  
 為了安全起見，可互通的應用程式通常會將所有識別碼括住，除了虛擬資料行（例如 Oracle 中的 ROWID 資料行）之外。 **SQLSpecialColumns** 會傳回虛擬資料行的清單。 此外，如果在物件名稱中出現特殊字元的應用程式特定限制，則最好讓互通的應用程式不使用這些位置中的特殊字元。
