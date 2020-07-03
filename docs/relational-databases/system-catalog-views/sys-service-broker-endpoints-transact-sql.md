---
title: sys.databases service_broker_endpoints （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_broker_endpoints_TSQL
- service_broker_endpoints
- service_broker_endpoints_TSQL
- sys.service_broker_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_broker_endpoints catalog view
ms.assetid: 6979ec9b-0043-411e-aafb-0226fa26c5ba
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 86a7fb5a83fe8e12f6721328e69c45e40e57eb46
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897905"
---
# <a name="sysservice_broker_endpoints-transact-sql"></a>sys.service_broker_endpoints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  這份目錄檢視會針對 Service Broker 端點，各包含一個資料列。 對於此視圖中的每個資料列，在包含 TCP 設定中繼資料的 [ **tcp_endpoints** ] 視圖中，都有一個具有相同**endpoint_id**的對應資料列。 TCP 是 Service Broker 唯一允許使用的通訊協定。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|**--**|從 sys.databases 繼承[&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)的資料行。|  
|**is_message_forwarding_enabled**|**bit**|端點支援訊息轉送。 這一開始會設定為**0** （已停用）。 不是 NULLABLE。|  
|**message_forwarding_size**|**int**|允許用於轉送訊息之**tempdb**空間的最大 mb 數。 這一開始會設定為**10**。 不是 NULLABLE。|  
|**connection_auth**|**tinyint**|與這個端點連接所需的連接驗證類型，它有下列幾種：<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -NEGOTIATE<br /><br /> **4** -憑證<br /><br /> **5** -NTLM、憑證<br /><br /> **6** -KERBEROS、憑證<br /><br /> **7** -NEGOTIATE，憑證<br /><br /> **8** -憑證、NTLM<br /><br /> **9** -憑證、KERBEROS<br /><br /> **10** -CERTIFICATE、NEGOTIATE<br /><br /> 不是 NULLABLE。|  
|**connection_auth_desc**|**nvarchar(60)**|與這個端點連接所需之連接類型的描述，它有下列幾種：<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM、CERTIFICATE<br /><br /> KERBEROS、CERTIFICATE<br /><br /> NEGOTIATE、CERTIFICATE<br /><br /> CERTIFICATE、NTLM<br /><br /> CERTIFICATE、KERBEROS<br /><br /> CERTIFICATE、NEGOTIATE<br /><br /> NULLABLE。|  
|**certificate_id**|**int**|驗證所用的憑證識別碼 (如果有的話)。<br /><br /> 0 = 正在使用 Windows 驗證。|  
|**encryption_algorithm**|**tinyint**|加密演算法。 以下是其描述和對應 DDL 選項的可能值。<br /><br /> **0** ：無。 對應的 DDL 選項：已停用。<br /><br /> **1** ： RC4。 對應的 DDL 選項： {必要的 &#124; 需要的演算法 RC4}。<br /><br /> **2** ： AES。 對應的 DDL 選項：必要的演算法 AES。<br /><br /> **3** ： NONE、RC4。 對應的 DDL 選項： {支援的 &#124; 支援的演算法 RC4}。<br /><br /> **4** ： NONE、AES。 對應的 DDL 選項：支援的演算法 AES。<br /><br /> **5** ： RC4、AES。 對應的 DDL 選項：必要的演算法 RC4 AES。<br /><br /> **6** ： AES、RC4。 對應的 DDL 選項：必要的演算法 AES RC4。<br /><br /> **7** ： NONE、RC4、AES。 對應的 DDL 選項：支援的演算法 RC4 AES。<br /><br /> **8** ： NONE、AES、RC4。 對應的 DDL 選項：支援的演算法 AES RC4。<br /><br /> 不是 NULLABLE。|  
|**encryption_algorithm_desc**|**nvarchar(60)**|加密演算法描述。 可能的值和其對應的 DDL 選項如下所示：<br /><br /> 無：已停用<br /><br /> RC4： {必要的 &#124; 需要的演算法 RC4}<br /><br /> AES：必要的演算法 AES<br /><br /> 無、RC4： {支援 &#124; 支援的演算法 RC4}<br /><br /> 無，AES：支援的演算法 AES<br /><br /> RC4，AES：必要的演算法 RC4 AES<br /><br /> AES，RC4：必要的演算法 AES RC4<br /><br /> NONE、RC4、AES：支援的演算法 RC4 AES<br /><br /> NONE、AES、RC4：支援的演算法 AES RC4<br /><br /> NULLABLE。|  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]  
>  只有 RC4 演算法支援回溯相容性。 只有在資料庫相容性層級為 90 或 100 時，才能使用 RC4 或 RC4_128 加密新資料  (不建議使用)。請改用較新的演算法，例如其中一個 AES 演算法。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本中使用 RC4 或 RC4_128 加密的資料，可以在任何相容性層級進行解密。  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
