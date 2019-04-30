---
title: SET NULL 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6f0e23abd31661210282967fa35080376eaaaf3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159307"
---
# <a name="set-null-command"></a>SET NULL 命令
決定如何支援 null 值的 ALTER TABLE-SQL、 CREATE TABLE-SQL 和 INSERT-SQL 命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 ON  
 （預設驅動程式; Visual FoxPro 的預設值是 OFF）。指定在使用 ALTER TABLE 和 CREATE TABLE 所建立的資料表中的所有資料行允許 null 值。 若要覆寫資料表中的資料行的 null 值支援，可以在資料行的定義包含 NOT NULL 子句。  
  
 也會指定，INSERT-SQL 會插入 null 值插入-SQL VALUE 子句中不包含任何資料行。 INSERT-SQL 會插入 null 值只允許 null 值的資料行。  
  
 OFF  
 指定在使用 ALTER TABLE 和 CREATE TABLE 所建立的資料表中的所有資料行不會允許 null 值。 您可以指定在 ALTER TABLE 和 CREATE TABLE 中的資料行的 null 值支援在資料行的定義中包含 NULL 子句。  
  
 也會指定，INSERT-SQL 會將空白值插入 INSERT-SQL VALUE 子句中不包含任何資料行。  
  
## <a name="remarks"></a>備註  
 SET NULL 會影響如何只在 null 值支援 ALTER TABLE、 CREATE TABLE 和 INSERT-SQL。 其他命令不會受到 NULL 設定。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
