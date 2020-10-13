---
title: 設定 iSCSI FCI 儲存體 - Linux 上的 SQL Server
description: 了解如何使用 Linux 上的 SQL Server iSCSI 來設定容錯移轉叢集執行個體 (FCI)。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 06/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 32ff32e3d342d63e6de7976213bf4a48ec915778
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784912"
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>設定容錯移轉叢集執行個體 - iSCSI - Linux 上的 SQL Server

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

此文章說明如何針對 Linux 上的容錯移轉叢集執行個體 (FCI) 設定 iSCSI 儲存體。 

## <a name="configure-iscsi"></a>設定 iSCSI 
iSCSI 會使用網路將磁碟從一部已知為目標的伺服器呈現給其他伺服器。 連線至 iSCSI 目標的伺服器需要設定 iSCSI 啟動器。 目標上的磁碟會被授與明確的權限，因此應該只有能夠存取它們的啟動器才能這樣做。 目標本身應該是高度可用且可靠的。

### <a name="important-iscsi-target-information"></a>重要的 iSCSI 目標資訊
雖然本節不會介紹如何設定 iSCSI 目標，因為它特定於您將使用的來源類型，但請確定已設定將由叢集節點使用之磁碟的安全性。  

如果使用以 Linux 為基礎的 iSCSI 目標，則絕對不應在任何 FCI 節點上設定目標。 針對效能和可用性，iSCSI 網路應該與來源和用戶端伺服器上一般網路流量所使用的網路不同。 用於 iSCSI 的網路應該要很快。 請記住，網路會耗用一些處理器頻寬，因此如果使用一般伺服器，請據此進行規劃。
確保在目標上完成的最重要事項，是為建立的磁碟指派適當的權限，以便只有參與 FCI 的伺服器才能存取它們。 以下顯示的範例來自 Microsoft iSCSI 目標，其中 linuxnodes1 是建立的名稱，在此情況下，會指派節點的 IP 位址，以便向它們顯示 NewFCIDisk1.vhdx。

![Initiator][1]

### <a name="instructions"></a>Instructions

本節將說明如何在將作為 FCI 節點的伺服器上設定 iSCSI 啟動器。 說明應該同時適用 RHEL 和 Ubuntu。

