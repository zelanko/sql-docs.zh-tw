---
title: 佈建 PDW 憑證
description: Analytics Platform System 的 PDW 憑證布建頁面 Configuration Manager 匯入或移除 PDW 區域所使用的憑證。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 676335fb8ee4aac5906c61084c28cd94cf8ea815
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400896"
---
# <a name="pdw-certificate-provisioning---analytics-platform-system"></a>PDW 憑證布建-Analytics Platform System
Analytics Platform System 的 **PDW 憑證** 布建頁面 **Configuration Manager** 匯入或移除 PDW 區域所使用的憑證。 使用加密連線的憑證，可以透過 SQL Server 用戶端、使用 SQL Server PDW 驅動程式的工具、 [管理主控台](monitor-the-appliance-by-using-the-admin-console.md)和 Integration Services 載入來協助保護與控制節點的通訊。  
  
## <a name="prerequisites"></a>必要條件  
安裝憑證之前，請執行下列動作：  
  
1.  取得安全的憑證。 如果您需要如何取得安全憑證的詳細資訊，請聯絡 Microsoft 支援服務。  
  
2.  將憑證儲存至受密碼保護的 PFX 檔案中的控制節點。  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>基於安全考慮，請取得受信任的憑證  
SQL Server PDW 支援使用憑證來加密控制節點的連接;包括連接到 **管理主控台**。  
  
根據預設， **管理主控台** 包含可提供隱私權的自我簽署憑證，但不提供伺服器驗證。 這可能會讓通訊容易受到攔截式攻擊。 當使用者使用自我簽署憑證連接到管理主控台時，Internet Explorer 會傳回錯誤：「此網站的安全性憑證有問題」。  
  
雖然透過自我簽署憑證的連線會將用戶端與伺服器之間的傳輸中資料加密，但連線仍有攻擊者的風險。  
  
> [!WARNING]  
> 設備系統管理員應該立即取得憑證，以連結至用戶端所辨識的受信任憑證授權單位單位，以便擁有安全的連線，並移除 Internet Explorer 報告的錯誤。  
  
憑證路徑必須包含對應至控制節點叢集 IP 位址的完整功能變數名稱 (建議的) 或使用者輸入其瀏覽器位址列以存取 **管理主控台**的名稱。  
  
使用 Analytics Platform System**Configuration Manager** 來新增或移除受信任的憑證。 不支援直接使用 Microsoft Windows HTTP Services 憑證設定工具 (**winHttpCertCfg.exe**) 來管理憑證。  
  
## <a name="import-or-remove-the-certificate"></a>匯入或移除憑證  
下列指示說明如何匯入或移除設備證書。

> [!WARNING]
> 若要更新過期的憑證，您必須先移除現有的憑證，然後再匯入新的憑證。
  
### <a name="to-import-the-certificate"></a>匯入憑證  
  
1.  啟動 **Configuration Manager**。 如需詳細資訊，請參閱 [啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在 **Configuration Manager**的左窗格中，展開 [ **平行處理資料倉儲拓撲**]，然後按一下 [ **憑證**]。  
  
3.  選取 [匯 **入憑證] 並設定設備使用它**，然後按一下 **[流覽** ] 以流覽並選取憑證檔案。  
  
4.  在 [ **密碼** ] 欄位中輸入憑證的密碼。  
  
5.  按一下 **[** 套用] 以設定設備的憑證。  
  
SQL Server PDW 將不會使用匯入的憑證來加密目前的連接，但是會將憑證用於新的連接。  
  
### <a name="to-remove-the-previously-imported-certificate"></a>移除先前匯入的憑證  
  
1.  啟動 **Configuration Manager**。 如需詳細資訊，請參閱 [啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在 **Configuration Manager**的左窗格中，展開 [ **平行處理資料倉儲拓撲**]，然後按一下 [ **憑證**]。  
  
3.  選取 **[移除在設備中布建的任何憑證**]。  
  
4.  按一下 **[** 套用] 以從設備移除先前匯入的憑證。  
  
SQL Server PDW 會繼續加密目前的連接，但不會針對新的連接使用移除的憑證。  
  
![DWConfig 應用裝置 PDW 憑證](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>另請參閱  
[啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
