---
title: MSSQLSERVER_4104 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4104 (Database Engine error)
ms.assetid: 52dc32d8-97ad-4ef0-834d-2e68f215d007
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 55bbf20609dc364fdb79c0c785ccffb691da991e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814386"
---
# <a name="mssqlserver4104"></a>MSSQLSERVER_4104
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|4104|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|ALG_MULTI_ID_BAD|  
|訊息文字|無法繫結多重部分 (Multi-Part) 識別碼 "%.*ls"。|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中實體的名稱也稱為 *「識別碼」*(Identifier)。 每當參考實體 (例如在查詢中指定資料行和資料表名稱) 時，您就可以使用識別碼。 多重部分識別碼包含一個或多個限定詞，當做識別碼的前置詞。 例如，資料表識別碼的前置詞可能是包含此資料表之資料庫名稱和結構描述等限定詞，或者資料行識別碼的前置詞可能是資料表名稱或資料表別名等限定詞。  
  
錯誤 4104 表示指定的多重部分識別碼無法對應至現有的實體。 這項錯誤可能會在下列情況下傳回：  
  
-   提供成為資料行名稱之前置詞的限定詞沒有對應至用於查詢中的任何資料表或別名名稱。  
  
    例如，下列陳述式會使用資料表別名 (`Dept`) 當做資料行前置詞，但是此資料表別名並未在 FROM 子句中參考。  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department;  
    ```  
  
    在下列陳述式中，多重部分資料行識別碼 `TableB.KeyCol` 會在 WHERE 子句中指定成兩個資料表之間 JOIN 條件的一部分。不過，`TableB` 並未在查詢中明確參考。  
  
    ```  
    DELETE FROM TableA WHERE TableA.KeyCol = TableB.KeyCol;  
    ```  
  
    ```  
    SELECT 'X' FROM TableA WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   資料表的別名名稱提供在 FROM 子句，但是針對資料行所提供的限定詞就是資料表名稱。 例如，下列陳述式會使用資料表名稱 `Department` 當做資料行前置詞。不過，資料表具有在 FROM 子句中參考的別名 (`Dept`)。  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department AS Dept;  
    ```  
  
    使用別名時，此資料表名稱就無法在陳述式中的其他位置使用。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法判斷多重部分識別碼是參考前置詞為資料表的資料行，還是前置詞為資料行之 CLR 使用者定義資料類型 (UDT) 的屬性。 發生這種情況的原因是在資料行名稱和屬性名稱之間使用句號分隔字元 (.)，藉以參考 UDT 資料行的屬性，而這種方式就如同在資料行名稱前面加上資料表名稱。 下列範例會建立兩份資料表：`a` 和 `b`。 資料表 `b` 包含資料行 `a`，而且此資料行會使用 CLR UDT `dbo.myudt2` 當做其資料類型。 SELECT 陳述式包含多重部分識別碼 `a.c2`。  
  
    ```  
    CREATE TABLE a (c2 int);   
    GO  
    ```  
  
    ```  
    CREATE TABLE b (a dbo.myudt2);   
    GO  
    ```  
  
    ```  
    SELECT a.c2 FROM a, b;   
    ```  
  
    假設 UDT `myudt2` 沒有名為 `c2` 的屬性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法判斷識別碼 `a.c2` 會參考資料表 `a` 中的資料行 `c2`，還是資料表 `b` 中屬性 `c2` 的資料行 `a`。  
  
## <a name="user-action"></a>使用者動作  
  
-   針對在查詢之 FROM 子句中指定的資料表名稱或別名名稱，比對資料行前置詞。 如果已經在 FROM 子句中定義資料表名稱的別名，您就只能使用此別名當做與該資料表相關聯之資料行的限定詞。  
  
    您可以依照下列方式更正上述參考 `HumanResources.Department` 資料表的陳述式：  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department AS Dept;  
    GO  
    ```  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department;  
    GO  
    ```  
  
-   確定所有資料表都指定在查詢中，而且資料表之間的 JOIN 條件已正確指定。 您可以依照下列方式更正上述 DELETE 陳述式：  
  
    ```  
    DELETE FROM dbo.TableA  
    WHERE TableA.KeyCol = (SELECT TableB.KeyCol   
                            FROM TableB   
                            WHERE TableA.KeyCol = TableB.KeyCol);  
    GO  
    ```  
  
    您可以依照下列方式更正 `TableA` 的上述 SELECT 陳述式：  
  
    ```  
    SELECT 'X' FROM TableA, TableB WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
    中的多個  
  
    ```  
    SELECT 'X' FROM TableA INNER JOIN TableB ON TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   針對識別碼使用唯一且清楚定義的名稱。 這樣做可讓您的程式碼更容易讀取和維護，而且也會盡可能降低多個實體具有模稜兩可參考的風險。  
  
## <a name="see-also"></a>另請參閱  
[MSSQLSERVER_107](~/relational-databases/errors-events/mssqlserver-107-database-engine-error.md)  
[資料庫識別碼](~/relational-databases/databases/database-identifiers.md)  
  
