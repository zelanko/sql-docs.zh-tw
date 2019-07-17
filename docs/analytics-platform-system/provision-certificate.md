---
title: 憑證佈建-Analytics Platform System |Microsoft Docs
description: Analytics Platform System 中佈建憑證。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0da49afe13ab0f8cc92e8dd58e78f40564ff53c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960223"
---
# <a name="certificate-provisioning-in-analytics-platform-system"></a>Analytics Platform System 中佈建的憑證
**佈建 PDW 憑證**Analytics Platform System 頁面**Configuration Manager**匯入或移除 PDW 所使用的憑證。 

使用此項目，來加密連線的憑證可以協助保護通訊安全到控制節點，透過 SQL Server 用戶端，使用 SQL Server PDW 驅動程式的工具[管理主控台](monitor-the-appliance-by-using-the-admin-console.md)，並載入 Integration Services。 
  
## <a name="prerequisites"></a>先決條件  
安裝之前的憑證，請執行下列作業：  
  
1.  取得安全的憑證。 如果您需要濆爧髍孮安全憑證的詳細資訊，請連絡 Microsoft 支援服務。  
  
2.  將憑證儲存到控制節點，在密碼保護的 PFX 檔案。  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>基於安全性理由，取得受信任的憑證  
SQL Server PDW 支援使用憑證來加密連接到控制節點中;包含通往**管理主控台**。  
  
根據預設，**管理主控台**包含自我簽署的憑證所提供的隱私權，但不是伺服器驗證。 這可以讓通訊容易受到攔截攻擊。 當使用者連線至管理主控台所使用的自我簽署的憑證時，Internet Explorer 就會傳回錯誤：「 沒有這個網站的安全性憑證有問題 」。  
  
雖然連線的自我簽署憑證透過加密進行中的資料，用戶端與伺服器之間，連線就是仍然有來自攻擊者的風險。  
  
> [!WARNING]  
> 應用裝置系統管理員，應立即取得憑證鏈結至信任的憑證授權單位辨識用戶端，才能有安全的連線，並移除 Internet Explorer 會報告錯誤。  
  
對應到控制節點 （建議選項） 的叢集 IP 位址的完整的網域名稱或使用者存取其瀏覽器位址列中輸入的名稱，必須包含憑證路徑**管理主控台**。  
  
使用 Analytics Platform System**Configuration Manager**新增或移除受信任的憑證。 直接使用 Microsoft Windows HTTP 服務的憑證組態工具 (**winHttpCertCfg.exe**) 來管理憑證不受支援。  
  
## <a name="import-or-remove-the-certificate"></a>匯入或移除憑證  
下列指示說明如何匯入或移除應用裝置的憑證。  
  
### <a name="to-import-the-certificate"></a>若要匯入憑證  
  
1.  啟動**Configuration Manager**。  
如需詳細資訊，請參閱 <<c0> [ 啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。</c0>  

2.  在左窗格中**Configuration Manager**，展開**平行處理資料倉儲拓樸**，然後按一下**憑證**。  
  
3.  選取 **匯入憑證，並設定設備，以使用它**，然後按一下**瀏覽**瀏覽至並選取憑證檔案。  
  
4.  輸入中的憑證的密碼**密碼**欄位。  
  
5.  按一下 **套用**設定設備的憑證。  
  
SQL Server PDW 不使用匯入的憑證，加密目前的連接，但將使用新的連線憑證。  
  
### <a name="to-remove-the-previously-imported-certificate"></a>若要移除先前匯入的憑證  
  
1.  啟動**Configuration Manager**。 

<!-- MISSING LINKS
For more information, see [Launch the Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager-analytics-platform-system.md).  
-->
  
2.  在左窗格中**Configuration Manager**，展開**平行處理資料倉儲拓樸**，然後按一下**憑證**。  
  
3.  選取 **移除佈建設備中的任何憑證**。  
  
4.  按一下 **套用**應用裝置中移除先前匯入的憑證。  
  
SQL Server PDW 加密目前的連線，將會繼續，但不是會針對新的連接使用移除的憑證。  
  
![DWConfig 應用裝置 PDW 憑證](media/dwconfig-appl-pdw-cert.png "DWConfig 應用裝置 PDW 憑證")  
  
## <a name="see-also"></a>另請參閱  
[啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
