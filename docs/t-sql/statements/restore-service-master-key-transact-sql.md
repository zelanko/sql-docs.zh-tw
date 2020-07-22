---
title: RESTORE SERVICE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RESTORE SERVICE MASTER KEY
- RESTORE_SERVICE_MASTER_KEY_TSQL
- LOAD SERVICE MASTER KEY
- LOAD_SERVICE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- importing Service Master Keys
- copying Service Master Keys
- service master key [SQL Server], importing
- RESTORE SERVICE MASTER KEY statement
- transferring Service Master Keys
ms.assetid: a68fd0ee-70ce-4104-aca0-fcae5f41fc38
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8565124ea527b5c9de885a5b342d6368b99149d6
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86482970"
---
# <a name="restore-service-master-key-transact-sql"></a>RESTORE SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從備份檔案匯入服務主要金鑰。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
RESTORE SERVICE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password' [FORCE]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 FILE **='** _path\_to\_file_ **'**  
 指定預存服務主要金鑰的完整路徑，包括檔案名稱。 *path_to_file* 可以是本機路徑或通往網路位置的 UNC 路徑。  
  
 PASSWORD **='** _password_ **'**  
 指定解密要從檔案匯入之服務主要金鑰時所需的密碼。  
  
 FORCE  
 即使有遺失資料的風險，仍強制更換服務主要金鑰。  
  
## <a name="remarks"></a>備註  
 當還原服務主要金鑰時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會解密所有已利用目前的服務主要金鑰來加密的金鑰和秘密，然後利用從備份檔案載入的服務主要金鑰來加密它們。  
  
 如果任何一項解密失敗，還原便會失敗。 您可以利用 FORCE 選項來省略錯誤，但這個選項會使所有無法解密的資料遺失。  
  
> [!CAUTION]  
>  服務主要金鑰是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 加密階層的根。 服務主要金鑰會直接或間接維護樹狀結構中之所有其他金鑰的安全。 如果在強制還原作業進行期間某相依金鑰無法解密，由該金鑰維護其安全的資料便會遺失。  
  
 重新產生加密階層是一項需要大量資源的作業。 您應該將這項作業安排在低需求時進行。  
  
## <a name="permissions"></a>權限  
 需要伺服器的 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例從備份檔案還原服務主要金鑰。  
  
```  
RESTORE SERVICE MASTER KEY   
    FROM FILE = 'c:\temp_backups\keys\service_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [服務主要金鑰](../../relational-databases/security/encryption/service-master-key.md)   
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)