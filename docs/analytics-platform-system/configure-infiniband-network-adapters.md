---
title: 設定 InfiniBand-Analytics Platform System |Microsoft Docs
description: 描述如何 InfiniBand 網路介面卡的伺服器上設定非應用裝置用戶端連接到控制節點上 Parallel Data Warehouse (PDW)。 基本連線能力和高可用性，以便載入、 備份及其他處理程序會自動連線到作用中的 InfiniBand 網路，使用下列指示。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0421361cf1718d6ee280269f9da125c148aa3afd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518266"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Analytics Platform System 設定 InfiniBand 網路介面卡
描述如何 InfiniBand 網路介面卡的伺服器上設定非應用裝置用戶端連接到控制節點上 Parallel Data Warehouse (PDW)。 基本連線能力和高可用性，以便載入、 備份及其他處理程序會自動連線到作用中的 InfiniBand 網路，使用下列指示。  
  
## <a name="Basics"></a>描述  
這些指示會說明如何尋找並再設定正確的 InfiniBand IP 位址和子網路遮罩 InfiniBand 連線伺服器上。 它們也會說明如何設定您的伺服器使用 AP 設備 DNS，讓您的連線會解析為作用中的 InfiniBand 網路。  
  
如需高可用性，AP 有兩個 InfiniBand 網路，一個使用中，一個被動。 每個 InfiniBand 網路會有不同的 IP 位址，控制節點。 如果使用中的 InfiniBand 網路故障，被動的 InfiniBand 網路會變成作用中的網路。 發生這種情況的指令碼或處理序會自動連線到作用中的 InfiniBand 網路而不需要變更指令碼參數。  
  
具體來說，在此發行項您：  
  
1.  找不到的 InfiniBand IP 位址的 APS DNS 伺服器 (appliance_domain AD01 和 appliance_domain *-ad02 移)。 若要這樣做您登入的 AD01 和 ad02 移伺服器，並針對每個 InfiniBand 網路取得 IP 位址。 InfiniBand AD 節點上的 DNS IP 位址是。  
  
2.  設定每個網路介面卡，可以使用 AP InfiniBand 網路上的 可用的 IP 位址。  
  
    1.  如果您有兩個 InfiniBand 網路介面卡，您可以設定一張介面卡與第一個 InfiniBand 網路 TeamIB1 和可用的 IP 位址的其他介面卡中稱為稱為 TeamIB2 的第二個 InfiniBand 網路中可用的 IP 位址。 使用 appliance_domain AD01 TeamIB1 IP 位址，做為慣用的 DNS 伺服器並 appliance_domain ad02 移 TeamIB1 TeamIB1 網路介面卡的替代 DNS 伺服器的 IP 位址。 使用 appliance_domain AD01 TeamIB2 IP 位址，做為慣用的 DNS 伺服器並 appliance_domain ad02 移 TeamIB2 TeamIB2 的網路介面卡的替代 DNS 伺服器的 IP 位址。  
  
    2.  如果您有只有一個的 InfiniBand 網路介面卡，您可以設定配接器具有從 InfiniBand 網路的其中一個可用的 IP 位址。 然後此使用 appliance_domain AD01 TeamIB1 和 appliance_domain ad02 移 TeamIB1，或是使用 appliance_domain AD01 TeamIB2 和 appliance_domain ad02 移 TeamIB2 兩者位於相同的介面卡上設定慣用和替代 DNS 伺服器分別網路設定的配接器，當做慣用和替代 DNS 伺服器。  
  
3.  設定 InfiniBand 網路介面卡，用以 AP DNS 伺服器解析您的連線到作用中的 InfiniBand 網路。  
  
    1.  若要進行此設定中，您可以使用的進階的 TCP/IP 設定設備網域的 DNS 尾碼加入您的用戶端伺服器上的 DNS 尾碼清單的開頭。 這只需要上其中一個網路介面卡; 設定此設定會套用至這兩個介面卡。  
  
設定您的 InfiniBand 網路介面卡之後, 用戶端程序可以使用連線到 InfiniBand 網路上的 [控制] 節點`PDW_region-SQLCTL01`伺服器的位址。 您的伺服器會將附加的分析平台系統的 DNS 尾碼，或您可以輸入完整的地址即`PDW_region-SQLCTL01.appliance_domain.pdw.local`。  
  
比方說，如果您的 PDW 區域名稱是 MyPDW，設備名稱 MyAPS dwloader 伺服器規格，來將資料載入是下列其中一項：  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>開始之前  
  
### <a name="requirements"></a>需求  
您需要 AP 設備網域帳戶來登入 AD01 節點。 比方說，F12345 * \Administrator。  
  
