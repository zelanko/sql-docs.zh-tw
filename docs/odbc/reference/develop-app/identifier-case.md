---
title: 識別項大小寫 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66218fb955a4133a5c689f72ab8f4b96504c9bd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="identifier-case"></a>識別項大小寫
在 SQL 陳述式和類別目錄函式引數，識別項和引號的識別碼可以是區分大小寫或不是，選取應用程式可以呼叫來判斷**SQLGetInfo** SQL_QUOTED_ SQL_IDENTIFIER_CASE 與IDENTIFIER_CASE 選項。  
  
 每個選項有四個可能的傳回值： 一個表示識別項或引號識別項的情況下機密和三個表示它不敏感。 三個值不區分大小寫的進一步說明識別碼儲存在系統目錄中的案例。 系統目錄中儲存識別碼則是只適用於顯示用途，例如當應用程式會顯示的結果目錄函數。它不會變更區分大小寫的識別項。
