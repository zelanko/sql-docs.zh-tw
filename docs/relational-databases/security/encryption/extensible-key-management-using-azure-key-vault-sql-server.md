---
title: 使用 Azure Key Vault 進行可延伸金鑰管理 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Extensible Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
- EKM, with key vault
- TDE, EKM and key vault
- Key Management with key vault
- SQL Server Connector, about
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
caps.latest.revision: 66
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 5d9a6276f2f166613a2f99f33fa10aabe78247ec
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37972291"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>使用 Azure Key Vault 進行可延伸金鑰管理 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  適用於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure 金鑰保存庫的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密使用 Azure 金鑰保存庫服務作為[可延伸金鑰管理 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md) 提供者，以保護 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密金鑰。  
  
 本主題描述 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器。 [使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)、[搭配使用 SQL Server 連接器與 SQL 加密功能](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)和 [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)中提供其他資訊。  
  
##  <a name="Uses"></a> 什麼是可延伸金鑰管理 (EKM) 以及使用它的原因？  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供數種類型的加密來協助保護敏感性資料，包括[透明資料加密 &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)、[資料行層級加密](../../../t-sql/functions/cryptographic-functions-transact-sql.md) (CLE) 和[備份加密](../../../relational-databases/backup-restore/backup-encryption.md)。 在上述所有情況的這個傳統金鑰階層中，資料會使用對稱資料加密金鑰 (DEK) 進行加密。 對稱資料加密金鑰會以儲存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的金鑰階層加密，受到更進一步的保護。 替代方案是 EKM 提供者模型，而不是此模型。 使用 EKM 提供者架構可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 透過儲存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之外部密碼編譯提供者中的非對稱金鑰，來保護資料加密金鑰。 此模型會多增加一層安全性，並分開管理金鑰和資料。  
   
 下圖比較使用 Azure 金鑰保存庫系統的傳統服務管理金鑰階層。  
  
 ![ekm-key-hierarchy-traditional](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-traditional.png "ekm-key-hierarchy-traditional")  
  
   
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器是作為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 與 Azure 金鑰保存庫之間的橋接器，因此 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以運用 Azure 金鑰保存庫服務的延展性、高效能和高可用性。 下圖代表金鑰階層架構在具有 Azure 金鑰保存庫和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器的 EKM 提供者架構中的運作方式。  
  
  Azure 金鑰保存庫可以與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Azure 虛擬機器和內部部署伺服器上的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 安裝搭配使用。 金鑰保存庫服務也提供選項，以使用受到緊密控制和監視的硬體安全性模組 (HSM)，對非對稱加密金鑰提供更高等級的保護。 如需金鑰保存庫的詳細資訊，請參閱 [Azure 金鑰保存庫](http://go.microsoft.com/fwlink/?LinkId=521401)。  
  
 下列影像摘要說明使用金鑰保存庫的 EKM 處理流程。 (影像中的程序步驟數字並非用以比對遵循影像的安裝步驟數字。)  
  
 ![使用 Azure Key Vault 的 SQL Server EKM](../../../relational-databases/security/encryption/media/ekm-using-azure-key-vault.png "使用 Azure Key Vault 的 SQL Server EKM")  

> [!NOTE]  
>  1.0.0.440 版和較舊版本皆已被取代，而且生產環境也不再支援。 請前往 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=45344) ，使用＜SQL Server 連接器升級＞下 [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) 頁面上的指示，升級為 1.0.1.0 版或更新版本。
  
 如需下一個步驟，請參閱 [使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)。  
  
 如需使用案例，請參閱 [搭配使用 SQL Server 連接器與 SQL 加密功能](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
