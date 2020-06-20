---
title: 定義 UDT 資料表和資料行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: aa9596629ed8b4877b1793fa0c56956c52989499
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954538"
---
# <a name="defining-udt-tables-and-columns"></a>定義 UDT 資料表及資料行
  一旦包含使用者定義型別（UDT）定義的元件已經在資料庫中註冊之後 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，就可以在資料行定義中使用。  
  
## <a name="creating-tables-with-udts"></a>建立具有 UDT 的資料表  
 在資料表中建立 UDT 資料行沒有特殊的語法。 您可以在資料行定義中使用 UDT 名稱，就像它是其中一個內部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型一樣。 下列 CREATE TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句會建立名為**Points**的資料表，其中包含名為**ID**的資料行，該資料行會定義為 `int` 識別欄位，而是資料表的主鍵。 第二個數據行的名稱為**PointValue**，其資料類型為**Point**。 此範例中使用的架構名稱為**dbo**。 請注意，您必須具有指定結構描述名稱的必要使用權限。 如果省略了結構描述名稱，則會使用資料庫使用者的預設結構描述。  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>在 UDT 資料行上建立索引  
 索引 UDT 資料行有兩個選項：  
  
-   索引完整值。 在這種情況下，如果 UDT 按二進位排序，您就可以使用 CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，在整個 UDT 資料行上建立索引。  
  
-   索引 UDT 運算式。 您可透過 UDT 運算式在保存的計算資料行上建立索引。 UDT 運算式可以是 UDT 的欄位、方法或屬性。 該運算式必須具有決定性，且不能執行資料存取。  
  
 如需詳細資訊，請參閱[CLR 使用者定義類型](clr-user-defined-types.md)和[CREATE INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/create-index-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server 中的使用者定義型別](working-with-user-defined-types-in-sql-server.md)  
  
  
