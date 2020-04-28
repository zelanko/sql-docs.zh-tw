---
title: 防毒軟體
description: 如果您的資料中心需要防毒軟體，請使用下列指導方針，在分析平臺系統（AP）上安裝防毒軟體。 我們建議您不要安裝防毒軟體，除非這是您的資料中心的公司需求。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c3687b839e52e64350591402c3aa19e9c2c54ac7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401476"
---
# <a name="antivirus-software-for-analytics-platform-system-aps"></a>分析平臺系統（AP）的防毒軟體
如果您的資料中心需要防毒軟體，請使用下列指導方針，在分析平臺系統上安裝防毒軟體。 我們建議您不要安裝防毒軟體，除非這是您的資料中心的公司需求。  
  
> [!WARNING]  
> 強烈建議您個別評估每部電腦和分析平臺系統的安全性風險，並選取適用于每部電腦的安全性風險層級的工具。 此外，建議您在推出任何防毒保護專案之前，先在完整的負載下測試整個系統，以測量穩定性和效能方面的任何變更。  
>   
> 病毒防護軟體需要一些系統資源才能執行。 您必須在安裝防毒軟體之前和之後執行測試，以判斷分析平臺系統上是否有任何效能影響。  
  
本主題是以[如何選擇防毒軟體在執行 SQL Server](https://support.microsoft.com/kb/309422)和[知識庫文章 961804](https://support.microsoft.com/kb/961804/en-us)的電腦上執行的指引為基礎。  
  
## <a name="exclusion-list-for-physical-hosts"></a>實體主機的排除清單  
若要在實體主機上安裝防毒軟體，請排除下列目錄和進程清單。 防毒軟體不應掃描這些應用程式。  
  
**排除這些目錄：**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-虛擬機器設定目錄  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual 硬碟-預設虛擬硬碟目錄  
  
-   C:\clusterStorage-虛擬硬碟目錄  
  
**排除這些進程：**  
  
-   虛擬機器管理（Vmms）  
  
-   虛擬機器工作進程（Vmwp .exe）  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>虛擬機器（Vm）的排除清單  
若要在 Vm 上安裝防毒軟體，請排除下列目錄和檔案清單。 防毒軟體不應掃描這些應用程式。  
  
**_PDW_region_-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-AD01**和** _appliance_domain_-AD02**  
  
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
[&#40;分析平臺系統&#41;的裝置管理工作](appliance-management-tasks.md)  
  
