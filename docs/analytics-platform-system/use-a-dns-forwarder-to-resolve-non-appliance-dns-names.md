---
title: "使用 DNS 轉寄站 dns 名稱解析非應用裝置 (AP)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 123d8a83-b7fd-4dc9-90d4-fa01af2d629d
caps.latest.revision: "21"
ms.openlocfilehash: 6538ec32f141592b6cf21a325b74f3e451e73092
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names"></a>使用 DNS 轉寄站 dns 名稱解析非應用裝置
可以在 Active Directory 網域服務節點上設定 DNS 轉寄站 (***appliance_domain*-AD01**和 ***appliance_domain*-ad02 移**)若要允許指令碼和存取外部伺服器的軟體應用程式程式 Analytics Platform System 應用裝置。  
  
## <a name="ResolveDNS"></a>使用 DNS 轉寄站  
若要避免解析 DNS 名稱的應用裝置中的伺服器設定 Analytics Platform System 應用裝置。 某些處理程序，例如 Windows 軟體 Update Services (WSUS)，將會需要存取應用裝置以外的伺服器。 若要支援這個使用案例 Analytics Platform System DNS 可以設定為支援 Analytics Platform System 主機和虛擬機器 (Vm) 以使用外部 DNS 伺服器來解析外部應用裝置的名稱，將允許的外部名稱轉寄站。 不支援自訂設定的 DNS 尾碼，這表示您必須使用完整的網域名稱來解析非應用裝置名稱。  
  
**若要建立 DNS 轉寄站 DNS gui**  
  
1.  登入 ***appliance_domain*-AD01**節點。  
  
2.  開啟 DNS 管理員 (**dnsmgmt.msc**)。  
  
3.  以滑鼠右鍵按一下伺服器名稱，然後按一下**屬性**。  
  
4.  在**進階**索引標籤上，取消選取**停用遞迴 （同時停用轉寄站）**選項，然後再按一下**套用**。)  
  
5.  按一下**轉寄站**索引標籤，然後按一下 **編輯**。  
  
6.  輸入將會提供名稱解析的外部 DNS 伺服器的 IP 位址。 Vm 和應用裝置中的伺服器 （主機） 會使用完整的網域名稱來連接到外部伺服器。  
  
7.  重複步驟 1 – 6 上 ***appliance_domain*-ad02 移**節點  
  
**若要利用 Windows PowerShell 中建立 DNS 轉寄站**  
  
1.  登入 ***appliance_domain*-AD01**節點。  
  
2.  執行下列 Windows PowerShell 指令碼從 ***appliance_domain*-AD01**節點。 在執行之前的 Windows PowerShell 指令碼，取代您非應用裝置的 DNS 伺服器的 IP 位址中的 IP 位址。  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  在上執行相同的命令 ***appliance_domain*-ad02 移**節點。  
  
## <a name="configuring-dns-resolution-for-wsus"></a>WSUS 設定的 DNS 解析  
SQL Server PDW 2012 提供整合式服務與修補程式的功能。 SQL Server PDW 使用 Microsoft Update 和其他 Microsoft 服務技術。 若要啟用更新應用裝置必須能夠連接到公司的 WSUS 儲存機制或 Microsoft 公用 WSUS 儲存機制。  
  
選擇要設定應用裝置，以尋找更新 Microsoft 公用 WSUS 儲存機制上的客戶，下列指示會應用裝置上設定適當的設定詳細資料。  
  
> [!NOTE]  
> 客戶的網路系統管理員必須提供可以解析名稱，在公司 DNS 伺服器的 IP 位址**Microsoft.com**。  
  
1.  使用遠端桌面，登入 VMM VM (<fabric domain>VMM) 使用 網狀架構的網域系統管理員帳戶。  
  
2.  開啟 控制台，按一下**網路和網際網路**，然後按一下 **網路和共用中心**。  
  
3.  在 連接 清單中，按一下**VMSEthernet**，然後按一下 **屬性**。  
  
4.  選取**網際網路通訊協定第 4 版 (TCP/IPv4)**，然後按一下 **屬性**。  
  
5.  在**備用 DNS 伺服器**方塊中，加入客戶網路系統管理員提供的 IP 位址。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
