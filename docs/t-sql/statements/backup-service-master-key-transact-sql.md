---
title: BACKUP SERVICE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BACKUP SERVICE MASTER KEY
- DUMP_SERVICE_MASTER_KEY_TSQL
- DUMP SERVICE MASTER KEY
- BACKUP_SERVICE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backing up service master keys [SQL Server]
- BACKUP SERVICE MASTER KEY statement
- cryptography [SQL Server], Service Master Key
- exporting Service Master Keys
- encryption [SQL Server], Service Master Key
- service master key [SQL Server], exporting
ms.assetid: f8356683-6680-4f1c-9eaf-5c29a9a9020d
caps.latest.revision: 29
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b11484c047505d0e53f4fedd908057a448ed3b14
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37786999"
---
# <a name="backup-service-master-key-transact-sql"></a>BACKUP SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  匯出服務主要金鑰。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
BACKUP SERVICE MASTER KEY TO FILE = 'path_to_file'   
    ENCRYPTION BY PASSWORD = 'password'  
```  
  
## <a name="arguments"></a>引數  
 FILE **='***path_to_file***'**  
 指定要作為服務主要金鑰匯出目的地之檔案的完整路徑，包含檔案名稱。 這可能是本機路徑或是通往網路位置的 UNC 路徑。  
  
 PASSWORD **='***password***'**  
 這是用來加密備份檔案中之服務主要金鑰的密碼。 這個密碼必須遵守複雜性檢查。 如需詳細資訊，請參閱＜ [Password Policy](../../relational-databases/security/password-policy.md)＞。  
  
## <a name="remarks"></a>Remarks  
 應該將服務主要金鑰備份並儲存至安全的離站位置。 建立這個備份，應該是必須在伺服器上執行的首要管理動作之一。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
 在下列範例中，服務主要金鑰是備份至檔案。  
  
```  
BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_key' ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)  
  
  