您必須在已設定的網路介面卡的權限的用戶端伺服器上的 Windows 帳戶。  
  
### <a name="prerequisites"></a>先決條件  
這些指示假設用戶端伺服器是已經 racked 並連接所有纜線到設備 InfiniBand 網路。 機架和纜線的指示，請參閱[取得並設定載入伺服器](acquire-and-configure-loading-server.md)。  
  
### <a name="general-remarks"></a>一般備註  
藉由使用 SQLCTL01，Analytics Platform System DNS 用戶端伺服器的控制節點會使用連接到作用中的 InfiniBand 網路。 這只適用於取得連線;如果在載入期間當機的 InfiniBand 網路，或備份，您需要重新啟動程序。  
  
若要符合您商務需求，您也可以在用戶端伺服器加入至您自己的非應用裝置群組或 Windows 網域。  
  
## <a name="Sec1"></a>步驟 1:取得設備 InfiniBand 網路設定  
*若要取得設備 InfiniBand 網路設定*  
  
1.  登入設備 AD01 節點使用 appliance_domain\Administrator 帳戶。  
  
2.  設備 AD01 在節點上，開啟 控制台選取網路和網際網路、 選取網路和共用中心 *，，然後選取 變更介面卡設定。  
  
3.  在 [網路連線] 視窗中，以滑鼠右鍵按一下 Team IB1 並選取屬性。  
  
    ![在 [管理] 節點的 InfiniBand 連接](media/network-teamib.png "管理節點 InfiniBand 連接")  
  
4.  從 [Internet Protocol Version 4 (TCP/IPv4) 屬性] 視窗中，記下的值**IP 位址**並**子網路遮罩**。  IP 位址**_設備\_網域_-AD01**節點是分析平台系統的 DNS 伺服器的 IP 位址。  
  
5.  上重複步驟 1-5 上述 TeamIB1 配接器**_設備\_網域_-ad02 移**伺服器。  
  
    ![PDW 管理節點 InfiniBand 1 屬性](media/network-ip1-properties.png "PDW 管理節點 InfiniBand 1 屬性")  
  
6.  按一下 [取消] 關閉視窗。  
  
7.  未使用的 IP 位址在網路上尋找 TeamIB1，並將它寫下來。  
  
    若要尋找未使用的 IP 位址，請開啟命令視窗並嘗試 ping 您的應用裝置的位址範圍內的 IP 位址。 在此範例中，TeamIB1 網路的 IP 位址會是 172.16.14.30。 尋找開頭為 172.16.14 未使用的 IP 位址。 例如，從命令列輸入 「 ping 172.16.14.254"。 如果 ping 要求失敗時，IP 位址使用。  
  
