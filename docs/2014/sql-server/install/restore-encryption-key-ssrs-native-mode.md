---
title: 還原加密金鑰 （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.restoreencryptionkey.F1
ms.assetid: 11ce51e5-f5d4-40b6-88d8-9360fb50e66c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9e85f9c17a28ba5c416bcab4853af9bdd823611f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126916"
---
# <a name="restore-encryption-key-ssrs-native-mode"></a>還原加密金鑰 (SSRS 原生模式)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用加密金鑰來保護儲存於報表伺服器資料庫中的敏感性資料安全。 為了確保您可持續存取加密的資料，一定要建立加密金鑰的備份，以免日後因為服務帳戶變更或進行規劃移轉時需要還原加密金鑰。 本主題提供如何使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員還原金鑰的概觀。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式。  
  
 若要還原此金鑰，您之前必須已經將此金鑰的備份副本儲存成受密碼保護的檔案。 在金鑰還原期間，報表伺服器將會以受密碼保護之檔案中找到的金鑰來取代現有的金鑰。 該檔案內的金鑰必須與用來加密和解密資料的金鑰相同。  
  
 若要確認您是否已還原有效的金鑰，請使用報表管理員來檢視訂閱或是任何具有使用預存認證之資料來源的報表。 如果當您嘗試開啟訂閱定義頁面時，收到「報表伺服器無法存取加密資料」錯誤，或是當您開啟之前針對報表資料來源使用預存認證的報表時，系統提示您輸入認證，則表示您還原了無效的金鑰。  
  
 如果您所還原的無效金鑰與之前用來加密資料的金鑰不同，這樣就無法針對目前儲存於報表伺服器資料庫內的資料進行解密。 如果您還原無效的金鑰，您應該立即還原正確金鑰的備份副本 (如果可用的話)。 如果您沒有之前用來加密資料之金鑰的備份副本，則必須刪除所有加密的資料。 按一下 **加密金鑰** 頁面上的 [[刪除]](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md) 按鈕，以執行這個步驟。 當您刪除加密的內容之後，您必須手動更新所有訂閱，並重新指定報表伺服器上針對報表和資料驅動訂閱所定義的所有預存認證。  
  
## <a name="restore-encryption-key-dialog"></a>[還原加密金鑰] 對話方塊  
 哪裡可以找到有關[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]組態管理員 中，請參閱[Reporting Services 組態管理員&#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 若要開啟 [還原加密金鑰] 對話方塊，請按一下 **組態管理員導覽窗格內的** [加密金鑰] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，然後按一下 **[還原]**。 當您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員內的 [服務帳戶] 頁面來更新服務帳戶時，這個對話方塊也會出現。 如需詳細資訊  
  
## <a name="options"></a>選項。  
 **檔案位置**  
 選取包含對稱金鑰副本的受密碼保護檔案。 預設的副檔名為 .snk。  
  
 **密碼**  
 輸入解除檔案鎖定的密碼。 只有知道此密碼的使用者才可以還原金鑰。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會強制實施增強式密碼原則。 此密碼至少必須包含 8 個字元，以及包含大小寫英數字元和至少一個符號字元的組合。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 F1 說明主題&#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [刪除和重新建立加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [將報表伺服器初始化 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [加密金鑰&#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
