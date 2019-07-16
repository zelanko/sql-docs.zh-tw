---
title: 防毒軟體-Analytics Platform System |Microsoft Docs
description: 如果您的資料中心需要防毒軟體，請使用下列方針 Analytics Platform System 上安裝防毒軟體。 建議您不要安裝防毒軟體，除非它是強制的需求，將資料中心。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1e52841ebe96d8aab84e4d09c91b590e8e4d7e2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961609"
---
# <a name="antivirus-software-for-analytics-platform-system"></a>Analytics Platform System 的防毒軟體
如果您的資料中心需要防毒軟體，請使用下列方針 Analytics Platform System 上安裝防毒軟體。 建議您不要安裝防毒軟體，除非它是強制的需求，將資料中心。  
  
> [!WARNING]  
> 我們強烈建議您個別評估每一部電腦和 Analytics Platform System、 整個安全性風險和您選取適用於每一部電腦的安全性風險層級的工具。 此外，我們建議您導入任何病毒防護專案之前，您會測試整個系統的完整負載來測量在穩定性和效能的任何變更。  
>   
> 病毒防護軟體需要執行某些系統資源。 您必須執行測試之前和之後安裝您的防毒軟體，以判斷是否有任何影響 Analytics Platform System 的效能。  
  
本主題根據中的指導方針[如何選擇要在執行 SQL Server 的電腦上執行的防毒軟體](https://support.microsoft.com/kb/309422)並[KB 文章 961804](https://support.microsoft.com/kb/961804/en-us)。  
  
## <a name="exclusion-list-for-physical-hosts"></a>實體主機的排除清單  
若要在實體主機上安裝防毒軟體，排除下列目錄和程序的清單。 這些不應該掃描的防毒軟體。  
  
**排除這些目錄：**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-虛擬機器設定檔目錄  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual Hard 磁碟虛擬硬碟的預設目錄  
  
-   C:\clusterStorage-虛擬硬碟機的目錄  
  
**排除這些處理程序：**  
  
-   虛擬機器管理 (Vmms.exe)  
  
-   虛擬機器工作流程 (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>虛擬機器 (Vm) 的排除清單  
若要在 Vm 上安裝防毒軟體，排除下列目錄和檔案的清單。 這些不應該掃描的防毒軟體。  
  
**_PDW_region_-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-AD01**並 **_appliance_domain_-ad02 移**  
  
-   無限制  
  
**計算節點 Vm**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-VMM**  
  
-   無限制  
  
**_appliance_domain_-WDS**  
  
-   無限制  
  
**_appliance_domain_-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>另請參閱  
[設備管理工作&#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
