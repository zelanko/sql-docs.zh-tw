---
title: 遙測意見反應
description: 將遙測意見反應傳送給 Microsoft for Analytics Platform System。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 639eb4e9e5c531e154b9eb7f91165af365bc519f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400366"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>將遙測意見反應傳送給 Microsoft for Analytics Platform System
Analytics Platform System 有選擇性的遙測功能，可將系統管理員主控台資料傳送給 Microsoft。 
  
> [!NOTE]  
> 在此版本中，Microsoft 不會主動監視遙測資料。 系統只會收集資料以供分析之用。  
  
## <a name="privacy"></a><a name="privacy"></a>隱私權  
為了提供最大隱私權保護，會在不啟用遙測的情況下寄送 AP。 啟用這項功能之前，請先複習 [Microsoft Analytics Platform System 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=400902)。 若要加入宣告，請執行以下所述的 PowerShell 腳本。  
  
## <a name="enable-telemetry"></a><a name="enable"></a>啟用遙測  
**DNS 轉送：** 將遙測資料傳送至 Microsoft 需要 Analytics Platform System 透過 DNS 轉寄站連接到網際網路。 若要啟用此功能，您必須在所有主機和工作負載 Vm 上啟用 DNS 轉送。 `Enable-RemoteMonitoring`使用 `SetupDnsForwarder` 可正確設定 DNS 轉送和啟用遙測的選項來叫用命令。 `Enable-RemoteMonitoring` `SetupDnsForwarder` 當 DNS 轉送已設定，而且您只想要啟用監視時，請在沒有選項的情況下叫用命令。  
  
> [!IMPORTANT]  
> 啟用 DNS 轉送會開啟所有主機和工作負載 Vm 的網際網路連線。  
  
#### <a name="to-enable-feedback"></a>若要啟用意見反應  
  
1.  使用設備網域系統管理員帳戶，連接到 (<strong> *appliance_domain*CTL01</strong>) 的控制節點，然後使用您的 Windows 系統管理員認證開啟命令提示字元。  
  
2.  流覽至下列目錄： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` 。  
  
3.  匯入模組 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要匯入，您必須在命令中使用兩個句點。  
  
    **範例︰**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  叫用 `Enable-RemoteMonitoring` 命令。  
  
    > [!NOTE]  
    > 腳本會假設網際網路連線正常運作，且不會驗證網際網路連線。  
  
    1.  當您第一次啟用遙測時，請使用下列命令來確保所有 DNS 轉寄站都已正確設定。 在此範例中，請將 DNS 轉送的 IP 位址取代 `xx.xx.xx.xx` 為您環境中的 Dns 轉寄站 ip 位址。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  若已設定 DNS 轉寄站，例如重新啟用先前停用的遙測，請使用下列命令來啟用遙測，而不需要設定 DNS 轉送。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  系統會提示您讀取並確認 AP 會收集設備的相關資訊。 您可以複製並貼到任何網際網路瀏覽器中，以查看 AP 隱私權聲明的連結。  
  
6.  輸入 **Y** 接受並加入宣告意見反應，或輸入 **N** 不接受。  
  
7.  如果您輸入 **Y** ，將會有一系列的命令會執行，以便在您的應用裝置上 (，並選擇性地將 DNS 轉寄站) 功能。 如果您看到任何錯誤或資訊，導致您認為命令不是成功的 contact CSS 來取得協助。  
  
如果您輸入 **N**，將不會執行任何命令，而且也不會啟用此功能，也不會再執行任何動作。  
  
多次執行命令並不會造成損害 `Enable-RemoteMonitoring` 。 如果已設定 DNS 轉寄站，您會收到一則警告訊息，指出這是情況。  
  
## <a name="disable-telemetry"></a><a name="disable"></a>停用遙測  
停用遙測將會停止將設備狀態相關資訊傳達給雲端中的 AP 監視服務的所有作業。  
  
> [!IMPORTANT]  
> 執行這項作業並不會停用您的 DNS 轉寄站或網際網路連線，而設備中的其他功能可能會使用這些連接。  
  
#### <a name="to-disable-telemetry"></a>停用遙測  
  
1.  使用設備網域系統管理員帳戶，連接到 (<strong> *appliance_domain*CTL01</strong>) 的控制項節點，然後以系統管理員許可權開啟 PowerShell 視窗。  
  
2.  流覽至下列目錄： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` 。  
  
3.  匯入模組 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要匯入，您必須在命令中使用兩個句點。  
  
    **範例︰**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  在 `Disable-RemoteMonitoring` 沒有參數的情況下叫用命令。 此命令會停止傳送意見反應。  (此情況並不會影響本機監視 ) 。不過，此命令不會停用 DNS 轉寄站及/或停用任何網際網路連線能力。 這必須在成功停用意見反應之後手動完成。  
  
    **範例︰**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
如果您看到任何錯誤或資訊，導致您認為命令不是成功的 contact CSS 來取得協助。  
  
多次執行命令並不會造成損害 `Disable-RemoteMonitoring` 。  
  
## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱
- [使用管理主控台 &#40;Analytics Platform System&#41;來監視設備 ](monitor-the-appliance-by-using-the-admin-console.md)  
- [使用 System Views &#40;Analytics Platform System&#41;監視設備 ](monitor-the-appliance-by-using-system-views.md)  
- [使用 System Center Operations Manager &#40;Analytics Platform System 監視設備&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [使用 DNS 轉寄站來解析 &#40;Analytics Platform System&#41;的非設備 DNS 名稱 ](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
