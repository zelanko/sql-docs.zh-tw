---
title: 備份加密金鑰 （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.backupencryptionkey.F1
ms.assetid: eb8c82be-323b-4d86-ab10-c1bf69a4abe3
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 89d5ffa496220bc14b963ebbad08b89b919eec3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37191239"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>備份加密金鑰 (SSRS 原生模式)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 您可以使用 加密金鑰來保護儲存在報表伺服器資料庫中的機密資料。 擁有此金鑰的備份對於確保對加密連接字串和認證的持續存取權非常重要。 如果您要將報表伺服器資料庫移到另一部電腦，或是您要變更報表伺服器服務帳戶的使用者名稱或密碼，您必須擁有此金鑰的備份副本。 這兩個作業都需要從您之前建立的備份副本還原此金鑰。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式。  
  
 若要開啟 [備份加密金鑰] 對話方塊中，按一下**加密金鑰**中的 [瀏覽] 窗格[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Configuration Manager，然後按一下**備份**。 當您更新使用中的 [服務帳戶] 頁面的服務帳戶時，也會出現此對話方塊[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Configuration Manager。 如需詳細資訊[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]組態管理員 中，請參閱[Reporting Services 組態管理員&#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>選項。  
 **檔案位置**  
 指定的檔案名稱和位置[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]對稱金鑰。 對稱金鑰絕不會以純文字的方式儲存。 您必須輸入密碼來保護該檔案。  
  
 **密碼**  
 請輸入可保護檔案的密碼，以防止未經授權的存取。 只有知道此密碼的使用者才能夠還原在檔案內鎖定的金鑰。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會強制執行強式密碼原則。 此密碼至少必須為 8 個字元，以及包含大小寫英數字元和至少一個符號字元的組合。  
  
 **確認密碼**  
 重新輸入您剛剛輸入的密碼。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 F1 說明主題&#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [刪除和重新建立加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [將報表伺服器初始化 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [加密金鑰&#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