8.  TeamIB2 的屬性執行相同的動作。 在 * 網路連線] 視窗中，小組 IB2 上按一下滑鼠右鍵，然後選取 [內容。  
  
9. 從 [網際網路通訊協定第 4 版 (Tcp/ipv4) 內容] 視窗中，記下 IP 位址和子網路遮罩值 TeamIB2 的屬性。  
  
10. 重複步驟 8 至 9 上述 TeamIB2 配接器 appliance_domain ad02 移伺服器上。  
  
    ![TeamIB2 的屬性](media/network-ip2-properties.png "TeamIB2 的屬性")  
  
11. 上尋找未使用的 IP 位址**TeamIB2**網路，然後將它寫下來。  
  
    若要尋找未使用的 IP 位址，請開啟命令視窗並嘗試 ping 您的應用裝置的位址範圍內的 IP 位址。 在此範例中，TeamIB2 網路的 IP 位址會是 172.16.18.30。 尋找開頭為 172.16.18 未使用的 IP 位址。 例如，從命令列輸入 「 ping 172.16.18.254"。 如果 ping 要求失敗時，IP 位址使用。  
  
## <a name="Sec2"></a>步驟 2:在您的用戶端伺服器上設定的 InfiniBand 網路介面卡設定  

### <a name="notes"></a>注意  
  
-   這些步驟顯示如何使用 AP DNS 伺服器中註冊您的伺服器。  
  
-   為了滿足您自己的網路需求，您也可以用戶端伺服器加入至您自己的非應用裝置群組或 Windows 網域。  
  
-   指示逐步執行每個伺服器上設定兩個網路介面卡。  如果您只有一張網路介面卡，挑選其中一個網路介面卡上設定，然後再新增做為替代的 DNS 伺服器的 次要 DNS IP 位址的網路。  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>若要設定您的用戶端伺服器上的 InfiniBand 網路介面卡設定  
  
1.  登入 Windows 系統管理員身分您載入、 備份或其他的用戶端伺服器應用裝置上 InfiniBand 網路。  
  
2.  開啟控制窗格 * 選取 網路和共用中心，然後選取 變更介面卡設定。  
  
### <a name="to-configure-the-first-network-adapter"></a>若要設定的第一個網路介面卡  
  
1.  在 [網路連線] 視窗中，以滑鼠右鍵按一下其中一個無法辨識的網路位置的 Mellanox 介面卡，然後選取屬性。  
  
    ![選取 InfiniBand 網路](media/network-connections.png "選取 InfiniBand 網路")  
  
2.  在 [屬性] 視窗  
  
    1.  在 [一般] 索引標籤上設定您驗證為 TeamIB1 的 ping 測試中可用的 IP 位址的 IP 位址。 這篇文章中所使用的範例值，您需要輸入 172.16.14.254。  
  
    2.  設定子網路遮罩的 TeamIB1 記下子網路遮罩。  
  
    3.  設定慣用 DNS 伺服器，以您先前記下從 appliance_domain * 的 TeamIB1 的 IP 位址-AD01 節點。  
  
    4.  設定備用 DNS 伺服器，以您先前記下從 appliance_domain * 的 TeamIB1 的 IP 位址-ad02 移節點。  
  
        ![InfiniBand 1 的網路介面卡內容](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  按一下 [確定] 以套用變更。  
  
### <a name="to-configure-the-second-network-adapter"></a>若要設定的第二個網路介面卡  
  
1.  如果您只有一張網路介面卡，請略過本節。  
  
2.  在 [網路連線] 視窗中，以滑鼠右鍵按一下第二個無法辨識的網路位置的 Mellanox 介面卡，然後選取屬性。  
  
    ![選取 InfiniBand 網路](media/network-connections.png "選取 InfiniBand 網路")  
  
3.  在 [屬性] 視窗  
  
    1.  在 [一般] 索引標籤上設定您驗證為 TeamIB2 的 ping 測試中可用的 IP 位址的 IP 位址。 這篇文章中所使用的範例值，您需要輸入 172.16.18.254。  
  
    2.  TeamIB2 的屬性記下子網路遮罩設定的子網路遮罩。  
  
    3.  設定慣用 DNS 伺服器，以您先前記下從 appliance_domain * 的 TeamIB2 的 IP 位址-AD01 節點。  
  
    4.  設定備用 DNS 伺服器，以您先前記下從 appliance_domain * 的 TeamIB2 的 IP 位址-ad02 移節點。  
  
        > [!NOTE]  
        > 如果您只有一個網路介面卡、 設定慣用和替代的 DNS 伺服器，分別為慣用和替代 DNS 伺服器使用的設備 AD01 TeamIB1 」 和 「 設備 ad02 移 TeamIB1 或使用設備 AD01 TeamIB2 和設備 ad02 移 TeamIB2 做為慣用和替代的 DNS 伺服器，視 AD 虛擬機器已容錯移轉。  
  
        ![InfiniBand 1 的網路介面卡內容](media/network-ib1-properties.png "InfiniBand 1 的網路介面卡內容")  
  
    5.  按一下 [確定] 以套用變更。  
  
### <a name="to-configure-the-dns-suffix"></a>若要設定的 DNS 尾碼  
  
1.  在 [網路連線] 視窗中，以滑鼠右鍵按一下其中一個網路位置的 Mellanox 介面卡，然後選取屬性。  
  
2.  按一下進階... 按鈕。  
  
3.  在 進階 TCP/IP 設定 視窗中，如果 附加這些 DNS 尾碼 （依順序） 選項不灰色，核取方塊為 附加這些 DNS 尾碼 （依順序）： 選取設備的網域尾碼，，按一下 新增...設備網域尾碼 `appliance_domain.local`  
  
4.  如果附加這些 DNS 尾碼 （依順序）： 選項呈現灰色，您可以將 APS 網域加入此伺服器藉由修改登錄機碼 HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient。  
  
    ![TCP/IP 設定](media/network-tcpip.png "TCP/IP 設定")  
  
5.  適用於更快速的位址解析，我們建議將設備後置詞移至清單頂端。  
  
6.  按一下 [確定]。  
  
7.  現在，您可以連線到設備的 Infiniband 網路利用`PDW_region-SQLCTL01.appliance_domain.local`，或只是`appliance_domain-SQLCTL01`。 如果您使用的完整名稱和 DNS 尾碼連接，可能會更快建立連線。  
  
    應用裝置的範例命名 MyAPS MyPDW PDW 區域：  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>另請參閱  
[取得並設定載入伺服器 ](acquire-and-configure-loading-server.md)  
  
