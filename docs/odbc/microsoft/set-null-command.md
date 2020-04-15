---
title: 設定 NULL 指令 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c83c9ef9f8a0ce143308b73d8df09b05fb2cdea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300808"
---
# <a name="set-null-command"></a>SET NULL 命令
確定 ALTER TABLE - SQL、建立表 - SQL 和 INSERT - SQL 命令支援空值的方式。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 (驅動程式的預設值;Visual FoxPro 的預設值為 OFF。指定使用 ALTER TABLE 和 CREATE TABLE 建立的表中的所有列都將允許空值。 通過在列的定義中包括"非 NULL"子句,可以覆蓋表中列的 null 支援。  
  
 還指定 INSERT - SQL 將在插入插入插入 - SQL VALUE 子句中未包括的任何列中。 INSERT - SQL 將僅將空值插入允許空值的列中。  
  
 OFF  
 指定使用 ALTER TABLE 和 CREATE TABLE 建立的表中的所有列都不允許為空值。 通過在列的定義中包括 NULL 子句,可以為 ALTER TABLE 和 CREATE TABLE 中的列指定空值支援。  
  
 還指定 INSERT - SQL 將在插入「插入 - SQL VALUE」子句中未包括的任何列中插入空白值。  
  
## <a name="remarks"></a>備註  
 設置 NULL 僅影響 ALTER TABLE、創建表和插入 - SQL 支援空值的方式。 其他命令不受 SET NULL 的影響。  
  
## <a name="see-also"></a>另請參閱  
 [變更表 - SQL 指令](../../odbc/microsoft/alter-table-sql-command.md)   
 [建立表 - SQL 指令](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
