---
title: 遙測意見反應
description: 將遙測意見反應傳送給 Microsoft，以供分析平臺系統。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 639eb4e9e5c531e154b9eb7f91165af365bc519f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400366"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>將遙測意見反應傳送給 Microsoft 以分析平臺系統
Analytics Platform System 具有選擇性的遙測功能，可將管理主控台資料傳送給 Microsoft。 
  
> [!NOTE]  
> 在此版本中，Microsoft 不會主動監視遙測資料。 收集的資料僅供分析之用。  
  
## <a name="privacy"></a>隱私權  
為了提供最高隱私權保護，AP 會在不啟用遙測的情況下寄送。 啟用這項功能之前，請先參閱[Microsoft Analytics Platform System 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=400902)。 若要加入宣告，請執行下列所述的 PowerShell 腳本。  
  
## <a name="enable"></a>啟用遙測  
**DNS 轉送：** 將遙測資料傳送至 Microsoft 需要分析平臺系統透過 DNS 轉寄站連接到網際網路。 若要啟用這項功能，您必須啟用所有主機和工作負載 Vm 上的 DNS 轉送。 使用`SetupDnsForwarder`選項`Enable-RemoteMonitoring`來叫用命令，以正確設定 DNS 轉送和啟用遙測。 當 DNS `Enable-RemoteMonitoring`轉送已設定`SetupDnsForwarder` ，而您只想要啟用活動訊號監視時，叫用命令，而不使用選項。  
  
> [!IMPORTANT]  
> 啟用 DNS 轉送會開啟所有主機和工作負載 Vm 的網際網路連線。  
  
#### <a name="to-enable-feedback"></a>若要啟用意見反應  
  
1.  使用設備網域系統管理員帳戶，連接到控制節點（<strong>*appliance_domain*CTL01</strong>），並使用您的 Windows 系統管理員認證開啟命令提示字元。  
  
2.  流覽至下列目錄： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  匯入模組`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要匯入，您必須在命令中使用兩個句點。  
  
    **實例**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  叫用`Enable-RemoteMonitoring`命令。  
  
    > [!NOTE]  
    > 此腳本會假設網際網路連線正常運作，且不會驗證網際網路連線。  
  
    1.  當您第一次啟用遙測時，請使用下列命令，以確保所有 DNS 轉寄站皆已正確設定。 在此範例中，請以您環境`xx.xx.xx.xx`中的 dns 轉寄站 ip 位址來取代 dns 轉送的 ip 位址。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  若已設定 DNS 轉寄站，例如重新啟用先前已停用的遙測，請使用下列命令來啟用遙測，而不需設定 DNS 轉送。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  系統會提示您閱讀並確認 AP 會收集設備的相關資訊。 其中將會有可供您複製並貼到任何網際網路瀏覽器以供審查的 AP 隱私權聲明連結。  
  
6.  輸入**Y**以接受並選擇意見反應，或輸入**N**不接受。  
  
7.  如果您輸入**Y** ，將會有一系列執行的命令，可在您的應用裝置上啟用遙測（以及選擇性的 DNS 轉寄站）功能。 如果您看到任何錯誤或資訊，導致您認為命令不是成功的 contact CSS 來取得協助。  
  
如果您輸入**N**，將不會執行任何命令，也不會啟用此功能，而且不會有任何其他可供您執行的動作。  
  
執行`Enable-RemoteMonitoring`命令多次並不會有任何傷害。 如果已設定 DNS 轉寄站，您會收到一則警告訊息，指出這是案例。  
  
## <a name="disable"></a>停用遙測  
停用遙測將會停止將設備狀態相關資訊傳送至雲端中的「AP 監視」服務的所有作業。  
  
> [!IMPORTANT]  
> 執行此作業並不會停用您的 DNS 轉寄站或網際網路連線，而應用裝置中的其他功能可能正在使用該連接。  
  
#### <a name="to-disable-telemetry"></a>停用遙測  
  
1.  使用設備網域系統管理員帳戶，連接到控制節點（<strong>*appliance_domain*CTL01</strong>），並以系統管理員許可權開啟 PowerShell 視窗。  
  
2.  流覽至下列目錄： `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`。  
  
3.  匯入模組`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 若要匯入，您必須在命令中使用兩個句點。  
  
    **實例**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  叫用`Disable-RemoteMonitoring`不含參數的命令。 此命令將會停止傳送意見反應。 （這不會影響本機監視）。不過，此命令不會停用 DNS 轉寄站，也不會停用任何網際網路連線能力。 這必須在成功停用意見反應之後手動完成。  
  
    **實例**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
如果您看到任何錯誤或資訊，導致您認為命令不是成功的 contact CSS 來取得協助。  
  
執行`Disable-RemoteMonitoring`命令多次並不會有任何傷害。  
  
## <a name="next-steps"></a>接下來的步驟
如需詳細資訊，請參閱：
- [使用管理主控台 &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [使用系統檢視 &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-system-views.md)  
- [使用 System Center Operations Manager &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [使用 DNS 轉寄站來解析 &#40;分析平臺系統的非應用裝置 DNS 名稱&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
