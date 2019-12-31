---
title: 使用 DNS 轉寄站
description: 使用 DNS 轉寄站來解析分析平臺系統中的非設備 DNS 名稱。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3d1d0d9428138da615fad7ff5745c758d9fcd3b8
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399437"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>使用 DNS 轉寄站來解析分析平臺系統中的非設備 DNS 名稱
您可以在分析平臺系統應用裝置的 Active Directory Domain Services 節點（**_設備\_網域_-AD01**和**_設備\_網域_-AD02**）上設定 DNS 轉寄站，以允許腳本和軟體應用程式存取外部伺服器。  
  
## <a name="ResolveDNS"></a>使用 DNS 轉寄站  
分析平臺系統裝置已設定為防止解析不在設備中之伺服器的 DNS 名稱。 某些處理常式（例如 Windows Software Update Services （WSUS））需要存取設備外的伺服器。 若要支援此使用案例，可以將分析平臺系統 DNS 設定為支援外部名稱轉寄站，以允許分析平臺系統主機和虛擬機器（Vm）使用外部 DNS 伺服器來解析設備以外的名稱。 不支援 DNS 尾碼的自訂設定，這表示您必須使用完整功能變數名稱來解析非設備伺服器名稱。  
  
**使用 DNS GUI 建立 DNS 轉寄站**  
  
1.  登入 [ **_設備\__] [網域-AD01** ] 節點。  
  
2.  開啟 [DNS 管理員] （**dnsmgmt.msc**）。  
  
3.  以滑鼠右鍵按一下伺服器的名稱，然後按一下 [**屬性**]。  
  
4.  在 [ **Advanced** ] 索引標籤上，取消選取 [**停用遞迴（同時停**用轉寄站）] 選項，**然後按一下 [** 套用]。）  
  
5.  按一下 [**轉寄**站] 索引標籤，然後按一下 [**編輯**]。  
  
6.  輸入將提供名稱解析的外部 DNS 伺服器的 IP 位址。 設備中的 Vm 和伺服器（主機）會使用完整的功能變數名稱連線到外部伺服器。  
  
7.  在**_設備\_網域_-AD02**節點上重複步驟 1-6  
  
**使用 Windows PowerShell 建立 DNS 轉寄站**  
  
1.  登入 [ **_設備\__] [網域-AD01**] 節點。  
  
2.  從 [ **_設備\__] [網域-AD01** ] 節點執行下列 Windows PowerShell 腳本。 執行 Windows PowerShell 腳本之前，請使用非設備 DNS 伺服器的 IP 位址來取代 IP 位址。  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  在**_設備\_網域_-AD02**節點上執行相同的命令。  
  
## <a name="configuring-dns-resolution-for-wsus"></a>設定 WSUS 的 DNS 解析  
SQL Server PDW 2012 提供整合式服務和修補功能。 SQL Server PDW 使用 Microsoft Update 和其他 Microsoft 服務技術。 若要啟用更新，設備必須能夠連線至公司 WSUS 存放庫或 Microsoft 公用 WSUS 存放庫。  
  
對於選擇設定設備以在 Microsoft 公用 WSUS 存放庫上尋找更新的客戶，下列指示會在設備上設定適當的設定詳細資料。  
  
> [!NOTE]  
> 客戶網路系統管理員必須提供可在**Microsoft.com**解析名稱之公司 DNS 伺服器的 IP 位址。  
  
1.  使用 [遠端桌面]，使用網狀架構網域<fabric domain>系統管理員帳戶登入 VMM VM （-vmm）。  
  
2.  開啟 [控制台]，按一下 [**網路和網際網路**]，然後按一下 [**網路和共用中心**]。  
  
3.  在 [連接] 清單中，按一下 [ **VMSEthernet**]，然後按一下 [**屬性**]。  
  
4.  選取 [網際網路通訊協定第 4 版 (TCP/IPv4)] ****，然後按一下 [內容] ****。  
  
5.  在 [**其他 DNS 伺服器**] 方塊中，新增客戶網路系統管理員所提供的 IP 位址。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
