---
title: 定義 UDT 表和列 |微軟文件
description: 註冊包含 UDT 定義的程式集後,可以在列定義中使用它。
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [CLR integration], columns
- UDTs [CLR integration], columns
- columns [CLR integration]
- user-defined types [CLR integration], tables
- tables [CLR integration]
- UDTs [CLR integration], tables
- UDTs [CLR integration], indexes
- user-defined types [CLR integration], indexes
- indexes [CLR integration]
ms.assetid: aea495f4-ce26-4952-b019-38f012625f3f
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f46ebc5089a4cb2fdb974df52d9bc876f925da4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486889"
---
# <a name="working-with-user-defined-types---defining-udt-tables-and-columns"></a>使用使用者定義型別 - 定義 UDT 資料表及資料行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫中註冊了包含使用者定義類型 (UDT) 定義的程式集後,可以在列定義中使用。 如需詳細資訊，請參閱 [CREATE TYPE (TRANSACT-SQL)](../../t-sql/statements/create-type-transact-sql.md)。  
  
## <a name="creating-tables-with-udts"></a>建立具有 UDT 的資料表  
 在資料表中建立 UDT 資料行沒有特殊的語法。 您可以在資料行定義中使用 UDT 名稱，就像它是其中一個內部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型一樣。 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]CREATE TABLE 語句建立名為 **「點**」的表,該列名為**ID,** 該列定義為**int**識別列和表的主鍵。 第二列名為**PointValue,** 資料型態為**Point**。 此範例中使用的架構名稱是**dbo**。 請注意，您必須具有指定結構描述名稱的必要使用權限。 如果省略了結構描述名稱，則會使用資料庫使用者的預設結構描述。  
  
```sql  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>在 UDT 資料行上建立索引  
 索引 UDT 資料行有兩個選項：  
  
-   **索引完整值。** 在這種情況下，如果 UDT 按二進位排序，您就可以使用 CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，在整個 UDT 資料行上建立索引。  
  
-   **索引 UDT 運算式。** 您可透過 UDT 運算式在保存的計算資料行上建立索引。 UDT 運算式可以是 UDT 的欄位、方法或屬性。 該運算式必須具有決定性，且不能執行資料存取。  
  
 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL 伺服器中的使用者定義類型](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)     
 [建立類型(轉算 SQL)](../../t-sql/statements/create-type-transact-sql.md)     
 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)     
