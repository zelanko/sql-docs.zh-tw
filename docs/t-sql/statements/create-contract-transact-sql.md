---
title: "建立合約 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONTRACT_TSQL
- CREATE_CONTRACT_TSQL
- CREATE CONTRACT
- CONTRACT
dev_langs: TSQL
helpviewer_keywords:
- CREATE CONTRACT statement
- contracts [Service Broker], creating
- message types [Service Broker], contracts
ms.assetid: 494cbfa6-8e93-4161-a64d-90d681915211
caps.latest.revision: "48"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b77fba7800b8533793f9b26574d442bb0c087b8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="create-contract-transact-sql"></a>CREATE CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立新的合約。 合約會定義 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 交談中所用的訊息類型，並決定交談的哪一端可以傳送該類型的訊息。 每一個交談都遵照一個合約。 交談開始時，起始服務會指定交談的合約。 目標服務則會指定目標服務接受交談的合約。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE CONTRACT contract_name  
   [ AUTHORIZATION owner_name ]  
      (  {   { message_type_name | [ DEFAULT ] }  
          SENT BY { INITIATOR | TARGET | ANY }   
       } [ ,...n] )   
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *contract_name*  
 這是要建立的合約名稱。 新合約會建立在目前的資料庫中，擁有者是 AUTHORIZATION 子句所指定的主體。 您不可指定伺服器、資料庫和結構描述名稱。 *Contract_name*可達 128 個字元。  
  
> [!NOTE]  
>  請勿建立合約使用關鍵字 ANY 代表*contract_name*。 當您在 CREATE BROKER PRIORITY 中針對合約名稱指定 ANY 時，就會考慮所有合約的優先權。 這並不限於名稱為 ANY 的合約。  
  
 授權*owner_name*  
 將合約的擁有者設為指定的資料庫使用者或角色。 當目前的使用者是**dbo**或**sa**， *owner_name*可以是任何有效的使用者或角色的名稱。 否則， *owner_name*必須是目前使用者的名稱、 目前的使用者具有 impersonate 權限，使用者名稱或目前使用者所屬的角色的名稱。 當略過這個子句時，合約會屬於目前的使用者。  
  
 *message_type_name*  
 這是要併入合約之訊息類型的名稱。  
  
 SENT BY   
 指定哪一個端點可以傳送指定訊息類型的訊息。 合約記錄服務可以用來進行特定交談的訊息。 每個交談都具有兩個端點：*啟動器*端點，服務開始交談，而*目標*端點，起始端連絡的服務。  
  
 INITIATOR   
 表示只有交談起始端可以傳送特定訊息類型的訊息。 開始交談的服務稱為*啟動器*的交談。  
  
 TARGET  
 表示只有交談目標可以傳送特定訊息類型的訊息。 接受交談的另一個服務所啟動的服務稱為*目標*的交談。  
  
 ANY  
 表示起始端和目標兩者都可以傳送這個類型的訊息。  
  
 [ DEFAULT ]  
 表示這個合約支援預設訊息類型的訊息。 依預設，所有資料庫都包含名稱為 DEFAULT 的訊息類型。 這個訊息類型使用 NONE 的驗證。 在這個子句的內容中，DEFAULT 不是關鍵字，必須用識別碼來分隔。 Microsoft SQL Server 也提供指定 DEFAULT 訊息類型的 DEFAULT 合約。  
  
## <a name="remarks"></a>備註  
 合約中訊息類型的順序並不重要。 在目標收到第一則訊息之後，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 允許交談的任何一端在任何時間傳送該端允許的任何訊息。 例如，如果交談起始端可以傳送訊息型別**//Adventure-Works.com/Expenses/SubmitExpense**，[!INCLUDE[ssSB](../../includes/sssb-md.md)]允許起始端傳送任意數目的**SubmitExpense**交談內的訊息。  
  
 合約中的訊息類型和方向無法變更。 若要改變合約的 AUTHORIZATION，請使用 ALTER AUTHORIZATION 陳述式。  
  
 合約必須允許起始端傳送訊息。 合約不包含至少一個 SENT BY ANY 或 SENT BY INITIATOR 的訊息類型時，CREATE CONTRACT 陳述式會失敗。  
  
 不論何種合約，服務一律可以收到的訊息類型`http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`， `http://schemas.microsoft.com/SQL/ServiceBroker/Error`，和`http://schemas.microsoft.com/SQL/ServiceBroker/EndDialog`。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會針對應用程式使用系統訊息的這些訊息類型。  
  
 合約不能是暫存物件。 您可以使用開頭是 # 的合約名稱，但它們是永久物件。  
  
## <a name="permissions"></a>Permissions  
 根據預設，成員**db_ddladmin**或**db_owner**固定資料庫角色和**sysadmin**固定的伺服器角色可以建立合約。  
  
 根據預設，合約的成員的擁有者**db_ddladmin**或**db_owner**固定資料庫角色和成員的**sysadmin**固定的伺服器角色擁有的參考在合約上的權限。  
  
 執行 CREATE CONTRACT 陳述式的使用者必須有所有指定訊息類型的 REFERENCES 權限。  
  
## <a name="examples"></a>範例  
 **A.建立合約**  
  
 下列範例會依據三種訊息類型建立費用償還合約。  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE           
    [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
    VALIDATION= WELL_FORMED_XML ;           
  
CREATE CONTRACT            
    [//Adventure-Works.com/Expenses/ExpenseSubmission]           
    ( [//Adventure-Works.com/Expenses/SubmitExpense]           
          SENT BY INITIATOR,           
      [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
          SENT BY TARGET,           
      [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
          SENT BY TARGET           
    ) ;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [卸除合約 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-contract-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
