---
title: 設定容錯移轉叢集執行個體儲存體 iSCSI Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 6876ac9f3aa6641efe4e08e6c434870347315bc6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057336"
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>設定容錯移轉叢集執行個體-iSCSI-Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明如何在 Linux 上設定容錯移轉叢集執行個體 (FCI) 的 iSCSI 存放裝置。 

## <a name="configure-iscsi"></a>設定 iSCSI 
iSCSI 使用網路來呈現從已知做為目標伺服器的伺服器的磁碟。 連線到 iSCSI 目標伺服器需要已設定 iSCSI 啟動器。 在目標上的磁碟可以明確權限，以便能夠存取它們的起始端可以這麼做。 本身的目標應該是高度可用且可靠。

### <a name="important-iscsi-target-information"></a>重要的 iSCSI 目標資訊
雖然本節不會討論如何設定 iSCSI 目標，因為它是專屬於您將使用的來源類型，請確定已將叢集節點所使用的磁碟的安全性。  

如果使用以 Linux 為基礎的 iSCSI 目標目標應該永遠不會設定在任何 FCI 節點上。 基於效能和可用性，iSCSI 網路應不同於所使用的來源伺服器與用戶端伺服器上的一般網路流量。 用於 iSCSI 的網路應快速。 請記住該網路不使用某些處理器的頻寬，因此據此規劃如果使用一般的伺服器。
最重要的是，以確保目標上完成時所建立的磁碟會指派適當的權限，以便只在 FCI 中參與的伺服器才能存取它們。 如下所示的範例，其中 linuxnodes1 是建立，名稱，而使 NewFCIDisk1.vhdx 顯示給他們，在此案例中，指派節點的 IP 位址時，Microsoft iSCSI 目標。

![Initiator][1]

### <a name="instructions"></a>Instructions

本節將討論如何設定伺服器，fci 會做為節點上的 iSCSI 啟動器。 指示應該可以如常 RHEL 和 Ubuntu 上運作。

