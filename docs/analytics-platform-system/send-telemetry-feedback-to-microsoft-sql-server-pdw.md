---
title: 遙測意見反應-Analytics Platform System |Microsoft Docs
description: 將遙測意見反應傳送給 Microsoft 分析平台系統。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 442505d470d1c7b7a82a02610d650d9f0b8c8d07
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678382"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>將遙測意見反應傳送給 Microsoft 分析平台系統
Analytics Platform System 有一項選擇性的遙測功能，管理主控台資料傳送給 Microsoft。 
  
> [!NOTE]  
> 在此版本中，Microsoft 並不會主動監視的遙測資料。 僅供分析所收集的資料。  
  
## <a name="privacy"></a>隱私權  
若要提供的最大的隱私權保護，AP 隨附不啟用遙測。 在之前啟用這項功能，請先檢閱[Microsoft Analytics Platform System Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=400902)。 若要參加，執行如下所述的 PowerShell 指令碼。  
  
## <a name="enable"></a>啟用遙測  
**DNS 轉送：** 將遙測資料傳送給 Microsoft 需要透過 DNS 轉寄站的網際網路連線的 Analytics Platform System。 若要啟用這項功能，您必須啟用 DNS 轉寄所有主機和工作負載 Vm 上。 叫用`Enable-RemoteMonitoring`命令搭配`SetupDnsForwarder`選項才能正確設定 DNS 轉送，並啟用遙測。 叫用`Enable-RemoteMonitoring`命令不含`SetupDnsForwarder`當已設定 DNS 轉送，而您只想要啟用活動訊號監視時。  
  
> [!IMPORTANT]  
> 啟用 DNS 轉送會開啟 所有主機和工作負載 Vm 的網際網路連線。  
  
#### <a name="to-enable-feedback"></a>若要啟用的意見反應  
  
1.  使用設備的網域系統管理員帳戶，連接到控制節點 (<strong>*appliance_domain*-CTL01</strong>)，然後開啟 命令提示字元中使用 Windows 系統管理員認證。  
  
2.  瀏覽至下列目錄： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  匯入模組 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要匯入您必須使用兩個句點命令中。  
  
    **範例:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  叫用`Enable-RemoteMonitoring`命令。  
  
    > [!NOTE]  
    > 指令碼會假設的網際網路連線正常運作，且不會驗證網際網路連線。  
  
    1.  第一次啟用遙測，會使用下列命令，以確保所有的 DNS 轉寄站已正確設定。 在此範例中將 DNS 轉送 IP 位址取代`xx.xx.xx.xx`與您的環境中的 DNS 轉寄站 IP 位址。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  當已設定 DNS 轉寄站，例如重新啟用先前停用遙測時，請使用下列命令以啟用遙測，但未設定 DNS 轉送。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  將提示您閱讀並認可 APS 會收集在應用裝置的相關資訊。 將會有 APS 隱私權聲明您可以複製並貼到任何的網際網路瀏覽器檢閱的連結。  
  
6.  請輸入**Y**接受並參加意見反應，或輸入**N**不接受。  
  
7.  如果您輸入**Y**會有一系列的命令會將遙測 （和選擇性 DNS 轉寄站） 可讓您的應用裝置上的功能。 如果您看到任何錯誤或讓您相信命令沒有成功的資訊連絡 CSS 以尋求協助。  
  
如果您輸入**N**會執行任何命令，並且將不會啟用此功能及就沒什麼要執行。  
  
在執行沒有壞處`Enable-RemoteMonitoring`命令多次。 如果已設定 DNS 轉寄站就會指出這種情況的警告訊息。  
  
## <a name="disable"></a>停用遙測  
停用遙測，將會停止所有作業進行通訊來監視在雲端中的服務 AP 設備的狀態資訊。  
  
> [!IMPORTANT]  
> 執行此作業不會停用您的 DNS 轉寄站或可能在設備中的其他功能所使用的網際網路連線。  
  
#### <a name="to-disable-telemetry"></a>若要停用遙測  
  
1.  使用設備的網域系統管理員帳戶，連接到控制節點 (<strong>*appliance_domain*-CTL01</strong>) 和系統管理員權限開啟 PowerShell 視窗。  
  
2.  瀏覽至下列目錄： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  匯入模組 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要匯入您必須使用兩個句點命令中。  
  
    **範例:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  叫用`Disable-RemoteMonitoring`命令不加任何參數。 此命令會停止傳送意見反應。 （這不會影響本機監視。）不過，命令將會不停用 DNS 轉寄站及/或停用任何網際網路連線。 這都必須已成功停用的意見反應之後以手動方式完成。  
  
    **範例:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
如果您看到任何錯誤或讓您相信命令沒有成功的資訊連絡 CSS 以尋求協助。  
  
在執行沒有壞處`Disable-RemoteMonitoring`命令多次。  
  
## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱：
- [使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [使用系統檢視表來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
- [使用 System Center Operations Manager 監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [使用 DNS 轉寄站解析非設備 DNS 名稱&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
