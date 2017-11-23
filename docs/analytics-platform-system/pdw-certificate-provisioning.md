---
title: "PDW 憑證佈建 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a423b7d-c6ea-45c1-80b0-26758170594c
caps.latest.revision: "22"
ms.openlocfilehash: f0134ec239b938ee7ace6fc6dc05e130fb844b2f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="pdw-certificate-provisioning"></a>PDW 憑證佈建
**PDW 憑證佈建**頁面 Analytics Platform System**Configuration Manager**匯入或移除 PDW 區域所使用的憑證。 使用，來加密連接的憑證可協助安全的通訊透過 SQL Server 用戶端，可以使用 SQL Server PDW 驅動程式的工具的控制節點到[管理主控台](monitor-the-appliance-by-using-the-admin-console.md)，和 Integration Services 就會載入。  
  
## <a name="prerequisites"></a>必要條件  
安裝之前的憑證，請執行下列作業：  
  
1.  取得安全的憑證。 如果您需要有關如何取得安全的憑證的詳細資訊，請連絡 Microsoft 支援服務。  
  
2.  將憑證儲存到受密碼保護 PFX 檔案中的控制項節點。  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>基於安全性理由，取得受信任的憑證  
SQL Server PDW 支援使用憑證來加密連接的控制節點。包括連線**管理主控台**。  
  
根據預設，**管理主控台**包含自我簽署的憑證所提供的隱私權，但不是伺服器驗證。 這可以讓通訊容易受到攔截的攻擊。 當使用者連線到系統管理員主控台所使用的自我簽署的憑證時，Internet Explorer 會傳回錯誤: 「 有 」 這個網站的安全性憑證有問題。  
  
雖然自我簽署憑證透過連線進行加密用戶端與伺服器之間傳遞資料，連線仍然是遭受攻擊的風險。  
  
> [!WARNING]  
> 應用裝置系統管理員應該立即取得憑證，以辨識用戶端，才能有安全的連線，並移除 Internet Explorer 會報告此錯誤的受信任的憑證授權單位鏈結。  
  
憑證路徑必須包含完整的網域名稱可對應至控制項節點叢集 IP 位址 （建議選項） 或存取其瀏覽器位址列中輸入使用者名稱**管理主控台**。  
  
使用 Analytics Platform System**Configuration Manager**新增或移除受信任的憑證。 直接使用 Microsoft Windows HTTP 服務的憑證組態工具 (**winHttpCertCfg.exe**) 來管理憑證不受支援。  
  
## <a name="import-or-remove-the-certificate"></a>匯入或移除憑證  
下列指示說明如何匯入或移除應用裝置的憑證。  
  
### <a name="to-import-the-certificate"></a>匯入憑證  
  
1.  啟動**Configuration Manager**。 如需詳細資訊，請參閱[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md).  
  
2.  在左窗格中**Configuration Manager**，依序展開**平行資料倉儲拓樸**，然後按一下 **憑證**。  
  
3.  選取**匯入憑證，並設定使用該應用裝置**，然後按一下 **瀏覽**瀏覽至並選取憑證檔案。  
  
4.  輸入的密碼中的憑證**密碼**欄位。  
  
5.  按一下**套用**設定應用裝置的憑證。  
  
SQL Server PDW 不使用匯入的憑證，加密目前的連接，但會針對新的連接使用憑證。  
  
### <a name="to-remove-the-previously-imported-certificate"></a>若要移除先前匯入的憑證  
  
1.  啟動**Configuration Manager**。 如需詳細資訊，請參閱[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md).  
  
2.  在左窗格中**Configuration Manager**，依序展開**平行資料倉儲拓樸**，然後按一下 **憑證**。  
  
3.  選取**移除佈建應用裝置中的任何憑證**。  
  
4.  按一下**套用**應用裝置中移除先前匯入的憑證。  
  
SQL Server PDW 會繼續目前的連接加密，但不是會針對新的連接使用移除的憑證。  
  
![DWConfig 應用裝置 PDW 憑證](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>請參閱＜  
[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