如需有關支援的 iSCSI 啟動器散發的詳細資訊，請參閱下列連結：
- [Red Hat](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](https://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  選擇將會參與 FCI 設定的其中一部伺服器。 任何一部伺服器都可以。 iSCSI 應該位於專用的網路上，因此請設定 iSCSI 來辨識和使用該網路。 執行 `sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new`，其中 `<iSCSIIfaceName>` 是網路的唯一或易記名稱。 下列範例會使用 `iSCSINIC`：
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  編輯 `/var/lib/iscsi/ifaces/iSCSIIfaceName`。 請確定下列值已完全填寫：

    - iface.net_ifacename 是作業系統中所見的網路卡名稱。
    - iface.hwaddress 是將在下方為此介面建立之唯一名稱的 MAC 位址。
    - iface.ipaddress
    - iface.subnet_Mask 

    請參閱下列範例：

    ![iSCSITargetSettings][2]

3.  尋找 iSCSI 目標。

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName> 是網路的唯一/易記名稱，\<TargetIPAddress> 是 iSCSI 目標的 IP 位址，而 \<TargetPort> 是 iSCSI 目標的連接埠。 

    ![iSCSITargetResults][3]

 
4.  登入目標

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName> 是網路的唯一/易記名稱，而 \<TargetIPAddress> 是 iSCSI 目標的 IP 位址。

    ![iSCSITargetLogin][4]

5.  檢查以查看是否有與 iSCSI 目標的連線。

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  檢查 iSCSI 已連結的磁碟

    ```bash
    sudo grep "Attached SCSI" /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  在 iSCSI 磁碟上建立實體磁碟區。

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<devicename> 是上一個步驟中裝置的名稱。 

 
8.  在 iSCSI 磁碟上建立磁碟區群組。 指派給單一磁碟區群組的磁碟會被視為集區或集合。 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName> 是磁碟區群組的名稱，而 \<devicename> 是步驟 6 中的裝置名稱。 
 
9.  建立並驗證磁碟的邏輯磁碟區。

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<size> 是要建立的磁碟區大小，而且可以指定為 G (GB)、T (TB) 等、\<LogicalVolumeName> 是邏輯磁碟區的名稱，而 \<VolumeGroupName> 是上一個步驟中的磁碟區群組名稱。 

    下列範例會建立 25GB 磁碟區。
 
    ![Create25GBVol][10]

10. 執行 `sudo lvs` 以查看已建立的 LVM。
 
11. 使用支援的檔案系統格式化邏輯磁碟區。 針對 EXT4，請使用下列範例：

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName> 是上一個步驟中的磁碟區群組名稱。 \<LogicalVolumeName> 是上一個步驟中的邏輯磁碟區名稱。  

12. 針對系統資料庫或任何儲存在預設資料位置的內容，請遵循這些步驟。 否則，請跳到步驟 13。

   * 確定您正在處理之伺服器上的 SQL Server 已經停止。

        ```bash
        sudo systemctl stop mssql-server
        sudo systemctl status mssql-server
        ```
    
   * 完全切換成超級使用者。 如果成功，您將不會收到任何通知。

        ```bash
        sudo -i
        ```
    
   * 切換成 mssql 使用者。 如果成功，您將不會收到任何通知。

        ```bash
        su mssql
        ```
    
   * 建立暫存目錄來儲存 SQL Server 資料和記錄檔。 如果成功，您將不會收到任何通知。

        ```bash
        mkdir <TempDir>
        ```
    
        \<TempDir> 是資料夾的名稱。 下列範例會建立名為 /var/opt/mssql/TempDir 的資料夾。

        ```bash
        mkdir /var/opt/mssql/TempDir
        ```
        
   * 將 SQL Server 資料和記錄檔複製到暫存目錄。 如果成功，您將不會收到任何通知。

        ```bash
        cp /var/opt/mssql/data/* <TempDir>
        ```
    
        \<TempDir> 是上一個步驟中的資料夾名稱。
    
   * 確認檔案位於目錄中。

        ```bash
        ls \<TempDir>
        ```
 
        \<TempDir> 是步驟 d 中資料夾的名稱。

   * 將檔案從現有的 SQL Server 資料目錄中刪除。 如果成功，您將不會收到任何通知。

        ```bash
        rm - f /var/opt/mssql/data/*
        ```
    
   * 確認檔案已被刪除。 下圖顯示從 c 到 h 的整個序列的範例。

        ```bash
        ls /var/opt/mssql/data
        ```
    
        ![45-CopyMove][8]

   * 輸入 `exit` 以切換回根使用者。

   * 在 SQL Server 資料資料夾中裝載 iSCSI 邏輯磁碟區。 如果成功，您將不會收到任何通知。

        ```bash
        mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
        ```

        \<VolumeGroupName> 是磁碟區群組的名稱，而 \<LogicalVolumeName> 是所建立之邏輯磁碟區的名稱。 下列範例語法符合上一個命令中的磁碟區群組和邏輯磁碟區。

        ```bash
        mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
        ```

   * 將裝載的擁有者變更為 mssql。 如果成功，您將不會收到任何通知。

        ```bash
        chown mssql /var/opt/mssql/data
        ```

   * 將裝載群組的擁有權變更為 mssql。 如果成功，您將不會收到任何通知。

        ```bash
        chgrp mssql /var/opt/mssql/data
        ```

   * 切換成 mssql 使用者。 如果成功，您將不會收到任何通知。

        ```bash
        su mssql
        ``` 

   * 複製暫存目錄 /var/opt/mssql/data 中的檔案。 如果成功，您將不會收到任何通知。

        ```bash
        cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
        ``` 
    
   * 驗證檔案存在。

        ```bash
        ls /var/opt/mssql/data
        ``` 

   *    輸入 `exit` 以退出 mssql 使用者。

   *    輸入 `exit` 以退出根使用者角色。

   *    啟動 SQL Server。 如果所有內容皆已正確複製，並正確地套用安全性，SQL Server 應該會顯示為已啟動。

        ```bash
        sudo systemctl start mssql-server
        sudo systemctl status mssql-server
        ``` 

   *    停止 SQL Server 並驗證它已關閉。

        ```bash
        sudo systemctl stop mssql-server
        sudo systemctl status mssql-server
        ``` 

13. 針對系統資料庫以外的其他內容 (例如，使用者資料庫或備份)，請遵循這些步驟。 如果僅使用預設位置，請跳到步驟 14。

   *    切換成超級使用者。 如果成功，您將不會收到任何通知。

        ```bash
        sudo -i
        ```

   *    建立 SQL Server 將會使用的資料夾。 

        ```bash
        mkdir <FolderName>
        ```

        \<FolderName> 是資料夾的名稱。 如果資料夾不是位於正確的位置，則必須指定其完整路徑。 下列範例會建立名為 /var/opt/mssql/userdata 的資料夾。

        ```bash
        mkdir /var/opt/mssql/userdata
        ```

   *    將 iSCSI 邏輯磁碟區裝載在上一個步驟中所建立的資料夾中。 如果成功，您將不會收到任何通知。

        ```bash
        mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
        ```

        \<VolumeGroupName> 是磁碟區群組的名稱，\<LogicalVolumeName> 是所建立之邏輯磁碟區的名稱，而 \<FolderName> 是資料夾的名稱。 範例語法如下所示。

        ```bash
        mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
        ```

   *    將建立之資料夾的擁有權變更為 mssql。 如果成功，您將不會收到任何通知。

        ```bash
        chown mssql <FolderName>
        ```

        \<FolderName> 是所建立之資料夾的名稱。 範例如下所示。

        ```bash
        chown mssql /var/opt/mssql/userdata
        ```

   *    將建立的資料夾群組變更為 mssql。 如果成功，您將不會收到任何通知。

        ```bash
        chown mssql <FolderName>
        ```

        \<FolderName> 是所建立之資料夾的名稱。 範例如下所示。

        ```bash
        chown mssql /var/opt/mssql/userdata
        ```

   *    輸入 `exit` 來退出超級使用者。

   *    若要進行測試，請在該資料夾中建立資料庫。 下列所示範例會使用 sqlcmd 來建立資料庫，將內容切換至它，確認檔案存在於 OS 層級，然後刪除暫存位置。 您可以使用 SSMS。
  
        ![50-ExampleCreateSSMS][9]

   *    將共用取消掛接 

        ```bash
        sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
        ```

        \<VolumeGroupName> 是磁碟區群組的名稱，\<LogicalVolumeName> 是所建立之邏輯磁碟區的名稱，而 \<FolderName> 是資料夾的名稱。 範例語法如下所示。

        ```bash
        sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
        ```

14. 設定伺服器，以便只有 Pacemaker 可以啟動磁碟區群組。

    ```bash
    sudo lvmconf --enable-halvm --services -startstopservices
    ```

15. 產生伺服器上的磁碟區群組清單。 系統會使用非 iSCSI 磁碟所列出的任何項目，例如 OS 磁碟。

    ```bash
    sudo vgs
    ```

16. 修改檔案 /etc/lvm/lvm.conf 的啟用設定區段。 設定下行：

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker> 是步驟 20 的輸出中，FCI 將不會使用的磁碟區群組清單。 將每一個放在引號中，並以逗號分隔。 範例如下所示。

    ![55-ListOfVGs][11]

17. 當 Linux 啟動時，它會裝載檔案系統。 為確保只有 Pacemaker 可以裝載 iSCSI 磁碟，請重建根檔案系統映像。 

    執行下列命令，這可能需要幾分鐘的時間才能完成。 如果成功，您將不會收到任何訊息。

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. 重新開機伺服器。

19. 在要參與 FCI 的另一部伺服器上，執行步驟 1 - 6。 這會向 SQL Server 呈現 iSCSI 目標。 
 
20. 產生伺服器上的磁碟區群組清單。 它應該會顯示稍早建立的磁碟區群組。 

    ```bash
    sudo vgs
    ``` 

23. 啟動 SQL Server，並確認它可以在這部伺服器上啟動。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. 停止 SQL Server 並確認它已關閉。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

25. 在將參與 FCI 的任何其他伺服器上重複步驟 1 - 6。

您現在已準備好設定 FCI。

| 散發 | 主題 |
| :----------- | :---- |
| Red Hat Enterprise Linux (包含 HA 附加元件) | [設定](sql-server-linux-shared-disk-cluster-configure.md)<br/>[操作](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md) |
| SUSE Linux Enterprise Server (包含 HA 附加元件) | [設定](sql-server-linux-shared-disk-cluster-sles-configure.md) |

## <a name="next-steps"></a>後續步驟

[設定容錯移轉叢集執行個體 - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/05-initiator.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/10-iscsiTargetSettings.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/15-iSCSITargetResults.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/20-iSCSITargetLogin.png
[5]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/25-iSCSIVerify.png
[6]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/7-setiscsinetwork.png
[7]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/30-iSCSIattachedDisks.png
[8]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/45-CopyMove.png
[9]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/50-ExampleCreateSSMS.png
[10]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/40-Create25GBVol.png
[11]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/55-ListOfVGs.png
