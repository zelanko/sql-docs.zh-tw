---
title: 設定和管理加密金鑰 (SSRS 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- private keys [Reporting Services]
- cryptography [Reporting Services]
- symmetric keys [Reporting Services]
- encryption [Reporting Services]
- public keys [Reporting Services]
ms.assetid: 58e61636-88a2-4338-ae5f-3dd210aee887
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 16a1851a46b6602bc9d92d5c7e0111ece8701d43
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222508"
---
# <a name="configure-and-manage-encryption-keys-ssrs-configuration-manager"></a>設定和管理加密金鑰 (SSRS 組態管理員)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用加密金鑰來保護儲存於報表伺服器資料庫中之認證和連線資訊的安全。 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，可透過用於保護敏感性資料的公開、私密和對稱金鑰組合來支援加密。 當您安裝或設定報表伺服器時，對稱金鑰會在報表伺服器起始設定期間建立，供報表伺服器用來對儲存於報表伺服器中之機密資料進行加密。 公開金鑰和私密金鑰是由作業系統所建立，可用來保護對稱金鑰。 針對負責儲存報表伺服器資料庫中之機密資料的每一個報表伺服器執行個體，建立一組公開金鑰和私密金鑰。  
  
 加密金鑰的管理包括建立對稱金鑰的備份副本，以及了解還原、刪除或變更金鑰的時機和方法。 如果您移轉報表伺服器安裝架構或設定向外延展部署，您必須擁有一份對稱金鑰的備份，才能將其套用於新的安裝架構。  
  
> [!IMPORTANT]  
>  定期變更 Reporting Services 加密金鑰是安全性最佳作法。 建議您在進行 Reporting Services 的主要版本升級之後，立即變更金鑰。 在升級之後變更金鑰可將升級循環以外，由變更 Reporting Services 加密金鑰所造成的其他服務中斷減至最少。  
  
 若要管理對稱金鑰，可以使用 Reporting Services 組態工具或 **rskeymgmt** 公用程式。 隨附於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的工具只能用來管理對稱金鑰 (公開金鑰和私密金鑰則由作業系統負責管理)。 Reporting Services 組態工具和 **rskeymgmt** 公用程式皆支援下列工作：  
  
-   備份對稱金鑰的副本，讓您能夠使用金鑰來復原報表伺服器安裝，或做為計劃移轉的一部分。  
  
-   還原先前儲存的對稱金鑰到報表伺服器資料庫，可以讓新報表伺服器執行個體存取它原先未加密的現有資料。  
  
-   在極罕見的無法再存取加密資料的事件中，刪除報表伺服器資料庫中的加密金鑰。  
  
-   在極罕見的對稱金鑰受到危害的事件中，重新建立對稱金鑰並重新將資料加密。 就安全性最佳做法而言，您應定期重新建立對稱金鑰 (例如，每幾個月)，以保護報表伺服器資料庫免於駭客進行破解金鑰的攻擊。  
  
-   在向外延展部署中加入或移除報表伺服器執行個體，其中多個報表伺服器共用單一報表伺服器資料庫和能加解密該資料庫的對稱金鑰。  
  
## <a name="in-this-section"></a>本節內容  
 [初始化報表伺服器&#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-initialize-a-report-server.md)  
 說明如何建立加密金鑰。  
  
 [備份與還原 Reporting Services 加密金鑰](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
 說明如何備份加密金鑰，並還原金鑰以復原或移轉報表伺服器安裝。  
  
 [儲存加密的報表伺服器資料&#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
 描述報表伺服器的加密。  
  
 [刪除並重新建立加密金鑰&#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)  
 說明如何以新版本取代對稱金鑰，以及如果無法驗證對稱金鑰，應如何重新建立。  
  
 [新增和移除向外延展部署的加密金鑰&#40;SSRS 組態管理員&#41;](add-and-remove-encryption-keys-for-scale-out-deployment.md)  
 說明如何加入和移除加密金鑰，以控制哪些報表伺服器屬於向外延展部署的一部分。  
  
## <a name="see-also"></a>另請參閱  
 [儲存加密的報表伺服器資料&#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
