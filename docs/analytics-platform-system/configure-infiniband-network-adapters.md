---
title: 設定不限
description: 說明如何在非應用裝置用戶端伺服器上設定「未使用的網路介面卡」，以連線至平行處理資料倉儲（PDW）上的控制節點。 請使用這些指示來取得基本連線能力，並提供高可用性，讓載入、備份和其他進程自動連接到作用中的未使用網路。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 583d7617c0620d5d1ec24d60fbf10435a547616d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401296"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>為分析平臺系統設定不適用的網路介面卡
說明如何在非應用裝置用戶端伺服器上設定「未使用的網路介面卡」，以連線至平行處理資料倉儲（PDW）上的控制節點。 請使用這些指示來取得基本連線能力，並提供高可用性，讓載入、備份和其他進程自動連接到作用中的未使用網路。  
  
## <a name="Basics"></a>描述  
這些指示會示範如何在未連線的伺服器上尋找並設定正確的未處理 IP 位址和子網路遮罩。 同時也會說明如何將伺服器設定為使用 AP 應用裝置 DNS，讓您的連線能夠解析成作用中的未執行網路。  
  
為了達到高可用性，AP 有兩個未使用的網路，一個主動和一個被動。 每個未使用的網路都有不同的 IP 位址可用於控制節點。 如果作用中的「未使用」網路中斷，被動式的網路會變成作用中的網路。 當這種情況發生時，腳本或程式會自動連接到使用中的未受影響網路，而不需要變更腳本參數。  
  
具體而言，在本文中您會：  
  
1.  尋找 AP DNS 伺服器（appliance_domain-AD01 和 appliance_domain *-AD02）的未處理 IP 位址。 若要這樣做，您可以登入 AD01 和 AD02 伺服器，並取得每個未處理網路的 IP 位址。 AD 節點上的未處理 IP 位址是 DNS IP 位址。  
  
2.  設定每張網路介面卡，以在 AP 的網路上使用可用的 IP 位址。  
  
    1.  如果您有兩個未使用的網路介面卡，您可以在第一個網路介面卡（稱為 TeamIB1）中設定一個介面卡，並在第二個未使用的網路（稱為 TeamIB2）中，為另一個介面卡提供可用的 IP 位址。 使用 appliance_domain-AD01 TeamIB1 IP 位址做為慣用的 DNS 伺服器，並 appliance_domain-AD02 TeamIB1 IP 位址做為 TeamIB1 網路介面卡的替代 DNS 伺服器。 使用 appliance_domain-AD01 TeamIB2 IP 位址做為慣用的 DNS 伺服器，並 appliance_domain-AD02 TeamIB2 IP 位址做為 TeamIB2 網路介面卡的替代 DNS 伺服器。  
  
    2.  如果您只有一個不受使用的網路介面卡，您可以使用其中一個不受網路的 IP 位址來設定介面卡。 接著，您可以使用 appliance_domain-AD01 TeamIB1 和 appliance_domain-AD02 TeamIB1，或使用 appliance_domain-AD01 TeamIB2 和 appliance_domain-AD02 TeamIB2 （以相同的方式），在此介面卡上設定慣用和替代 DNS 伺服器。[網路] 做為所設定的介面卡，分別作為慣用和替代 DNS 伺服器。  
  
3.  將您的「未使用網路介面卡」設定為使用 AP DNS 伺服器，以將您的連線解析成作用中的未執行網路  
  
    1.  若要進行此設定，您可以使用 [advanced TCP/IP] 設定，將設備網域 DNS 尾碼新增至用戶端伺服器上的 DNS 尾碼清單的開頭。 這只需要在其中一個網路介面卡上設定;此設定適用于這兩個介面卡。  
  
在設定您的網路介面卡之後，用戶端進程可以使用`PDW_region-SQLCTL01`做為伺服器的位址，連線到不會網路上的控制節點。 您的伺服器會附加分析平臺系統 DNS 尾碼，或者您可以輸入完整的位址， `PDW_region-SQLCTL01.appliance_domain.pdw.local`也就是。  
  
例如，如果您的 PDW 區功能變數名稱稱是 MyPDW，而設備名稱是 MyAPS，則用於載入資料的 dwloader 伺服器規格就是下列其中一項：  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>開始之前  
  
### <a name="requirements"></a>需求  
您需要有一個 AP 設備網域帳戶，才能登入 [AD01] 節點。 例如，F12345 * \Administrator。  
  
您在用戶端伺服器上需要有設定網路介面卡許可權的 Windows 帳戶。  
  
