---
title: "設定分析平台 System (APS) 的 InfiniBand 網路介面卡"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "描述如何 InfiniBand 網路介面卡的伺服器上設定非應用裝置用戶端連接到控制項節點上 SQL Server Parallel Data Warehouse (PDW)。"
ms.date: 01/05/2017
ms.topic: article
ms.assetid: 61f3c51a-4411-4fe8-8b03-c8e1ba279646
caps.latest.revision: 
ms.openlocfilehash: 052dfcb32de7fb84acc0ce97c55775944a1d0dc1
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>設定 Analytics Platform System InfiniBand 網路介面卡
描述如何 InfiniBand 網路介面卡的伺服器上設定非應用裝置用戶端連接到控制項節點上 SQL Server Parallel Data Warehouse (PDW)。 使用下列指示的基本連線和高可用性，以便載入、 備份、 和其他處理程序會自動連線到作用中的 InfiniBand 網路。  
  
## <a name="Basics"></a>Description  
以下指示說明如何尋找，然後設定正確的 InfiniBand IP 位址與子網路遮罩 InfiniBand 連接伺服器上。 它們也會說明如何設定您的伺服器能夠使用 AP 應用裝置 DNS，讓您的連線會解析為作用中的 InfiniBand 網路。  
  
APS 高可用性，具有兩個 InfiniBand 網路，一個使用中，一個被動。 每個 InfiniBand 網路具有不同的 IP 位址的控制節點。 如果作用中的 InfiniBand 網路效能降低，被動的 InfiniBand 網路就會變成作用中的網路。 當發生這種情況的指令碼或程序自動連線至作用中的 InfiniBand 網路而不需要變更指令碼參數。  
  
特別是，在您將本主題內容：  
  
1.  尋找 InfiniBand IP 位址的 APS DNS 伺服器 (appliance_domain AD01 和 appliance_domain *-ad02 移)。 若要這樣做，您將登入 AD01 和 ad02 移伺服器，並為每個 InfiniBand 網路取得 IP 位址。 [AD] 節點的 InfiniBand IP 位址是 DNS IP 位址。  
  
2.  設定每個網路介面卡的 APS InfiniBand 網路上使用可用的 IP 位址。  
  
    1.  如果您有兩個 InfiniBand 網路介面卡，一張介面卡使用設定稱為 TeamIB1，並可用的 IP 位址的其他介面卡都可以呼叫第二個 InfiniBand 網路中的第一個 InfiniBand 網路中可用的 IP 位址TeamIB2。 使用 appliance_domain AD01 TeamIB1 IP 位址，做為慣用的 DNS 伺服器以及 appliance_domain ad02 移 TeamIB1 TeamIB1 網路介面卡的替代 DNS 伺服器的 IP 位址。 使用 appliance_domain AD01 TeamIB2 的慣用的 DNS 伺服器和 appliance_domain ad02 移 TeamIB2 的 IP 位址做為 TeamIB2 網路介面卡的替代 DNS 伺服器的 IP 位址。  
  
    2.  如果您有只有一個 InfiniBand 網路介面卡，您將設定配接器與從 InfiniBand 網路的其中一個可用的 IP 位址。 然後您將使用 appliance_domain AD01 TeamIB1 和 appliance_domain ad02 移 TeamIB1 或是使用 appliance_domain AD01 TeamIB2 和 appliance_domain ad02 移 TeamIB2 兩者位於此介面卡上設定慣用和替代 DNS 伺服器相同的網路設定的配接器做為慣用和替代 DNS 伺服器為分別。  
  
3.  設定要用於 AP DNS 伺服器解析您連線到作用中的 InfiniBand 網路 InfiniBand 網路介面卡。  
  
    1.  若要設定此您將加入設備網域的 DNS 尾碼的 DNS 尾碼清單的開頭，用戶端伺服器上使用的進階的 TCP/IP 設定。 這只需要一個網路介面卡; 上設定設定將套用至這兩個介面卡。  
  
之後設定 InfiniBand 網路介面卡，用戶端程序可以連接到 [控制] 節點的 InfiniBand 網路上使用`PDW_region-SQLCTL01`伺服器的位址。 您的伺服器將會附加分析平台系統的 DNS 尾碼，或您可以輸入完整的位址，也就是`PDW_region-SQLCTL01.appliance_domain.pdw.local`。  
  
例如，如果您的 PDW 區域名稱是 MyPDW 應用裝置名稱是 MyAPS，dwloader 伺服器規格，來載入資料將下列其中一項：  
  
