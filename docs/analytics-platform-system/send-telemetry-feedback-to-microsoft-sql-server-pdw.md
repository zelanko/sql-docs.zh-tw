---
title: 將遙測意見反應傳送給 Microsoft (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40a994f0-7eff-4db9-9572-401d6e1187a0
caps.latest.revision: 18
ms.openlocfilehash: 970533d5c0220ac651074977f7f522a480d5e2a4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="send-telemetry-feedback-to-microsoft"></a>將遙測意見反應傳送給 Microsoft
Analytics Platform System 具有選擇性的遙測功能，系統管理員主控台資料傳送給 Microsoft。 我們建議您啟用這個選項來協助我們改善產品。  
  
> [!NOTE]  
> 在此版本中，Microsoft 並不會主動監視的遙測資料。 僅供分析收集的資料。  
  
## <a name="privacy"></a>隱私權  
若要提供的最大隱私權保護，AP 隨附不啟用遙測。 再啟用這個功能，先檢閱[Microsoft Analytics Platform System 隱私權聲明](http://go.microsoft.com/fwlink/?LinkId=400902)。 然後，來選擇加入執行 PowerShell 指令碼如下所述。  
  
## <a name="enable"></a>啟用遙測  
**DNS 轉寄：**遙測資料傳送給 Microsoft 需要 Analytics Platform System，DNS 轉寄站透過網際網路連線。 若要啟用這項功能，您必須啟用轉送上的所有主機和工作負載 Vm 的 DNS。 叫用`Enable-RemoteMonitoring`命令搭配`SetupDnsForwarder`正確設定 DNS 轉送，並啟用遙測的選項。 叫用`Enable-RemoteMonitoring`命令，而`SetupDnsForwarder`選項時已設定 DNS 轉送，而且您只想要啟用活動訊號監視。  
  
> [!IMPORTANT]  
> 啟用 DNS 轉寄，便會開啟所有主機和工作負載 Vm 的網際網路連線。  
  
#### <a name="to-enable-feedback"></a>若要啟用的意見反應  
  
1.  使用應用裝置的網域系統管理員帳戶，連接到的控制節點 (***appliance_domain *-CTL01**)，然後開啟命令提示字元中使用 Windows 系統管理員認證。  
  
2.  瀏覽至下列目錄： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  匯入模組 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要匯入您必須使用兩個句點命令中。  
  
    **範例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  叫用`Enable-RemoteMonitoring`命令。  
  
    > [!NOTE]  
    > 指令碼會假設的網際網路連線正常運作，並不會驗證網際網路連線。  
  
    1.  第一次啟用遙測，會使用下列命令，確定已正確設定所有 DNS 轉寄站。 在此範例中，取代 DNS 轉送 IP 位址`xx.xx.xx.xx`與您的環境中的 DNS 轉寄站 IP 位址。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  當已設定 DNS 轉寄站，例如重新啟用已停用遙測時，使用下列命令來啟用遙測但未設定 DNS 轉寄。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  系統會提示您讀取和認可 AP 會收集應用裝置的相關資訊。 會有您可以複製並貼到 檢閱任何網際網路瀏覽器的 APS 隱私權陳述式的連結。  
  
6.  輸入**Y**接受及選擇加入意見反應，或輸入**N**不接受。  
  
7.  如果您輸入**Y**會有一系列的命令會執行遙測 （並可選擇 DNS 轉寄站） 可讓您的應用裝置上的功能。 如果您看到任何錯誤或資訊將引導您認為命令已不成功，請連絡 CSS，以取得協助。  
  
如果您輸入**N**、 會執行任何命令，將不會啟用此功能和任何您必須執行的動作。  
  
在執行沒有壞處`Enable-RemoteMonitoring`命令多次。 如果已設定 DNS 轉寄站就會警告訊息，指出此情況下。  
  
## <a name="disable"></a>停用遙測  
停用遙測，將會停止通訊狀態監視雲端服務 ap 應用裝置的相關資訊的所有作業。  
  
> [!IMPORTANT]  
> 執行此作業將會停用您的 DNS 轉寄站或網際網路連線可能是由應用裝置中的其他功能的使用中。  
  
#### <a name="to-disable-telemetry"></a>若要停用遙測  
  
1.  使用應用裝置的網域系統管理員帳戶，連接到的控制節點 (***appliance_domain *-CTL01**) 並以系統管理員權限開啟 PowerShell 視窗。  
  
2.  瀏覽至下列目錄： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  匯入模組 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要匯入您必須使用兩個句點命令中。  
  
    **範例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  叫用`Disable-RemoteMonitoring`命令，而參數。 此命令會停止傳送意見反應。 （這不會影響本機監視。）不過，命令將會不停用 DNS 轉寄站及/或停用任何網際網路連線。 這都必須成功地停用的意見反應之後手動完成。  
  
    **範例：**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
如果您看到任何錯誤或資訊將引導您認為命令已不成功，請連絡 CSS，以取得協助。  
  
在執行沒有壞處`Disable-RemoteMonitoring`命令多次。  
  
## <a name="see-also"></a>另請參閱  
[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
[使用系統檢視表來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
[使用 System Center Operations Manager 監視的應用裝置&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
[使用 DNS 轉寄站 dns 名稱解析非應用裝置&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
