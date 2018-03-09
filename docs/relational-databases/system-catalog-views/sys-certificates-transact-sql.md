---
title: "sys.certificates (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- certificates
- certificates_TSQL
- sys.certificates_TSQL
- sys.certificates
dev_langs:
- TSQL
helpviewer_keywords:
- sys.certificates catalog view
ms.assetid: e5046102-a65c-401e-b80d-05636884dec9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 60cb7a204aaa38a3aaaa24b8c04bb676715de783
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="syscertificates-transact-sql"></a>sys.certificates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對資料庫中的每個憑證，各傳回一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|憑證的名稱。 在資料庫中，這是唯一的。|  
|**certificate_id**|**int**|憑證的識別碼。 在資料庫中，這是唯一的。|  
|**principal_id**|**int**|擁有這個憑證的資料庫主體識別碼。|  
|**pvt_key_encryption_type**|**char(2)**|如何為私密金鑰加密。<br /><br /> NA = 憑證沒有私密金鑰<br /><br /> MK = 私密金鑰是由主要金鑰加密<br /><br /> PW = 私密金鑰是由使用者自訂密碼加密<br /><br /> SK = 私密金鑰是由服務主要金鑰加密。|  
|**pvt_key_encryption_type_desc**|**nvarchar （60)**|私密金鑰加密方式的描述。<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**is_active_for_begin_dialog**|**bit**|如果是 1，則這個憑證是用來起始加密的服務對話。|  
|**issuer_name**|**nvarchar(442)**|憑證簽發者的名稱。|  
|**cert_serial_number**|**nvarchar （64)**|憑證的序號。|  
|**sid**|**varbinary(85)**|這個憑證的登入 SID。|  
|**string_sid**|**nvarchar （128)**|這個憑證登入 SID 的字串表示法|  
|**主體**|**nvarchar(4000)**|這個憑證的主旨。|  
|**expiry_date**|**datetime**|當憑證逾期時。|  
|**start_date**|**datetime**|當憑證生效時。|  
|**憑證指紋**|**varbinary(32)**|憑證的 SHA-1 雜湊。 SHA-1 雜湊在全域範圍內是唯一的。|  
|**attested_by**|**nvarchar （260)**|僅供系統使用。|  
|pvt_key_last_backup_date|**datetime**|憑證的私密金鑰上一次匯出的日期和時間。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
  