### <a name="prerequisites"></a>Prerequisites  
這些指示假設用戶端伺服器已架裝，並纜線到設備的網路。 如需機架和纜線的指示，請參閱[取得和設定載入伺服器](acquire-and-configure-loading-server.md)。  
  
### <a name="general-remarks"></a>一般備註  
藉由使用 SQLCTL01，分析平臺系統 DNS 會使用作用中的未受管理網路，將您的用戶端伺服器連接到控制節點。 這只適用于「連線」;如果未使用的網路在負載或備份期間停止運作，您必須重新開機該進程。  
  
若要符合您自己的商務需求，您也可以將用戶端伺服器加入您自己的非應用裝置工作組或 Windows 網域。  
  
## <a name="Sec1"></a>步驟1：取得設備不會的網路設定  
*取得設備的網路設定*  
  
1.  使用 appliance_domain \Administrator 帳戶來登入應用裝置的 [AD01] 節點。  
  
2.  在 [設備的 AD01] 節點上，開啟 [控制台]，選取 [網路和網際網路]，選取 [網路和共用中心]，然後選取 [變更介面卡設定]。  
  
3.  在 [網路連線] 視窗中，以滑鼠右鍵按一下 [Team IB1]，然後選取 [屬性]。  
  
    ![管理節點上的不會連線數](media/network-teamib.png "管理節點上的不會連線數")  
  
4.  從 [網際網路通訊協定第4版（TCP/IPv4）] 屬性視窗中，記下 [ **IP 位址**] 和 [**子網路遮罩**] 的值。  **_設備\_網域_-AD01**節點的 IP 位址是 ANALYTICS Platform System DNS 伺服器的 ip 位址。  
  
5.  針對**_設備\_網域_-AD02**伺服器上的 TeamIB1 介面卡，重複上述的步驟1-5。  
  
    ![PDW 管理節點不會有1個屬性](media/network-ip1-properties.png "PDW 管理節點不會有1個屬性")  
  
6.  按一下 [取消] 關閉視窗。  
  
7.  在 TeamIB1 網路上尋找未使用的 IP 位址，並將它寫下來。  
  
    若要尋找未使用的 IP 位址，請開啟命令視窗，並嘗試 ping 設備位址範圍內的 IP 位址。 在此範例中，TeamIB1 網路的 IP 位址是172.16.14.30。 尋找以172.16.14 開頭且未使用的 IP 位址。 例如，從命令列輸入 "ping 172.16.14.254"。 如果 ping 要求不成功，則可以使用 IP 位址。  
  
8.  針對 TeamIB2 執行相同的動作。 在 [網路連線] 視窗中，以滑鼠右鍵按一下 [Team IB2]，然後選取 [屬性]。  
  
9. 從 [網際網路通訊協定第4版（TCP/IPv4）] 屬性視窗中，記下 TeamIB2 的 IP 位址和子網路遮罩值。  
  
10. 針對 appliance_domain-AD02 伺服器上的 TeamIB2 介面卡，重複上述的步驟8-9。  
  
    ![TeamIB2 的屬性](media/network-ip2-properties.png "TeamIB2 的屬性")  
  
11. 在**TeamIB2**網路上尋找未使用的 IP 位址，並將它寫下來。  
  
    若要尋找未使用的 IP 位址，請開啟命令視窗，並嘗試 ping 設備位址範圍內的 IP 位址。 在此範例中，TeamIB2 網路的 IP 位址是172.16.18.30。 尋找以172.16.18 開頭且未使用的 IP 位址。 例如，從命令列輸入 "ping 172.16.18.254"。 如果 ping 要求不成功，則可以使用 IP 位址。  
  
## <a name="Sec2"></a>步驟2：在用戶端伺服器上設定未設定的網路介面卡  

### <a name="notes"></a>注意  
  
-   這些步驟說明如何向 AP DNS 伺服器註冊您的伺服器。  
  
-   若要符合您自己的網路需求，您也可以將用戶端伺服器加入您自己的非應用裝置工作組或 Windows 網域。  
  
-   指示逐步說明如何在每部伺服器上設定兩個網路介面卡。  如果您只有一張網路介面卡，請挑選網路介面卡上要設定的其中一個網路，然後將第二個 DNS IP 位址新增為替代 DNS 伺服器。  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>若要在用戶端伺服器上設定「不限網路介面卡」設定  
  
1.  以 Windows 系統管理員身分登入您的載入、備份或應用裝置上的其他用戶端伺服器。  
  
2.  開啟 [控制項] 窗格，選取 [網路和共用中心]，然後選取 [變更介面卡設定]。  
  
