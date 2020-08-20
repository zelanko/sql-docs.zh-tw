---
description: sys.certificates (Transact-SQL)
title: sys. 憑證 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 95e4d3b3b1b06810fc1e60564a4ad7c84e85189a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486516"
---
# <a name="syscertificates-transact-sql"></a>sys.certificates (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  針對資料庫中的每個憑證，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|憑證的名稱。 在資料庫中，這是唯一的。|  
|**certificate_id**|**int**|憑證的識別碼。 在資料庫中，這是唯一的。|  
|**principal_id**|**int**|擁有這個憑證的資料庫主體識別碼。|  
|**pvt_key_encryption_type**|**char(2)**|如何為私密金鑰加密。<br /><br /> NA = 憑證沒有私密金鑰<br /><br /> MK = 私密金鑰是由主要金鑰加密<br /><br /> PW = 私密金鑰是由使用者自訂密碼加密<br /><br /> SK = 私密金鑰是由服務主要金鑰加密。|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|私密金鑰加密方式的描述。<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**is_active_for_begin_dialog**|**bit**|如果是 1，則這個憑證是用來起始加密的服務對話。|  
|**issuer_name**|**Nvarchar (442) **|憑證簽發者的名稱。|  
|**cert_serial_number**|**Nvarchar (64) **|憑證的序號。|  
|**希**|**Varbinary (85) **|這個憑證的登入 SID。|  
|**string_sid**|**nvarchar(128)**|這個憑證登入 SID 的字串表示法|  
|**subject**|**nvarchar(4000)**|這個憑證的主旨。|  
|**expiry_date**|**datetime**|當憑證逾期時。|  
|**start_date**|**datetime**|當憑證生效時。|  
|**指紋**|**varbinary(32)**|憑證的 SHA-1 雜湊。 SHA-1 雜湊在全域範圍內是唯一的。|  
|**attested_by**|**nvarchar(260)**|僅供系統使用。|  
|**pvt_key_last_backup_date**|**datetime**|上次匯出憑證私密金鑰的日期和時間。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
  