如需有關支援的散發套件的 iSCSI 啟動器的詳細資訊，請參閱下列連結：
- [Red Hat](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](http://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  您可以選擇其中一個將參與的伺服器 FCI 組態中。 不論哪一個。 iSCSI 應該是在專用的網路，因此設定 iSCSI 辨識並使用該網路。 執行`sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new`其中`<iSCSIIfaceName>`是網路的唯一或易記名稱。 下列範例會使用`iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  編輯`/var/lib/iscsi/ifaces/iSCSIIfaceName`。 請確定它已完全填妥下列值：

    - iface.net_ifacename 是網路卡的名稱，在 OS 中所示。
    - iface.hwaddress 是名稱的唯一，將會建立下列這個介面的 MAC 位址。
    - iface.ipaddress
    - iface.subnet_Mask 

    請參閱下列範例：

    ![iSCSITargetSettings][2]

3.  找到 iSCSI 目標。

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName > 是網路的唯一/易記名稱\<TargetIPAddress > 是 iSCSI 目標的 IP 位址和\<TargetPort > 是的 iSCSI 目標的連接埠。 

    ![iSCSITargetResults][3]

 
4.  登入目標

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName > 是唯一的/易記名稱，網路和\<TargetIPAddress > 是 iSCSI 目標的 IP 位址。

    ![iSCSITargetLogin][4]

5.  請檢查連接到 iSCSI 目標。

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  檢查 iSCSI 連接磁碟

    ```bash
    sudo grep “Attached SCSI” /var/log/messages
    ```
    ![30 iSCSIattachedDisks][7]

7.  建立實體的磁碟區上的 iSCSI 磁碟。

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<devicename > 會將裝置從上一個步驟的名稱。 

 
8.  建立磁碟區群組上的 iSCSI 磁碟。 指派給單一磁碟區群組的磁碟會被視為集區或集合。 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName > 磁碟區群組的名稱和\<devicename > 是來自步驟 6 之裝置的名稱。 
 
9.  建立並驗證磁碟的邏輯磁碟區。

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<大小 > 是要建立時，磁碟區的大小，而且可以指定與 G (gb)、 T (tb) 等\<LogicalVolumeName > 是邏輯磁碟區的名稱和\<VolumeGroupName > 是從磁碟區群組的名稱上一個步驟。 

    下列範例會建立 25 GB 的磁碟區。
 
    ![Create25GBVol][10]

10. 執行`sudo lvs`若要查看已建立 LVM。
 
11. 格式化具有支援的檔案系統的邏輯磁碟區。 針對 EXT4，使用下列的範例：

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName > 是從上一個步驟的磁碟區群組的名稱。 \<LogicalVolumeName > 是上一個步驟的邏輯磁碟區的名稱。  

12. 系統資料庫或儲存在預設資料位置的任何項目，請遵循下列步驟。 否則，請跳至步驟 13。

   *    請確定 SQL Server 已停止您正在使用的伺服器上。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    全面轉換成是超級使用者的參數。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```

   *    要使用 mssql 使用者的參數。 如果成功，則不會收到任何通知。

    ```bash
    su mssql
    ```

   *    建立暫存目錄來儲存 SQL Server 資料和記錄檔。 如果成功，則不會收到任何通知。

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > 資料夾的名稱。 下列範例會建立名為 /var/opt/mssql/TempDir 的資料夾。

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    將 SQL Server 資料和記錄檔複製到暫存目錄。 如果成功，則不會收到任何通知。

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > 是從上一個步驟的資料夾名稱。
    
   *    確認目錄中的檔案。

    ```bash
    ls \<TempDir>
    ```
    \<TempDir > 會從步驟 d 資料夾的名稱。

   *    從現有的 SQL Server 資料目錄中刪除檔案。 如果成功，則不會收到任何通知。

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    請確認已刪除的檔案。 下圖顯示從 c 到 h 整個序列的範例。

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45-CopyMove][8]
 
   *    型別`exit`若要切換回根使用者。

   *    掛接 iSCSI 邏輯磁碟區的 SQL Server data 資料夾中。 如果成功，則不會收到任何通知。

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName > 磁碟區群組的名稱和\<LogicalVolumeName > 是已建立的邏輯磁碟區的名稱。 下列的範例語法會比對前一個命令的邏輯磁碟區與磁碟區群組。

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    將 mssql 掛接的擁有者。 如果成功，則不會收到任何通知。

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    將 mssql 掛上群組的擁有權。 如果成功，則不會收到任何通知。

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    切換至 mssql 使用者。 如果成功，則不會收到任何通知。

    ```bash
    su mssql
    ``` 

   *    從暫存目錄 /var/opt/mssql/data 複製檔案。 如果成功，則不會收到任何通知。

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    請確認檔案有。

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    輸入`exit`無法 mssql。
    
   *    輸入`exit`不是根目錄。

   *    啟動 SQL Server。 如果所有項目已正確地複製和套用的安全性是否正確，SQL Server 應該會顯示為已啟動。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    停止 SQL Server，並確認它已關閉。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. 項目以外的系統資料庫，例如使用者資料庫或備份，請遵循下列步驟。 如果僅使用預設位置，請跳至步驟 14。

   *    切換到是超級使用者。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```

   *    建立將由 SQL Server 的資料夾。 

    ```bash
    mkdir <FolderName>
    ```

    \<資料夾名稱 > 是資料夾的名稱。 資料夾的完整路徑必須指定如果不在正確的位置。 下列範例會建立名為 /var/opt/mssql/userdata 的資料夾。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    掛接 iSCSI 邏輯磁碟區在上一個步驟中建立的資料夾中。 如果成功，則不會收到任何通知。
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 磁碟區群組的名稱\<LogicalVolumeName > 是已建立的邏輯磁碟區的名稱和\<資料夾名稱 > 是資料夾的名稱。 範例語法如下所示。

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    變更以 mssql 所建立之資料夾的擁有權。 如果成功，則不會收到任何通知。

    ```bash
    chown mssql <FolderName>
    ```

    \<資料夾名稱 > 是已建立的資料夾名稱。 下列為範例。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    變更建立 mssql 資料夾的群組。 如果成功，則不會收到任何通知。

    ```bash
    chown mssql <FolderName>
    ```

    \<資料夾名稱 > 是已建立的資料夾名稱。 下列為範例。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    型別`exit`不再是超級使用者。

   *    若要測試，請在該資料夾中建立資料庫。 如下所示的範例會使用 sqlcmd 建立資料庫、 切換到它的內容，請確認檔案存在於 OS 層級，然後刪除 暫存位置。 您可以使用 SSMS。
  
    ![50 ExampleCreateSSMS][9]

   *    取消掛接共用 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 磁碟區群組的名稱\<LogicalVolumeName > 是已建立的邏輯磁碟區的名稱和\<資料夾名稱 > 是資料夾的名稱。 範例語法如下所示。

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. 因此，唯一的 Pacemaker 可以啟用磁碟區群組，請設定伺服器。

    ```bash
    sudo lvmconf --enable-halvm --services –startstopservices
    ```
 
15. 產生伺服器上的磁碟區群組的清單。 列出的任何項目不是 iSCSI 磁碟是由系統，例如針對 OS 磁碟。

    ```bash
    sudo vgs
    ```

16. 修改檔案 /etc/lvm/lvm.conf 啟動組態區段。 設定下面這一行：

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker > 是的輸出中的磁碟區群組，將無法供 FCI 的步驟 20 的清單。 將以引號括住，而且會分開每個以逗號分隔。 下列為範例。

    ![55-ListOfVGs][11]
 
 
17. 當 Linux 啟動時，它將會掛接檔案系統。 若要確保只有 Pacemaker 可以掛接 iSCSI 磁碟，重建根檔案系統映像。 

    執行下列命令，這可能需要一些時間才能完成。 如果成功，您會回到收到任何訊息。

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. 重新啟動伺服器。

19. 在要參與 FCI 的另一部伺服器，執行步驟 1 – 6。 這將會顯示的 iSCSI 目標 SQL server。 
 
20. 產生伺服器上的磁碟區群組的清單。 它應該會顯示先前建立的磁碟區群組。 

    ```bash
    sudo vgs
    ``` 
23. 啟動 SQL Server，並確認它可以啟動此伺服器上。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. 停止 SQL Server，並確認它已關閉。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. 重複步驟 1-6，FCI 會參與的任何其他伺服器上。

您現在已準備好設定 FCI。

|Distribution |主題 
|----- |-----
|**Red Hat Enterprise Linux HA 附加元件** |[設定](sql-server-linux-shared-disk-cluster-configure.md)<br/>[操作](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server HA 附加元件** |[設定](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>後續的步驟

[設定容錯移轉叢集執行個體-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

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
