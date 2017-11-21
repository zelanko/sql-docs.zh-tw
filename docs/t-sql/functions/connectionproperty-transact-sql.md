---
title: "CONNECTIONPROPERTY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONNECTIONPROPERTY_TSQL
- CONNECTIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- CONNECTIONPROPERTY statement
ms.assetid: 6bd9ccae-af77-4a05-b97f-f8ab41cfde42
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a5b023530bce0269af96918b0d578c6ca54293d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

針對傳入要求的唯一連接，傳回連接屬性的相關資訊。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>引數  
*屬性*  
連接的屬性。 *屬性*可以是下列值之一。
  
|值|資料類型|Description|  
|---|---|---|
|net_transport|**nvarchar （40)**|傳回這項連接所用的實體傳輸通訊協定。 不可為 Null。<br /><br /> 傳回值為： **HTTP**，**具名管道**，**工作階段**，**共用記憶體**， **SSL**， **TCP**，和**VIA**。<br /><br /> 注意： 一律會傳回**工作階段**當連接已啟用，multiple active result set (MARS)，並啟用連接共用。|  
|protocol_type|**nvarchar （40)**|傳回裝載的通訊協定類型。 它目前會區分 TDS (TSQL) 和 SOAP。 可為 Null。|  
|auth_scheme|**nvarchar （40)**|傳回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連線的驗證配置。 驗證配置為 Windows 驗證 (NTLM、KERBEROS、DIGEST、BASIC、NEGOTIATE) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 不可為 Null。|  
|local_net_address|**varchar(48)**|傳回這項連接之目標伺服器的 IP 位址。 只適用於使用 TCP 傳輸提供者的連接。 可為 Null。|  
|local_tcp_port|**int**|如果這項連接是使用 TCP 傳輸的連接，傳回這項連接的目標伺服器 TCP 埠。 可為 Null。|  
|client_net_address|**varchar(48)**|要求連接到此伺服器之用戶端的位址。 可為 Null。|  
|physical_net_transport|**nvarchar （40)**|傳回這項連接所用的實體傳輸通訊協定。 當連接啟用 Multiple Active Result Set (MARS) 時準確。|  
|\<任何其他字串 >||如果輸入無效，則會傳回 NULL。|  
  
## <a name="remarks"></a>備註  
**local_net_address**和**local_tcp_port**傳回 NULL [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。
  
值，會傳回所對應的資料行中所顯示的選項相同[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)動態管理檢視。 例如：
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>另請參閱
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  

