---
title: 定義 UDT 資料表及資料行 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1b87e497c6610a2d75daa9432246e4f4b4690bab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153428"
---
# <a name="defining-udt-tables-and-columns"></a>定義 UDT 資料表及資料行
  一旦包含使用者定義的型別 (UDT) 的組件定義中已註冊[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫，它可以用在資料行定義。  
  
## <a name="creating-tables-with-udts"></a>建立具有 UDT 的資料表  
 在資料表中建立 UDT 資料行沒有特殊的語法。 您可以在資料行定義中使用 UDT 名稱，就像它是其中一個內部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型一樣。 下列 CREATE TABLE[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式會建立一個名為資料表**點**，具有名為資料行**識別碼**其定義為`int`身分識別資料行和 \ 資料表的主索引鍵。 第二個資料行稱為**PointValue**，資料類型為**點**。 在此範例中使用的結構描述名稱是**dbo**。 請注意，您必須具有指定結構描述名稱的必要使用權限。 如果省略了結構描述名稱，則會使用資料庫使用者的預設結構描述。  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>在 UDT 資料行上建立索引  
 索引 UDT 資料行有兩個選項：  
  
-   索引完整值。 在這種情況下，如果 UDT 按二進位排序，您就可以使用 CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，在整個 UDT 資料行上建立索引。  
  
-   索引 UDT 運算式。 您可透過 UDT 運算式在保存的計算資料行上建立索引。 UDT 運算式可以是 UDT 的欄位、方法或屬性。 該運算式必須具有決定性，且不能執行資料存取。  
  
 如需詳細資訊，請參閱 < [clr 使用者定義型別](clr-user-defined-types.md)並[CREATE INDEX &#40;-&#41;](/sql/t-sql/statements/create-index-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [在 SQL Server 中使用使用者定義型別](working-with-user-defined-types-in-sql-server.md)  
  
  
