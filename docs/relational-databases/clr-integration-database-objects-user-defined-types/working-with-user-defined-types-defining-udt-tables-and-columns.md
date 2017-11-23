---
title: "定義 UDT 資料表及資料行 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs: TSQL
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
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1157aea65f3a1802743d1831b2299e4e999a5b5b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="working-with-user-defined-types---defining-udt-tables-and-columns"></a>使用使用者定義型別為定義 UDT 資料表及資料行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]一旦包含使用者定義型別 (UDT) 的組件定義已經註冊在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫，才能使用資料行定義中。  
  
## <a name="creating-tables-with-udts"></a>建立具有 UDT 的資料表  
 在資料表中建立 UDT 資料行沒有特殊的語法。 您可以在資料行定義中使用 UDT 名稱，就像它是其中一個內部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型一樣。 下列 CREATE TABLE[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式會建立名為**點**，具有名為資料行**識別碼**其定義為**int**識別資料行，資料表的主索引鍵。 第二個資料行名為**PointValue**，資料類型為**點**。 在此範例中使用的結構描述名稱是**dbo**。 請注意，您必須具有指定結構描述名稱的必要使用權限。 如果省略了結構描述名稱，則會使用資料庫使用者的預設結構描述。  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>在 UDT 資料行上建立索引  
 索引 UDT 資料行有兩個選項：  
  
-   索引完整值。 在這種情況下，如果 UDT 按二進位排序，您就可以使用 CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，在整個 UDT 資料行上建立索引。  
  
-   索引 UDT 運算式。 您可透過 UDT 運算式在保存的計算資料行上建立索引。 UDT 運算式可以是 UDT 的欄位、方法或屬性。 該運算式必須具有決定性，且不能執行資料存取。  
  
 如需詳細資訊，請參閱[clr 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)和[CREATE INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>請參閱＜  
 [在 SQL Server 中使用使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
  
  
