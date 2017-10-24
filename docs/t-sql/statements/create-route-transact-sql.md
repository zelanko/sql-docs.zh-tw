---
title: "建立路由 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_ROUTE_TSQL
- ROUTE
- CREATE ROUTE
- ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lifetimes [Service Broker]
- routes [Service Broker], creating
- forwarding brokers [SQL Server]
- service names [Service Broker]
- database mirroring [SQL Server], routing
- expired routes [SQL Server]
- activating routes
- CREATE ROUTE statement
ms.assetid: 7e695364-1a98-4cfd-8ebd-137ac5a425b3
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7268b5c9b43505d3c66fb6573a9a41c3cd62e3a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-route-transact-sql"></a>CREATE ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將新的路由加入目前資料庫的路由表中。 如果是外寄郵件，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 會檢查本機資料庫中的路由表來判斷路由。 針對肇因於另一個執行個體所引發之交談的訊息，包括要轉送的訊息[!INCLUDE[ssSB](../../includes/sssb-md.md)]簽入路由**msdb**。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE ROUTE route_name  
[ AUTHORIZATION owner_name ]  
WITH    
   [ SERVICE_NAME = 'service_name', ]  
   [ BROKER_INSTANCE = 'broker_instance_identifier' , ]  
   [ LIFETIME = route_lifetime , ]  
   ADDRESS =  'next_hop_address'  
   [ , MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *route_name*  
 這是要建立的路由名稱。 新路由會建立在目前的資料庫中，擁有者是 AUTHORIZATION 子句所指定的主體。 您不可指定伺服器、資料庫和結構描述名稱。 *Route_name*必須是有效**sysname**。  
  
 授權*owner_name*  
 將路由的擁有者設為指定的資料庫使用者或角色。 *Owner_name*目前使用者是中的其中一個成員時，可以是任何有效的使用者或角色的名稱**db_owner**固定的資料庫角色或**sysadmin**固定的伺服器角色。 否則， *owner_name*必須是目前使用者的名稱、 目前的使用者具有 IMPERSONATE 權限，使用者名稱或目前使用者所屬的角色的名稱。 當略過這個子句時，路由會屬於目前的使用者。  
  
 取代所有提及的  
 導入定義所建立之路由的子句。  
  
 SERVICE_NAME = **'***service_name***'**  
 指定這個路由所指向的遠端服務名稱。 *Service_name*必須完全符合遠端服務的名稱會使用。 [!INCLUDE[ssSB](../../includes/sssb-md.md)]使用位元組的比較，以比對*service_name*。 換言之，這項比較會區分大小寫，且不會考慮目前的定序。 如果省略 SERVICE_NAME，這個路由會符合任何服務名稱，但符合的優先權低於指定 SERVICE_NAME 的路由。 服務名稱的路由**'SQL/ServiceBroker/BrokerConfiguration'** Broker Configuration Notice 服務的路由。 指向這項服務的路由不能指定 Broker 執行個體。  
  
 BROKER_INSTANCE = **'***broker_instance_identifier***'**  
 指定主控目標服務的資料庫。 *Broker_instance_identifier*參數必須是遠端的資料庫中，您可以選取的資料庫中執行下列查詢取得的 broker 執行個體識別碼：  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID()  
```  
  
 當省略 BROKER_INSTANCE 子句時，這項路由會符合任何 Broker 執行個體。 當交談並未指定 Broker 執行個體時，符合任何 Broker 執行個體的路由，其相符優先權會高於含明確 Borker 執行個體的路由。 如果交談指定了 Broker 執行個體，含 Borker 執行個體的路由之優先權會高於符合任何 Broker 執行個體的路由。  
  
 存留期 **=**  *route_lifetime*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將路由保留在路由表中的時間量 (以秒為單位)。 在存留期間結束時，路由會到期，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在選擇新交談的路由時，不會再考慮這個路由。 如果省略這個子句，則*route_lifetime*是 NULL，而且路由永遠不會到期。  
  
 位址**='***next_hop_address***'**  
 指定這個路由的網路位址。 *Next_hop_address*指定 TCP/IP 位址，格式如下：  
  
 **TCP: / /**{ *dns_name* | *netbios_name* | *ip_address* } **:** *port_number*  
  
 指定*port_number*必須符合的通訊埠編號[!INCLUDE[ssSB](../../includes/sssb-md.md)]的執行個體的端點[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在指定電腦。 這可以在選取的資料庫中執行下列查詢來取得：  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 當服務在鏡像資料庫中，您也必須指定主控鏡像資料庫之其他執行個體的 MIRROR_ADDRESS。 否則，這個路由不會進行容錯移轉，將工作交給鏡像。  
  
 當路由指定**'LOCAL'**如*next_hop_address*，訊息會傳遞給目前執行個體內的服務[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 當路由指定**'TRANSPORT'**如*next_hop_address*，根據服務名稱中包含的網路位址來判斷網路位址。 指定的路由**'TRANSPORT'**不能指定服務名稱或 broker 執行個體。  
  
 MIRROR_ADDRESS **='***next_hop_mirror_address***'**  
 指定具有在一個鏡像的資料庫的鏡像資料庫的網路位址*next_hop_address*。 *Next_hop_mirror_address*指定 TCP/IP 位址，格式如下：  
  
 **TCP: / /**{ *dns_name* | *netbios_name* | *ip_address* } **:** *port_number*  
  
 指定*port_number*必須符合的通訊埠編號[!INCLUDE[ssSB](../../includes/sssb-md.md)]的執行個體的端點[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在指定電腦。 這可以在選取的資料庫中執行下列查詢來取得：  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 當指定 MIRROR_ADDRESS 時，路由必須指定 SERVICE_NAME 子句和 BROKER_INSTANCE 子句。 指定的路由**'LOCAL'**或**'TRANSPORT'**如*next_hop_address*不能指定鏡像位址。  
  
## <a name="remarks"></a>備註  
 儲存路由的路由表是可以透過讀取的中繼資料資料表**sys.routes**目錄檢視。 您只能利用 CREATE ROUTE、ALTER ROUTE 和 DROP ROUTE 陳述式來更新這個目錄檢視。  
  
 依預設，每個使用者資料庫中的路由表都包含一個路由。 這個路由的名稱**AutoCreatedLocal**。 這個路由指定**'LOCAL'**如*next_hop_address*和符合任何服務名稱和 broker 執行個體識別項。  
  
 當路由指定**'TRANSPORT'**如*next_hop_address*，根據服務的名稱來判斷網路位址。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以順利處理開頭是有效的格式是網路位址的服務名稱*next_hop_address*。  
  
 路由表可以包含指定相同服務、網路位址和 Broker 執行個體識別碼之任意數目的路由。 在這個情況下，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 會利用在交談所指定的資訊和路由表所指定的資訊之間，設計用來尋找完全相符項目的程序，來選擇路由。  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 不會從路由表中移除過期的路由。 您可以利用 ALTER ROUTE 陳述式，使過期的路由成為在使用中。  
  
 路由不能是暫存物件。 將開頭的名稱路由 **#**  ，但它們是永久物件。  
  
## <a name="permissions"></a>Permissions  
 預設值的成員建立路由的權限**db_ddladmin**或**db_owner**固定資料庫角色和**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-tcpip-route-by-using-a-dns-name"></a>A. 使用 DNS 名稱來建立 TCP/IP 路由  
 下列範例會建立服務 `//Adventure-Works.com/Expenses` 的路由。 這個路由指定送往這項服務的訊息要通過 TCP 而到達 DNS 名稱 `1234` 所識別之主機的通訊埠 `www.Adventure-Works.com`。 目標伺服器會在到達時將訊息傳遞給唯一識別碼 `D8D4D268-00A3-4C62-8F91-634B89C1E315` 所識別的 Broker 執行個體。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://www.Adventure-Works.com:1234' ;  
```  
  
### <a name="b-creating-a-tcpip-route-by-using-a-netbios-name"></a>B. 使用 NetBIOS 名稱來建立 TCP/IP 路由  
 下列範例會建立服務 `//Adventure-Works.com/Expenses` 的路由。 這個路由指定送往這項服務的訊息要通過 TCP 而到達 NetBIOS 名稱 `1234` 所識別之主機的通訊埠 `SERVER02`。 在到達時，目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將訊息傳遞給唯一識別碼 `D8D4D268-00A3-4C62-8F91-634B89C1E315` 所識別的資料庫執行個體。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH   
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://SERVER02:1234' ;  
```  
  
### <a name="c-creating-a-tcpip-route-by-using-an-ip-address"></a>C. 使用 IP 位址來建立 TCP/IP 路由  
 下列範例會建立服務 `//Adventure-Works.com/Expenses` 的路由。 這個路由指定送往這項服務的訊息要通過 TCP 而到達在 IP 位址 `1234` 之主機的通訊埠 `192.168.10.2`。 在到達時，目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將訊息傳遞給唯一識別碼 `D8D4D268-00A3-4C62-8F91-634B89C1E315` 所識別的 Broker 執行個體。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://192.168.10.2:1234' ;  
```  
  
### <a name="d-creating-a-route-to-a-forwarding-broker"></a>D. 建立通往轉送 Broker 的路由  
 下列範例會建立通往伺服器 `dispatch.Adventure-Works.com` 之轉送 Broker 的路由。 由於既未指定服務名稱，也未指定 Broker 執行個體識別碼，因此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將這個路由用在未定義任何其他路由的服務上。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    ADDRESS = 'TCP://dispatch.Adventure-Works.com' ;   
```  
  
### <a name="e-creating-a-route-to-a-local-service"></a>E. 建立通往本機服務的路由  
 下列範例會建立通往與路由位於相同執行個體之服務 `//Adventure-Works.com/LogRequests` 的路由。  
  
```  
CREATE ROUTE LogRequests  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/LogRequests',  
    ADDRESS = 'LOCAL' ;  
```  
  
### <a name="f-creating-a-route-with-a-specified-lifetime"></a>F. 建立含指定存留期間的路由  
 下列範例會建立服務 `//Adventure-Works.com/Expenses` 的路由。 路由的存留期間是 `259200` 秒，相當於 72 小時。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    LIFETIME = 259200,  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234' ;  
```  
  
### <a name="g-creating-a-route-to-a-mirrored-database"></a>G. 建立通往鏡像資料庫的路由  
 下列範例會建立服務 `//Adventure-Works.com/Expenses` 的路由。 服務在鏡像的資料庫中。 其中一個鏡像資料庫所在的位址是 `services.Adventure-Works.com:1234`，另一個資料庫所在的位址是 `services-mirror.Adventure-Works.com:1234`。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = '69fcc80c-2239-4700-8437-1001ecddf933',  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234',   
    MIRROR_ADDRESS = 'TCP://services-mirror.Adventure-Works.com:1234' ;  
```  
  
### <a name="h-creating-a-route-that-uses-the-service-name-for-routing"></a>H. 建立使用服務名稱來進行傳遞的路由  
 下列範例會建立一個路由，利用服務名稱來判斷訊息所要送往的網路位址。 請注意，在網路位址中指定 `'TRANSPORT'` 的路由，符合的優先權低於其他路由。  
  
```  
CREATE ROUTE TransportRoute  
    WITH ADDRESS = 'TRANSPORT' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER ROUTE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [DROP ROUTE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

