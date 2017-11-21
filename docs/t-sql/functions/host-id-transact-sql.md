---
title: "HOST_ID (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HOST_ID
- HOST_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], workstations
- HOST_ID function
- workstation IDs [SQL Server]
- identification numbers [SQL Server], workstations
ms.assetid: 36ba56d4-20d7-4cd1-aa2a-e40a6c0a4e39
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0cf562d5e9eb868494245ba561e77aa7546d83ad
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="hostid-transact-sql"></a>HOST_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回工作站識別碼。 工作站識別碼是用戶端電腦上，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之應用程式的處理序識別碼 (PID)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
HOST_ID ()  
```  
  
## <a name="return-types"></a>傳回類型  
 **char （10)**  
  
## <a name="remarks"></a>備註  
 當系統函數的參數是選擇性時，就會假設使用目前資料庫、主機電腦、伺服器使用者或資料庫使用者。 內建函數後面一律必須接著括號。  
  
 系統函數可以用於選取清單、WHERE 子句以及任何可以使用運算式的位置。  
  
## <a name="examples"></a>範例  
 下列範例會建立一份資料表，利用 `HOST_ID()` 定義中的 `DEFAULT` 來記錄電腦的終端機識別碼，這些電腦會將資料列插入記錄訂單的資料表中。  
  
```  
CREATE TABLE Orders  
   (OrderID     int       PRIMARY KEY,  
    CustomerID  nchar(5)  REFERENCES Customers(CustomerID),  
    TerminalID  char(8)   NOT NULL DEFAULT HOST_ID(),  
    OrderDate   datetime  NOT NULL,  
    ShipDate    datetime  NULL,  
    ShipperID   int       NULL REFERENCES Shippers(ShipperID));  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [系統函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

