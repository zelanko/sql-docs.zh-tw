---
title: "建立遠端服務繫結 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE REMOTE SERVICE BINDING
- SERVICE_BINDING_TSQL
- CREATE REMOTE SERVICE
- REMOTE_TSQL
- CREATE_REMOTE_SERVICE_BINDING_TSQL
- CREATE_REMOTE_SERVICE_TSQL
- BINDING
- SERVICE BINDING
- BINDING_TSQL
- CREATE_REMOTE_TSQL
- REMOTE_SERVICE_TSQL
- CREATE REMOTE
- REMOTE SERVICE
- REMOTE_SERVICE_BINDING_TSQL
- REMOTE
- REMOTE SERVICE BINDING
dev_langs:
- TSQL
helpviewer_keywords:
- binding remote service [Service Broker]
- dialog security [Service Broker]
- end-to-end security [Service Broker]
- security [Service Broker], remote service bindings
- CREATE REMOTE SERVICE BINDING statement
- conversation security [Service Broker]
- remote service bindings [Service Broker], creating
ms.assetid: 4165c404-4d50-4063-9a6e-6e267d309376
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4083cb617d76084719450a6abc49fd76345cc7a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-remote-service-binding-transact-sql"></a>CREATE REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立一項繫結來定義與遠端服務的交談起始時所用的安全性認證。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE REMOTE SERVICE BINDING binding_name   
   [ AUTHORIZATION owner_name ]   
   TO SERVICE 'service_name'   
   WITH  USER = user_name [ , ANONYMOUS = { ON | OFF } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *binding_name*  
 這是要建立之遠端服務繫結的名稱。 您不可指定伺服器、資料庫和結構描述名稱。 *Binding_name*必須是有效**sysname**。  
  
 授權*owner_name*  
 將繫結的擁有者設為指定的資料庫使用者或角色。 當目前的使用者是**dbo**或**sa**， *owner_name*可以是任何有效的使用者或角色的名稱。 否則， *owner_name*必須是目前使用者的名稱、 目前的使用者具有 IMPERSONATE 權限的使用者名稱或目前使用者所屬的角色的名稱。  
  
 服務 '*service_name*'  
 指定將遠端服務繫結到 WITH USER 子句所識別的使用者。  
  
 使用者 = *user_name*  
 指定擁有 TO SERVICE 子句所識別的遠端服務之相關憑證的資料庫主體。 這個憑證用來加密和驗證與遠端服務交換的訊息。  
  
 ANONYMOUS  
 指定與遠端服務通訊時，是否使用匿名驗證。 如果 ANONYMOUS = ON，使用匿名驗證，且遠端資料庫中的作業就會發生成員的身分**公用**固定的資料庫角色。 如果 ANONYMOUS = OFF，遠端資料庫的作業會以這個資料庫的特定使用者身分來執行。 如果未指定這個子句，預設值便是 OFF。  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 利用遠端服務繫結來尋找新交談要用的憑證。 中的憑證與相關聯的公開金鑰*user_name*用來驗證訊息傳送至遠端服務，並接著用來加密交談的工作階段金鑰。 憑證*user_name*必須對應於主控遠端服務之資料庫中的使用者憑證。  
  
 只有與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體以外目標服務通訊的起始服務，才需要遠端服務繫結。 主控起始服務的資料庫必須含有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體以外的任何目標服務的遠端服務繫結。 主控目標服務的資料庫不需要含有與它交談的起始服務之遠端服務繫結。 當起始端服務和目標服務位於相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中時，不需要任何遠端服務繫結。 不過，如果遠端服務繫結存在 where *service_name*指定的 TO SERVICE 符合名稱的本機服務[!INCLUDE[ssSB](../../includes/sssb-md.md)]會使用繫結。  
  
 當 ANONYMOUS = ON，起始服務會連接至目標服務的成員身分**公用**固定的資料庫角色。 依預設，這個角色的成員並沒有連接到資料庫的權限。 若要成功地傳送訊息時，必須授與目標資料庫**公用**資料庫的 CONNECT 權限和目標服務的 SEND 權限的角色。  
  
 當使用者擁有多項憑證時，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 會從目前有效的憑證中，選取到期日最晚的憑證，並將它標示為 AVAILABLE FOR BEGIN_DIALOG。  
  
## <a name="permissions"></a>Permissions  
 權限建立遠端服務繫結至名為在使用者子句中，成員的使用者的預設**db_owner**固定的資料庫角色、 成員的**db_ddladmin**固定資料庫角色和成員**sysadmin**固定的伺服器角色。  
  
 執行 CREATE REMOTE SERVICE BINDING 陳述式的使用者必須有陳述式指定的主體之模擬權限。  
  
 遠端服務繫結不能是暫存物件。 遠端服務繫結名稱開頭為 **#**  ，但它們是永久物件。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-remote-service-binding"></a>A. 建立遠端服務繫結  
 下列範例會建立 `//Adventure-Works.com/services/AccountsPayable` 服務的繫結。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會使用 `APUser` 資料庫主體所擁有的憑證來向遠端服務驗證，以及與遠端服務交換工作階段加密金鑰。  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser ;  
```  
  
### <a name="b-creating-a-remote-service-binding-using-anonymous-authentication"></a>B. 利用匿名驗證來建立遠端服務繫結  
 下列範例會建立 `//Adventure-Works.com/services/AccountsPayable` 服務的繫結。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會使用 `APUser` 資料庫主體所擁有的憑證來與遠端服務交換工作階段加密金鑰。 Broker 並不接受遠端服務的驗證。 在主控遠端服務資料庫中，訊息會傳遞做為**客體**使用者。  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser, ANONYMOUS=ON ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [更改遠端服務繫結 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [卸除遠端服務繫結 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

