---
title: SET Null 命令 |Microsoft Docs
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
ms.openlocfilehash: 9f8addb9b4c7c200ee8f213bdd959067039ccfff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063675"
---
# <a name="set-null-command"></a>SET NULL 命令
決定 ALTER TABLE-SQL、CREATE TABLE SQL 和 INSERT-SQL 命令如何支援 null 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 （驅動程式的預設值; Visual FoxPro 的預設值為 OFF）。指定以 ALTER TABLE 和 CREATE TABLE 建立之資料表中的所有資料行都允許 null 值。 您可以在資料行的定義中包含 NOT Null 子句，以覆寫資料表中資料行的 null 值支援。  
  
 此外，也指定 INSERT-SQL 會將 null 值插入至不包含在 INSERT-SQL VALUE 子句中的任何資料行。 INSERT-SQL 只會將 null 值插入允許 null 值的資料行。  
  
 OFF  
 指定以 ALTER TABLE 和 CREATE TABLE 建立之資料表中的所有資料行，都不允許 null 值。 您可以藉由在資料行的定義中包含 Null 子句，為 ALTER TABLE 和 CREATE TABLE 中的資料行指定 null 值支援。  
  
 此外，也指定 INSERT-SQL 會將空白值插入至不包含在 INSERT-SQL VALUE 子句中的任何資料行。  
  
## <a name="remarks"></a>備註  
 SET Null 只會影響 ALTER TABLE、CREATE TABLE 和 INSERT SQL 支援 Null 值的方式。 其他命令不會受到 SET Null 的影響。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