-   `dwloader –S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader –S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>開始之前  
  
### <a name="requirements"></a>需求  
您需要 AP 應用裝置網域帳戶登入到 AD01 節點。 例如，F12345 * \Administrator。  
  
您必須已設定網路介面卡的權限的用戶端伺服器上的 Windows 帳戶。  
  
### <a name="prerequisites"></a>필수 구성 요소  
這些指示假設已 racked 並接上應用裝置 InfiniBand 網路用戶端伺服器。 軌道及纜線連接指示，請參閱[取得和設定載入伺服器](acquire-and-configure-loading-server.md)。  
  
### <a name="general-remarks"></a>一般備註  
藉由使用 SQLCTL01，Analytics Platform System DNS 將您用戶端伺服器連線到的控制節點使用作用中的 InfiniBand 網路。 這只適用於連接;如果 InfiniBand 網路效能降低負載或備份期間，您必須重新啟動程序。  
  
若要符合您商務需求，您也可以在用戶端伺服器加入至您自己的非應用裝置群組或 Windows 網域。  
  
## <a name="Sec1"></a>步驟 1： 取得設備 InfiniBand 網路設定  
*要取得設備 InfiniBand 網路設定*  
  
1.  應用裝置 AD01 節點使用 appliance_domain\Administrator 帳戶來登入。  
  
2.  應用裝置 AD01 在節點上，開啟 控制台選取網路和網際網路、 選取網路和共用中心 *，，然後選取 變更介面卡設定。  
  
3.  在 [網路連線] 視窗中，小組 IB1 上按一下滑鼠右鍵，然後選取屬性。  
  
    ![[管理] 節點的 InfiniBand 連接](media/network-teamib.png "管理節點 InfiniBand 連接")  
  
4.  從 [網際網路通訊協定第 4 版 (TCP/IPv4) 內容] 視窗中，記下的值**IP 位址**和**子網路遮罩**。  IP 位址的 ***appliance_domain *-AD01**節點是分析平台系統的 DNS 伺服器的 IP 位址。  
  
5.  上重複步驟 1-5 上述 TeamIB1 配接器的 ***appliance_domain *-ad02 移**伺服器。  
  
    ![PDW 管理節點 InfiniBand 1 屬性](media/network-ip1-properties.png "PDW 管理節點 InfiniBand 1 屬性")  
  
6.  按一下 [取消] 來關閉視窗。  
  
7.  未使用的 IP 位址在網路上找到 TeamIB1，並將它寫下來。  
  
    若要尋找未使用的 IP 位址，請開啟命令視窗並嘗試 ping 您的應用裝置的位址範圍內的 IP 位址。 在此範例中，TeamIB1 網路的 IP 位址會是 172.16.14.30。 尋找開頭為 172.16.14 未使用的 IP 位址。 例如，從命令列輸入 「 ping 172.16.14.254"。 Ping 要求不成功，IP 位址可用。  
  
8.  TeamIB2 的屬性執行相同的動作。 在 * 網路連線] 視窗中，小組 IB2 上按一下滑鼠右鍵，然後選取 [內容。  
  
9. 從 [網際網路通訊協定第 4 版 (TCP/IPv4) 內容] 視窗中，記下 IP 位址和子網路遮罩的值 TeamIB2 的屬性。  
  
10. 重複步驟 8-9 上述 TeamIB2 配接器 appliance_domain ad02 移伺服器上。  
  
    ![TeamIB2 的](media/network-ip2-properties.png "TeamIB2 的屬性")  
  
11. 尋找未使用的 IP 位址上**TeamIB2**網路，然後將它寫下來。  
  
    若要尋找未使用的 IP 位址，請開啟命令視窗並嘗試 ping 您的應用裝置的位址範圍內的 IP 位址。 在此範例中，TeamIB2 網路的 IP 位址會是 172.16.18.30。 尋找開頭為 172.16.18 未使用的 IP 位址。 例如，從命令列輸入 「 ping 172.16.18.254"。 Ping 要求不成功，IP 位址可用。  
  
## <a name="Sec2"></a>步驟 2： 設定用戶端伺服器上的 InfiniBand 網路介面卡設定  

### <a name="notes"></a>注意  
  
-   這些步驟顯示如何註冊您的伺服器與 AP DNS 伺服器。  
  
-   若要符合您自己的網路需求，您也可以在用戶端伺服器加入至您自己的非應用裝置群組或 Windows 網域。  
  
-   指示逐步執行每個伺服器上設定兩個網路介面卡。  如果您只有一張網路介面卡，請挑選其中一個網路介面卡上設定，然後將第二個 DNS 的 IP 位址新增為替代的 DNS 伺服器的網路。  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>若要設定用戶端伺服器上的 InfiniBand 網路介面卡設定  
  
1.  您載入、 備份或其他用戶端網路上的伺服器應用裝置 InfiniBand Windows 管理員的身分登入。  
  
2.  開啟控制窗格 * 選取 網路和共用中心，然後選取 變更介面卡設定。  
  
### <a name="to-configure-the-first-network-adapter"></a>若要設定的第一個網路介面卡  
  
1.  在 [網路連線] 視窗中，以滑鼠右鍵按一下其中一個無法辨識的網路位置 Mellanox 配接器，然後選取屬性。  
  
    ![選取 InfiniBand 網路](media/network-connections.png "選取 InfiniBand 網路")  
  
2.  在 [屬性] 視窗  
  
    1.  在 [一般] 索引標籤上設定您確認為 TeamIB1 ping 測試中可用的 IP 位址的 IP 位址。 本主題中使用的範例值，您會輸入 172.16.14.254。  
  
    2.  子網路遮罩設為您記下 TeamIB1 的子網路遮罩。  
  
    3.  將慣用 DNS 伺服器設為您稍早記下從 appliance_domain * TeamIB1 的 IP 位址-AD01 節點。  
  
    4.  將替代的 DNS 伺服器設為您稍早記下從 appliance_domain * TeamIB1 的 IP 位址-ad02 移節點。  
  
        ![InfiniBand 1 個網路介面卡內容](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  按一下 [確定] 以套用變更。  
  
### <a name="to-configure-the-second-network-adapter"></a>若要設定的第二個網路介面卡  
  
1.  如果您只有一張網路介面卡，請略過本節。  
  
2.  在 [網路連線] 視窗中，以滑鼠右鍵按一下第二個無法辨識的網路位置 Mellanox 配接器，然後選取屬性。  
  
    ![選取 InfiniBand 網路](media/network-connections.png "選取 InfiniBand 網路")  
  
3.  在 [屬性] 視窗  
  
    1.  在 [一般] 索引標籤上設定您確認為 TeamIB2 的 ping 測試中可用的 IP 位址的 IP 位址。 本主題中使用的範例值，您會輸入 172.16.18.254。  
  
    2.  TeamIB2 的記下子網路遮罩設定的子網路遮罩。  
  
    3.  將慣用 DNS 伺服器設為您稍早記下從 appliance_domain * TeamIB2 的 IP 位址-AD01 節點。  
  
    4.  將其他 DNS 伺服器設為您稍早記下從 appliance_domain * TeamIB2 的 IP 位址-ad02 移節點。  
  
        > [!NOTE]  
        > 如果您只有一個網路介面卡，設定慣用和替代的 DNS 伺服器，分別為慣用和替代 DNS 伺服器使用 AD01 TeamIB1 應用裝置和應用裝置 ad02 移 TeamIB1 或使用設備 AD01 TeamIB2 和應用裝置 ad02 移 TeamIB2 做為慣用和替代 DNS 伺服器視 AD 虛擬機器已容錯移轉。  
  
        ![InfiniBand 1 個網路介面卡內容](media/network-ib1-properties.png "InfiniBand 1 個網路介面卡內容")  
  
    5.  按一下 [確定] 以套用變更。  
  
### <a name="to-configure-the-dns-suffix"></a>若要設定的 DNS 尾碼  
  
1.  在 [網路連線] 視窗中，以滑鼠右鍵按一下其中一個網路位置 Mellanox 配接器，然後選取屬性。  
  
2.  按一下 進階... 按鈕，可選取色彩。  
  
3.  在 進階 TCP/IP 設定 視窗中，如果 附加這些 DNS 尾碼 （依順序） 選項不灰色，核取方塊為 附加這些 DNS 尾碼 （依順序）： 選取應用裝置的網域尾碼，然後按一下 新增... 將應用裝置的網域尾碼 `appliance_domain.local`  
  
4.  如果 附加這些 DNS 尾碼 （依順序）： 選項呈現灰色，您可以將 AP 網域加入此伺服器藉由修改登錄機碼 HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient。  
  
    ![TCP/IP 設定](media/network-tcpip.png "TCP/IP 設定")  
  
5.  更快的位址解析，我們建議將應用裝置的後置詞移至清單頂端。  
  
6.  按一下 [確定]。  
  
7.  現在，您可以連接應用裝置上 Infiniband 網路使用`PDW_region-SQLCTL01.appliance_domain.local`，或只是`appliance_domain-SQLCTL01`。 如果您使用的完整名稱和 DNS 尾碼連接，可能會更快建立連線。  
  
    名為的應用裝置的範例命名 MyAPS 與 MyPDW PDW 區域：  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>另請參閱  
[取得和設定來載入伺服器 ](acquire-and-configure-loading-server.md)  
  
