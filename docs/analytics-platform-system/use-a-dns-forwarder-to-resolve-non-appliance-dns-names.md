---
title: Analytics Platform System 中使用的 DNS 轉送工具 |Microsoft Docs 」
description: 您可以使用 DNS 轉寄站解析非設備 DNS 名稱，Analytics Platform System 中。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6ce978d7b05382b1a02018f3d5022b0f8bfaf585
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509322"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>使用 DNS 轉寄站解析非設備 DNS 名稱在 Analytics Platform System
可以在 Active Directory 網域服務節點上設定 DNS 轉寄站 (**_設備\_網域_-AD01**並**_設備\_網域_-ad02 移**) 的程式的 Analytics Platform System 設備，以允許指令碼和軟體應用程式存取外部伺服器。  
  
## <a name="ResolveDNS"></a>使用 DNS 轉寄站  
Analytics Platform System appliance 會設定為防止解析 DNS 名稱的伺服器不在設備中。 某些處理程序，例如 Windows Software Update Services (WSUS)，將需要存取外部應用裝置的伺服器。 若要支援這個使用案例 Analytics Platform System DNS 可以設定為支援可讓 Analytics Platform System 主機和虛擬機器 (Vm) 使用外部 DNS 伺服器將設備之外的名稱解析的外部名稱轉寄站。 不支援的 DNS 尾碼的自訂組態，這表示您必須使用完整的網域名稱來解析非應用裝置伺服器名稱。  
  
**若要使用 DNS GUI 建立 DNS 轉寄站**  
  
1.  登入**_設備\_網域_-AD01**節點。  
  
2.  開啟 DNS 管理員 (**dnsmgmt.msc**)。  
  
3.  以滑鼠右鍵按一下伺服器名稱，然後按一下**屬性**。  
  
4.  在**進階**索引標籤上，取消選取**停用遞迴 （同時停用轉寄站）** 選項，然後再按一下**套用**。)  
  
5.  按一下 **轉寄站**索引標籤，然後按一下**編輯**。  
  
6.  輸入將提供的名稱解析的外部 DNS 伺服器的 IP 位址。 Vm 和設備中的伺服器 （主機） 會使用完整的網域名稱連線到外部伺服器。  
  
7.  重複步驟 1-6 上**_設備\_網域_-ad02 移**節點  
  
**若要使用 Windows PowerShell 建立 DNS 轉寄站**  
  
1.  登入**_設備\_網域_-AD01**節點。  
  
2.  執行下列 Windows PowerShell 指令碼，從**_設備\_網域_-AD01**節點。 執行 Windows PowerShell 指令碼之前，請與您的非設備 DNS 伺服器的 IP 位址取代 IP 位址。  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  在執行相同的命令**_設備\_網域_-ad02 移**節點。  
  
## <a name="configuring-dns-resolution-for-wsus"></a>設定適用於 WSUS 的 DNS 解析  
SQL Server PDW 2012 提供整合式服務與修補功能。 Microsoft Update 及其他 Microsoft 服務技術，則會使用 SQL Server PDW。 若要啟用更新設備必須能夠連接到公司的 WSUS 儲存機制或 Microsoft 公用 WSUS 存放庫。  
  
下列指示選擇設定設備，以尋找更新的 Microsoft 公用 WSUS 存放庫上的客戶，設備上設定適當的組態詳細資料。  
  
> [!NOTE]  
> 客戶的網路系統管理員必須提供可以解析名稱，在公司 DNS 伺服器的 IP 位址**Microsoft.com**。  
  
1.  使用遠端桌面，登入 VMM VM (<fabric domain>VMM) 網狀架構的網域系統管理員帳戶的使用。  
  
2.  開啟 [控制台]，按一下**網路和網際網路**，然後按一下**網路和共用中心**。  
  
3.  在 [連接] 清單中，按一下**VMSEthernet**，然後按一下**屬性**。  
  
4.  選取  **Internet Protocol Version 4 (TCP/IPv4)**，然後按一下**屬性**。  
  
5.  在 **備用 DNS 伺服器**方塊中，新增客戶網路系統管理員提供的 IP 位址。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