### <a name="to-configure-the-first-network-adapter"></a>設定第一張網路介面卡  
  
1.  在 [網路連線] 視窗中，于 Mellanox 介面卡的其中一個無法辨識的網路位置上按一下滑鼠右鍵，然後選取 [屬性]。  
  
    ![選取 InfiniBand 網路](media/network-connections.png "選取 InfiniBand 網路")  
  
2.  在 [屬性視窗  
  
    1.  在 [一般] 索引標籤上，將 IP 位址設定為您在 TeamIB1 的 ping 測試中可免費驗證的 IP 位址。 如需本文中使用的範例值，請輸入172.16.14.254。  
  
    2.  將子網路遮罩設定為您為 TeamIB1 所寫下的子網路遮罩。  
  
    3.  將慣用的 DNS 伺服器設定為您先前從 appliance_domain *-AD01 節點記下的 TeamIB1 IP 位址。  
  
    4.  將替代 DNS 伺服器設定為您先前從 appliance_domain *-AD02 節點記下的 TeamIB1 IP 位址。  
  
        ![未用1網路介面卡屬性](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  按一下 [確定] 以套用變更。  
  
### <a name="to-configure-the-second-network-adapter"></a>設定第二張網路介面卡  
  
1.  如果您只有一張網路介面卡，請略過本節。  
  
2.  在 [網路連線] 視窗中，以滑鼠右鍵按一下 [Mellanox 介面卡的第二個無法辨識的網路位置]，然後選取 [屬性]。  
  
    ![選取 InfiniBand 網路](media/network-connections.png "選取 InfiniBand 網路")  
  
3.  在 [屬性視窗  
  
    1.  在 [一般] 索引標籤上，將 IP 位址設定為您在 TeamIB2 的 ping 測試中可免費驗證的 IP 位址。 如需本文中使用的範例值，請輸入172.16.18.254。  
  
    2.  將子網路遮罩設定為您為 TeamIB2 所寫下的子網路遮罩。  
  
    3.  將慣用的 DNS 伺服器設定為您先前從 appliance_domain *-AD01 節點記下的 TeamIB2 IP 位址。  
  
    4.  將替代 DNS 伺服器設定為您先前從 appliance_domain *-AD02 節點記下的 TeamIB2 IP 位址。  
  
        > [!NOTE]  
        > 如果您只有一張網路介面卡，請使用設備 AD01 TeamIB1 和設備 AD02 TeamIB1 做為慣用和替代 DNS 伺服器，分別設定慣用和替代 DNS 伺服器，或使用設備 AD01 TeamIB2 和應用裝置 AD02 TeamIB2 作為慣用和替代 DNS 伺服器（視 AD 虛擬機器是否已故障切換而定）。  
  
        ![未用1網路介面卡屬性](media/network-ib1-properties.png "未用1網路介面卡屬性")  
  
    5.  按一下 [確定] 以套用變更。  
  
### <a name="to-configure-the-dns-suffix"></a>設定 DNS 尾碼  
  
1.  在 [網路連線] 視窗中，在 [Mellanox 介面卡] 的其中一個網路位置上按一下滑鼠右鍵，然後選取 [屬性]。  
  
2.  按一下 [Advanced ...]button.  
  
3.  在 [Advanced TCP/IP 設定] 視窗中，如果 [附加這些 DNS 尾碼（依順序）] 選項未呈現灰色，請核取 [附加這些 DNS 尾碼（依順序）] 方塊，選取設備網域尾碼，然後按一下 [新增 ...]。設備網域尾碼為`appliance_domain.local`  
  
4.  如果 [附加這些 DNS 尾碼（依順序）：] 選項呈現灰色，您可以藉由修改登錄機碼來將 AP 網域新增到此伺服器，HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows NT\DNSClient。  
  
    ![TCP/IP 設定](media/network-tcpip.png "TCP/IP 設定")  
  
5.  如需更快速的位址解析，建議您將設備尾碼移至清單頂端。  
  
6.  按一下 [確定]。  
  
7.  現在，您可以使用`PDW_region-SQLCTL01.appliance_domain.local`或簡單地`appliance_domain-SQLCTL01`連接到設備的未受網路。 如果您使用完整名稱和 DNS 尾碼進行連線，可能會更快速地建立連接。  
  
    名為 MyAPS 且具有 MyPDW PDW 區域的設備範例：  
  
    -   MyPDW-SQLCTL01. MyAPS. local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>另請參閱  
[取得並設定載入伺服器](acquire-and-configure-loading-server.md)  
  
