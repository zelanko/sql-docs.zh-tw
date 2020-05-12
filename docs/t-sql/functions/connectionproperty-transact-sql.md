---
title: CONNECTIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONNECTIONPROPERTY_TSQL
- CONNECTIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- CONNECTIONPROPERTY statement
ms.assetid: 6bd9ccae-af77-4a05-b97f-f8ab41cfde42
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a5cf9d02986587ed3e5234343306d6d73c7203a7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832228"
---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

至於傳入至伺服器的要求，若有獨特的連線支援該要求，則此函數會傳回其連線屬性的相關資訊。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>引數  
*property*  
連線的屬性。 *property* 可以是下列值之一：
  
|值|資料類型|描述|  
|---|---|---|
|net_transport|**nvarchar(40)**|傳回此連線使用的實體傳輸通訊協定。 這個值不可為 Null。 可能的傳回值：<br /><br /> **HTTP**<br /> **具名管道**<br /> **工作階段**<br /> **共用記憶體**<br /> **SSL**<br /> **TCP**<br /><br /> 和<br /><br /> **VIA**<br /><br /> 注意：當連線同時啟用 Multiple Active Result Set (MARS) 和連線共用之後，一律會傳回**工作階段**。|  
|protocol_type|**nvarchar(40)**|傳回裝載通訊協定型別。 它目前會區分 TDS (TSQL) 和 SOAP。 可為 Null。|  
|auth_scheme|**nvarchar(40)**|傳回連線 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證配置。 驗證配置為 Windows 驗證 (NTLM、KERBEROS、DIGEST、BASIC、NEGOTIATE) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 不可為 Null。|  
|local_net_address|**varchar(48)**|傳回此特定連線目標伺服器的 IP 位址。 只適用於使用 TCP 傳輸提供者的連線。 可為 Null。|  
|local_tcp_port|**int**|如果這項連線是使用 TCP 傳輸的連線，傳回這項連線的目標伺服器 TCP 埠。 可為 Null。|  
|client_net_address|**varchar(48)**|針對嘗試與此伺服器連線的用戶端，要求用戶端的位址。 可為 Null。|  
|physical_net_transport|**nvarchar(40)**|傳回此連線使用的實體傳輸通訊協定。 當連接啟用 Multiple Active Result Set (MARS) 時準確。|  
|\<任何其他字串>||輸入無效時，會傳回 NULL。|  
  
## <a name="remarks"></a>備註  
**local_net_address** 和 **local_tcp_port** 會在 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 中傳回 NULL。
  
傳回的值與針對 [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md) 動態管理檢視中對應資料行所顯示的選項相同。 例如：
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>另請參閱
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  
