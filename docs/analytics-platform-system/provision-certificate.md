---
title: 憑證提供
description: 分析平臺系統中的憑證布建。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 669e65a7d27b208d861a33618d889707134dfefa
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400516"
---
# <a name="certificate-provisioning-in-analytics-platform-system"></a>分析平臺系統中的憑證布建
分析平臺系統的 [ **PDW 憑證提供**] 頁面**Configuration Manager**匯入或移除 PDW 所使用的憑證。 

使用，加密連線的憑證可以透過 SQL Server 用戶端、使用 SQL Server PDW 驅動程式的工具、[管理主控台](monitor-the-appliance-by-using-the-admin-console.md)，以及 Integration Services 載入，協助保護與控制節點的通訊。 
  
## <a name="prerequisites"></a>必要條件  
安裝憑證之前，請執行下列動作：  
  
1.  取得安全憑證。 如果您需要如何取得安全憑證的詳細資訊，請聯絡 Microsoft 支援服務。  
  
2.  將憑證儲存至受密碼保護的 PFX 檔案中的控制節點。  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>基於安全性理由，取得受信任的憑證  
SQL Server PDW 支援使用憑證來加密控制節點的連接;包括與**管理主控台**的連接。  
  
根據預設，**管理主控台**會包含提供隱私權的自我簽署憑證，但不包括伺服器驗證。 這可能會讓通訊容易受到攔截式攻擊。 當使用者使用自我簽署憑證連接到管理主控台時，Internet Explorer 會傳回錯誤：「此網站的安全性憑證有問題」。  
  
雖然透過自我簽署憑證的連線會加密用戶端與伺服器之間的傳輸中資料，但連線仍然會有攻擊者的風險。  
  
> [!WARNING]  
> 設備系統管理員應該立即取得連結至用戶端所識別之受信任憑證授權單位單位的憑證，以便擁有安全連線並移除 Internet Explorer 報告的錯誤。  
  
憑證路徑必須包含對應至控制節點叢集 IP 位址的完整功能變數名稱（建議選項），或使用者在其瀏覽器的網址列中輸入以存取**管理主控台**的名稱。  
  
流量分析平臺系統**Configuration Manager**來新增或移除受信任的憑證。 不支援直接使用 Microsoft Windows HTTP Services 憑證設定工具（**winHTTPcertcfg.exe .exe**）來管理憑證。  
  
## <a name="import-or-remove-the-certificate"></a>匯入或移除憑證  
下列指示說明如何匯入或移除應用裝置憑證。  
  
### <a name="to-import-the-certificate"></a>匯入憑證  
  
1.  啟動**Configuration Manager**。  
如需詳細資訊，請參閱[&#40;分析平臺系統&#41;啟動 Configuration Manager ](launch-the-configuration-manager.md)。  

2.  在**Configuration Manager**的左窗格中，展開 [**平行處理資料倉儲拓撲**]，然後按一下 [**憑證**]。  
  
3.  選取 [匯**入憑證] 並設定設備來使用它**，然後按一下 **[流覽**] 以流覽並選取憑證檔案。  
  
4.  在 [**密碼**] 欄位中輸入憑證的密碼。  
  
5.  按一下 **[** 套用] 以設定設備的憑證。  
  
SQL Server PDW 不會使用匯入的憑證來加密目前的連線，但會針對新的連接使用憑證。  
  
### <a name="to-remove-the-previously-imported-certificate"></a>移除先前匯入的憑證  
  
1.  啟動**Configuration Manager**。 

<!-- MISSING LINKS
For more information, see [Launch the Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager-analytics-platform-system.md).  
-->
  
2.  在**Configuration Manager**的左窗格中，展開 [**平行處理資料倉儲拓撲**]，然後按一下 [**憑證**]。  
  
3.  選取 **[移除在設備上布建的任何憑證**]。  
  
4.  按一下 **[** 套用] 以從設備中移除先前匯入的憑證。  
  
SQL Server PDW 會繼續加密目前的連線，但不會針對新的連接使用已移除的憑證。  
  
![DWConfig 應用裝置 PDW 憑證](media/dwconfig-appl-pdw-cert.png "DWConfig 設備 PDW 憑證")  
  
## <a name="see-also"></a>另請參閱  
[啟動 Configuration Manager &#40;分析平臺系統&#41;](launch-the-configuration-manager.md)  
