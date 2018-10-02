---
title: CREATE REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 53b43fece12144b60a4d6b0cfcd0918997e55613
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710506"
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
 這是要建立之遠端服務繫結的名稱。 您不可指定伺服器、資料庫和結構描述名稱。 *binding_name* 必須是有效的 **sysname**。  
  
 AUTHORIZATION *owner_name*  
 將繫結的擁有者設為指定的資料庫使用者或角色。 當目前的使用者是 **dbo** 或 **sa** 時，*owner_name* 可以是任何有效使用者或角色的名稱。 否則，*owner_name* 必須是目前使用者的名稱、目前使用者擁有的 IMPERSONATE 權限使用者名稱，或目前使用者所屬的角色名稱。  
  
 TO SERVICE '*service_name*'  
 指定將遠端服務繫結到 WITH USER 子句所識別的使用者。  
  
 USER = *user_name*  
 指定擁有 TO SERVICE 子句所識別的遠端服務之相關憑證的資料庫主體。 這個憑證用來加密和驗證與遠端服務交換的訊息。  
  
 ANONYMOUS  
 指定與遠端服務通訊時，是否使用匿名驗證。 如果 ANONYMOUS = ON，便會使用匿名驗證，且遠端資料庫的作業會以 **public** 固定資料庫角色成員的身分來執行。 如果 ANONYMOUS = OFF，遠端資料庫的作業會以這個資料庫的特定使用者身分來執行。 如果未指定這個子句，預設值便是 OFF。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 利用遠端服務繫結來尋找新交談要用的憑證。 已與 *user_name* 建立關聯的憑證中之公開金鑰會用來驗證傳給遠端服務的訊息，以及對之後要用來加密交談的工作階段金鑰進行加密。 *user_name* 的憑證必須對應於主控遠端服務之資料庫中的使用者憑證。  
  
 只有與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體以外目標服務通訊的起始服務，才需要遠端服務繫結。 主控起始服務的資料庫必須含有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體以外的任何目標服務的遠端服務繫結。 主控目標服務的資料庫不需要含有與它交談的起始服務之遠端服務繫結。 當起始端服務和目標服務位於相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中時，不需要任何遠端服務繫結。 但是，如果有遠端服務繫結存在 (此時為 TO SERVICE 指定的 *service_name* 符合本機服務的名稱)，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 將會使用此繫結。  
  
 當 ANONYMOUS = ON 時，起始服務會以 **public** 固定資料庫角色成員的身分來連線到目標服務。 依預設，這個角色的成員並沒有連接到資料庫的權限。 若要順利傳送訊息，目標資料庫必須將資料庫的 CONNECT 權限和目標服務的 SEND 權限授與 **public** 角色。  
  
 當使用者擁有多項憑證時，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 會從目前有效的憑證中，選取到期日最晚的憑證，並將它標示為 AVAILABLE FOR BEGIN_DIALOG。  
  
## <a name="permissions"></a>[權限]  
 建立遠端服務繫結的權限預設為 USER 子句中所指定的使用者、**db_owner** 固定資料庫角色的成員、**db_ddladmin** 固定資料庫角色的成員，以及 **sysadmin** 固定伺服器角色的成員。  
  
 執行 CREATE REMOTE SERVICE BINDING 陳述式的使用者必須有陳述式指定的主體之模擬權限。  
  
 遠端服務繫結不能是暫存物件。 您可以使用開頭是 **#** 的遠端服務繫結名稱，但它們是永久物件。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-remote-service-binding"></a>A. 建立遠端服務繫結  
 下列範例會建立 `//Adventure-Works.com/services/AccountsPayable` 服務的繫結。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會使用 `APUser` 資料庫主體所擁有的憑證來向遠端服務驗證，以及與遠端服務交換工作階段加密金鑰。  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser ;  
```  
  
### <a name="b-creating-a-remote-service-binding-using-anonymous-authentication"></a>B. 利用匿名驗證來建立遠端服務繫結  
 下列範例會建立 `//Adventure-Works.com/services/AccountsPayable` 服務的繫結。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會使用 `APUser` 資料庫主體所擁有的憑證來與遠端服務交換工作階段加密金鑰。 Broker 並不接受遠端服務的驗證。 在主控遠端服務的資料庫中，訊息是以 **guest** 使用者的身分來傳遞。  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser, ANONYMOUS=ON ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
