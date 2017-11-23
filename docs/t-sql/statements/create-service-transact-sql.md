---
title: "建立服務 (TRANSACT-SQL) |Microsoft 文件"
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
- CREATE_SERVICE_TSQL
- SERVICE
- CREATE SERVICE
- SERVICE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- services [Service Broker], creating
- CREATE SERVICE statement
- contracts [Service Broker], service creation
ms.assetid: fb804fa2-48eb-4878-a12f-4e0d5f4bc9e3
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5298494b6c3be0685df771f6d86e11c7b788d002
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="create-service-transact-sql"></a>CREATE SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立新的服務。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服務是一項特定工作或一組工作的名稱。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會利用服務的名稱路由傳送訊息，將訊息傳遞至資料庫內的正確佇列，以及強制使用合約進行交談。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE SERVICE service_name  
   [ AUTHORIZATION owner_name ]  
   ON QUEUE [ schema_name. ]queue_name  
   [ ( contract_name | [DEFAULT][ ,...n ] ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *服務名稱*  
 這是要建立的服務名稱。 新服務會建立在目前資料庫中，擁有者是 AUTHORIZATION 子句所指定的主體。 您不可指定伺服器、資料庫和結構描述名稱。 *Service_name*必須是有效**sysname**。  
  
> [!NOTE]  
>  不要在建立服務使用關鍵字 ANY 代表*service_name*。 當您在 CREATE BROKER PRIORITY 中針對服務名稱指定 ANY 時，就會考慮所有服務的優先權。 這並不限於名稱為 ANY 的服務。  
  
 授權*owner_name*  
 將服務的擁有者設為指定的資料庫使用者或角色。 當目前的使用者是**dbo**或**sa**， *owner_name*可能是任何有效的使用者或角色的名稱。 否則， *owner_name*必須是目前使用者的名稱、 目前的使用者具有 IMPERSONATE 權限，使用者名稱或目前使用者所屬的角色的名稱。  
  
 ON 佇列 [ *schema_name***。** ] *queue_name*  
 指定接收服務訊息的佇列。 佇列必須在服務的相同資料庫中。 如果沒有*schema_name*提供結構描述是使用者執行陳述式的預設結構描述。  
  
 *contract_name*  
 指定目標可以是這項服務的合約。 服務程式會利用指定的合約來起始與這項服務的交談。 如果未指定任何合約，服務就只能起始交談。  
  
 **[**預設**]**  
 指定這項服務可以是遵照 DEFAULT 合約的交談目標。 在這個子句的內容中，DEFAULT 不是關鍵字，必須用識別碼來分隔。 DEFAULT 合約允許交談的兩端傳送訊息類型是 DEFAULT 的訊息。 訊息類型 DEFAULT 所用的驗證是 NONE。  
  
## <a name="remarks"></a>備註  
 服務會顯露相關合約所提供的功能，供其他服務使用。 CREATE SERVICE 陳述式會指定目標是這項服務的合約。 交談必須使用服務指定的合約，才能將這項服務設為目標。 未指定合約的服務，不會向其他服務顯露任何功能。  
  
 這項服務所初始化的交談可以使用任何合約。 當服務只要起始交談時，您便建立不指定任何合約的服務。  
  
 當 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 接受來自遠端服務的新交談時，目標服務的名稱會決定 Broker 將交談訊息放在其中的佇列。  
  
## <a name="permissions"></a>Permissions  
 建立服務的權限的成員預設**db_ddladmin**或**db_owner**固定資料庫角色和**sysadmin**固定的伺服器角色。 執行 CREATE SERVICE 陳述式的使用者必須有佇列及所有指定合約的 REFERENCES 權限。  
  
 服務的 REFERENCES 權限預設為服務的成員擁有者**db_ddladmin**或**db_owner**固定資料庫角色和成員的**sysadmin**固定的伺服器角色。 SEND 權限的服務，也就是成員的擁有者服務預設**db_owner**固定資料庫角色的成員**sysadmin**固定的伺服器角色。  
  
 服務不能是暫存物件。 服務名稱開頭 **#**  ，但它們是永久物件。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-service-with-one-contract"></a>A. 建立含有一份合約的服務  
 下列範例會在 `//Adventure-Works.com/Expenses` 結構描述中的 `ExpenseQueue` 佇列上建立 `dbo` 服務。 以這項服務為目標的對話必須遵照 `//Adventure-Works.com/Expenses/ExpenseSubmission` 合約。  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE [dbo].[ExpenseQueue]  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="b-creating-a-service-with-multiple-contracts"></a>B. 建立含有多份合約的服務  
 下列範例會在 `//Adventure-Works.com/Expenses` 佇列上建立 `ExpenseQueue` 服務。 以這項服務為目標的對話必須遵照 `//Adventure-Works.com/Expenses/ExpenseSubmission` 合約或 `//Adventure-Works.com/Expenses/ExpenseProcessing` 合約。  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission],  
     [//Adventure-Works.com/Expenses/ExpenseProcessing]) ;  
```  
  
### <a name="c-creating-a-service-with-no-contracts"></a>C. 建立不含任何合約的服務  
 下列範例會建立服務`//Adventure-Works.com/Expenses on the ExpenseQueue`佇列。 這項服務沒有合約資訊。 因此，這項服務只能是交談的起始端。  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER 服務 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [卸除服務 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
