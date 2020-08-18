---
description: REVOKE Service Broker 權限 (Transact-SQL)
title: REVOKE Service Broker 權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- routes [Service Broker], permissions
- Service Broker, permissions
- remote service bindings [Service Broker], permissions
- permissions [Service Broker]
- message types [Service Broker], permissions
- contracts [Service Broker], permissions
- services [Service Broker], permissions
- REVOKE statement, Service Broker
ms.assetid: 70f1d938-97e2-48a4-9bc0-8be9f2f2c36d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2d018e710bb272d9daa9eda7099d201b80ea3c1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88357114"
---
# <a name="revoke-service-broker-permissions-transact-sql"></a>REVOKE Service Broker 權限 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  撤銷 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 合約、訊息類型、遠端服務繫結、路由或服務的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] ON  
    {   
       [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
        }  
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 GRANT OPTION FOR  
 表示授與指定權限給其他主體的權限會被撤銷。 不會撤銷權限本身。  
  
> [!IMPORTANT]  
>  如果主體有不含 GRANT 選項的指定權限，則會撤銷權限本身。  
  
 *permission*  
 指定可以在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 上撤銷的安全性實體權限。 如需這些權限的清單，請參閱本主題稍後的「備註」一節。  
  
 CONTRACT **::**_contract_name_  
 指定正在撤銷權限的合約。 範圍限定詞 **::** 為必要項目。  
  
 MESSAGE TYPE **::**_message_type_name_  
 指定正在撤銷權限的訊息類型。 範圍限定詞 **::** 為必要項目。  
  
 REMOTE SERVICE BINDING **::**_remote_binding_name_  
 指定正在撤銷權限的遠端服務繫結。 範圍限定詞 **::** 為必要項目。  
  
 ROUTE **::**_route_name_  
 指定要撤銷其權限的路由。 範圍限定詞 **::** 為必要項目。  
  
 SERVICE **::**_message_type_name_  
 指定要撤銷其權限的服務。 範圍限定詞 **::** 為必要項目。  
  
 *database_principal*  
 指定要撤銷其權限的主體。 *database_principal* 可以是下列其中之一：  
  
-   資料庫使用者  
  
-   資料庫角色  
  
-   應用程式角色  
  
-   對應至 Windows 登入的資料庫使用者  
  
-   對應至 Windows 群組的資料庫使用者  
  
-   對應至憑證的資料庫使用者  
  
-   對應至非對稱金鑰的資料庫使用者  
  
-   未對應至伺服器主體的資料庫使用者  
  
 CASCADE  
 指出目前正在撤銷的權限，而這個權限也會被這個主體所授與或拒絕的其他主體所撤銷。  
  
> [!CAUTION]  
>  獲得授與 WITH GRANT OPTION 之權限的串聯撤銷，會同時撤銷該權限的 GRANT 和 DENY。  
  
 AS *revoking_principal*  
 指定主體，執行這項查詢的主體會從這個主體衍生其權限來撤銷權限。 *revoking_principal* 可以是下列其中一項：  
  
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
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 合約是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 合約上撤銷之最特定且最有限的權限，並列出利用隱含方式來包含這些權限的較通用權限。  
  
|Service Broker 合約權限|Service Broker 合約權限所隱含|資料庫權限所隱含|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Service Broker 訊息類型  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 訊息類型是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 訊息類型上撤銷之最特定且最有限的權限，並列出利用隱含方式來包含這些權限的較通用權限。  
  
|Service Broker 訊息類型權限|Service Broker 訊息類型權限所隱含|資料庫權限所隱含|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Service Broker 遠端服務繫結  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 遠端服務繫結是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 遠端服務繫結上撤銷之最特定且最有限的權限，並列出利用隱含方式來包含這些權限的較通用權限。  
  
|Service Broker 遠端服務繫結權限|Service Broker 遠端服務繫結權限所隱含|資料庫權限所隱含|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Service Broker 路由  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 路由是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 路由上撤銷之最特定且最有限的權限，並列出利用隱含方式來包含這些權限的較通用權限。  
  
|Service Broker 路由權限|Service Broker 路由權限所隱含|資料庫權限所隱含|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Service Broker 服務  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服務是一個由資料庫所包含的資料庫層級安全性實體，在權限階層中，此資料庫為該安全性實體的父系。 下表所列的是可以在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服務上撤銷之最特定且最有限的權限，並列出利用隱含方式來包含這些權限的較通用權限。  
  
|Service Broker 服務權限|Service Broker 服務權限所隱含|資料庫權限所隱含|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>權限  
 需要 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 合約、訊息類型、遠端服務繫結、路由或服務的 CONTROL 權限  
  
## <a name="see-also"></a>另請參閱  
 [GRANT Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)   
 [DENY Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
