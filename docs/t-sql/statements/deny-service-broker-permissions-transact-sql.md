---
title: "DENY Service Broker 權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [Service Broker]
- routes [Service Broker], permissions
- Service Broker, permissions
- DENY statement, Service Broker
- remote service bindings [Service Broker], permissions
- permissions [Service Broker]
- message types [Service Broker], permissions
- denying permissions [SQL Server], Service Broker
- contracts [Service Broker], permissions
- services [Service Broker], permissions
ms.assetid: 7c6de71b-865c-41db-9413-ad9b3562e579
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed0ab0e375ecddbf9086647adce744a8ef4cb53d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="deny-service-broker-permissions-transact-sql"></a>DENY Service Broker 權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  拒絕 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 合約、訊息類型、遠端服務繫結、路由或服務的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DENY permission  [ ,...n ] ON  
    {    
       [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
        }  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>引數  
 *權限*  
 指定 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 安全性實體可以拒絕的權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 合約**::***contract_name*  
 指定正在拒絕權限的合約。 範圍限定詞**::**需要。  
  
 訊息類型**::***message_type_name*  
 指定正在拒絕權限的訊息類型。 範圍限定詞**::**需要。  
  
 遠端服務繫結**::***remote_binding_name*  
 指定正在拒絕權限的遠端服務繫結。 範圍限定詞**::**需要。  
  
 路由**::***route_name*  
 指定正在拒絕權限的路由。 範圍限定詞**::**需要。  
  
 服務**::***message_type_name*  
 指定正在拒絕權限的服務。 範圍限定詞**::**需要。  
  
 *database_principal*  
 指定要拒絕其權限的主體。 它有下列幾種：  
  
-   資料庫使用者  
-   資料庫角色  
-   應用程式角色  
-   對應至 Windows 登入的資料庫使用者  
-   對應至 Windows 群組的資料庫使用者  
-   對應至憑證的資料庫使用者  
-   對應至非對稱金鑰的資料庫使用者  
-   未對應至伺服器主體的資料庫使用者  
  
CASCADE  
 指出目前受到拒絕的權限，也為這個主體曾授與此權限的其他主體所拒絕。  
  
*denying_principal*  
 指定主體，執行這項查詢的主體會從這個主體衍生權限來拒絕權限。 它有下列幾種：  
  
-   資料庫使用者  
-   資料庫角色  
-   應用程式角色  
-   對應至 Windows 登入的資料庫使用者  
-   對應至 Windows 群組的資料庫使用者  
-   對應至憑證的資料庫使用者  
-   對應至非對稱金鑰的資料庫使用者  
-   未對應至伺服器主體的資料庫使用者  
  
## <a name="remarks"></a>備註  
  
## <a name="service-broker-contracts"></a>Service Broker 合約  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 合約是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 之最特定且最有限權限可拒絕[!INCLUDE[ssSB](../../includes/sssb-md.md)]合約詳列於下表，列出利用隱含方式包含它們的較通用權限。  
  
|Service Broker 合約權限|Service Broker 合約權限所隱含|資料庫權限所隱含|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Service Broker 訊息類型  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 訊息類型是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下面所列的是可以拒絕之最特定且最有限的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 訊息類型權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|Service Broker 訊息類型權限|Service Broker 訊息類型權限所隱含|資料庫權限所隱含|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Service Broker 遠端服務繫結  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 遠端服務繫結是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下面所列的是可以拒絕之最特定且最有限的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 遠端服務繫結權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|Service Broker 遠端服務繫結權限|Service Broker 遠端服務繫結權限所隱含|資料庫權限所隱含|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Service Broker 路由  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 路由是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 之最特定且最有限權限可拒絕[!INCLUDE[ssSB](../../includes/sssb-md.md)]路由詳列於下表，列出利用隱含方式包含它們的較通用權限。  
  
|Service Broker 路由權限|Service Broker 路由權限所隱含|資料庫權限所隱含|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Service Broker 服務  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服務是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 之最特定且最有限權限可拒絕[!INCLUDE[ssSB](../../includes/sssb-md.md)]服務詳列於下表，列出利用隱含方式包含它們的較通用權限。  
  
|Service Broker 服務權限|Service Broker 服務權限所隱含|資料庫權限所隱含|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 合約、訊息類型、遠端服務繫結、路由或服務的 CONTROL 權限。 如果使用 AS 子句，指定的主體必須擁有要拒絕其權限的類型。  
  
## <a name="see-also"></a>另請參閱  
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOKE Service Broker 權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [權限 &#40; Database engine&#41;](../../relational-databases/security/permissions-database-engine.md)  
  
  

