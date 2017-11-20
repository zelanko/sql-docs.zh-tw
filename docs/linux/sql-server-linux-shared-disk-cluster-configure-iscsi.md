---
title: "設定容錯移轉叢集執行個體儲存體 iSCSI SQL Server on Linux |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 18a73a25e8817577930ad058dbad56d56586d417
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>設定容錯移轉叢集執行個體-iSCSI-SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本文說明如何在 Linux 上設定 iSCSI 儲存體容錯移轉叢集執行個體 (FCI)。 

## <a name="configure-iscsi"></a>設定 iSCSI 
iSCSI 用來顯示已知做為目標伺服器的伺服器，從磁碟的網路。 連線到 iSCSI 目標伺服器需要已設定 iSCSI 啟動器。 在目標上的磁碟會獲得明確權限，如此應該要能夠存取它們的起始端可以這樣做。 目標本身應該是高度可用且可靠。

### <a name="important-iscsi-target-information"></a>重要的 iSCSI 目標資訊
雖然本節不將討論如何設定 iSCSI 目標，因為它是針對您要使用的來源類型，請確定已將叢集節點使用的磁碟的安全性。  

如果使用以 Linux 為基礎的 iSCSI 目標的目標應該永遠不會設定在任何 FCI 節點上。 對於效能和可用性，iSCSI 網路應該不同於所使用的來源伺服器與用戶端伺服器上的一般網路流量。 用於 iSCSI 的網路應該是快速。 請記住該網路無法使用某些處理器的頻寬，所以請據此是否使用一般的伺服器。
最重要的是，以確保完成目標上為所建立的磁碟會指派適當的權限，以便參與 FCI 中的伺服器才能存取它們。 下列範例從 Microsoft iSCSI 目標其中 linuxnodes1 是名稱建立，而使它們不會顯示 NewFCIDisk1.vhdx，在此情況下，指派節點的 IP 位址。

![Initiator][1]

### <a name="instructions"></a>Instructions

本節將討論如何將 fci 做為節點的伺服器上設定 iSCSI 啟動器。 指示應該會如 RHEL 和 Ubuntu 上運作。

如需有關支援的發行版本的 iSCSI 啟動器的詳細資訊，請參閱下列連結：
- [Red Hat](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](http://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  選擇其中一個伺服器，為即將加入 FCI 組態中。 不論哪一個。 iSCSI 應該是在專用的網路，因此設定 iSCSI 辨識，並使用該網路。 執行`sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new`其中`<iSCSIIfaceName>`是網路的唯一或好記名稱。 下列範例會使用`iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7 setiscsinetwork][6]
 
2.  編輯`/var/lib/iscsi/ifaces/iSCSIIfaceName`。 請確定它擁有完整填寫下列值：

    - 在作業系統中所見，iface.net_ifacename 是網路卡的名稱。
    - iface.hwaddress 是名稱的唯一，將會建立下列這個介面的 MAC 位址。
    - iface.ipaddress
    - iface.subnet_Mask 

    請參閱下列範例：

    ![iSCSITargetSettings][2]

3.  找到 iSCSI 目標。

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName > 網路的唯一/易記名稱\<TargetIPAddress > 是 iSCSI 目標的 IP 位址和\<TargetPort > 是的 iSCSI 目標的連接埠。 

    ![iSCSITargetResults][3]

 
4.  登入目標

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName > 網路的唯一/易記名稱和\<TargetIPAddress > 是 iSCSI 目標的 IP 位址。

    ![iSCSITargetLogin][4]

5.  請檢查已連線到 iSCSI 目標。

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  檢查 iSCSI 連接的磁碟

    ```bash
    sudo grep “Attached SCSI” /var/log/messages
    ```
    ![30 iSCSIattachedDisks][7]

7.  在 iSCSI 磁碟上建立的實體磁區。

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<devicename > 會將裝置從上一個步驟的名稱。 

 
8.  ISCSI 磁碟上建立磁碟區群組。 指派給單一磁碟區群組的磁碟會被視為在集區或集合。 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName > 磁碟區群組的名稱和\<devicename > 是從步驟 6 裝置的名稱。 
 
9.  建立並確認磁碟的邏輯磁碟區。

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<大小 > 是要建立時，磁碟區的大小，而且可以指定與 G (gb)、 T (tb) 等等，\<LogicalVolumeName > 是邏輯磁碟區的名稱和\<VolumeGroupName > 是從磁碟區群組的名稱上一個步驟。 

    下列範例會建立 25 GB 的磁碟區。
 
    ![Create25GBVol][10]

10. 執行`sudo lvs`若要查看已建立 LVM。
 
11. 支援的檔案系統邏輯磁碟區格式化。 如需 EXT4，使用下列範例：

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName > 是從上一個步驟的磁碟區群組的名稱。 \<LogicalVolumeName > 是從上一個步驟的邏輯磁碟區的名稱。  

12. 系統資料庫或儲存在預設資料位置的任何項目，請遵循下列步驟。 否則，請跳至步驟 13。

   *    請確定 SQL Server 會停止您正在使用的伺服器上。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    參數完全是超級使用者。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```

   *    Mssql 使用者參數。 如果成功，則不會收到任何通知。

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
    
   *    請確認檔案是目錄中。

    ```bash
    ls \<TempDir>
    ```
    \<TempDir > 是從步驟 d 資料夾的名稱。

   *    從現有的 SQL Server 資料目錄刪除檔案。 如果成功，則不會收到任何通知。

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    請確認已刪除的檔案。 下圖顯示從 c 到 h 整個序列的範例。

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45 CopyMove][8]
 
   *    型別`exit`切換回根使用者。

   *    裝載 SQL Server data 資料夾中的 iSCSI 邏輯磁碟區。 如果成功，則不會收到任何通知。

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName > 磁碟區群組的名稱和\<LogicalVolumeName > 是建立邏輯磁碟區的名稱。 下列範例語法符合上面所建立的邏輯磁碟區與磁碟區群組。

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    Mssql 來變更掛接的擁有者。 如果成功，則不會收到任何通知。

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    將裝載群組擁有權變更為 mssql。 如果成功，則不會收到任何通知。

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
 
   *    輸入`exit`不是 mssql。
    
   *    輸入`exit`不是根目錄。

   *    啟動 SQL Server。 如果所有項目已正確複製，並套用安全性是否正確，SQL Server 應該會顯示為已啟動。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    停止 SQL Server 並確認它已關閉。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. 進行的非系統資料庫，例如使用者資料庫或備份，請遵循下列步驟。 如果只使用的預設位置，請跳至步驟 14。

   *    參數是超級使用者。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```

   *    建立將 SQL Server 所使用的資料夾。 

    ```bash
    mkdir <FolderName>
    ```

    \<資料夾名稱 > 資料夾的名稱。 將資料夾的完整路徑必須指定如果不在正確的位置。 下列範例會建立名為 /var/opt/mssql/userdata 的資料夾。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    裝載 iSCSI 邏輯磁碟區在上一個步驟中建立的資料夾中。 如果成功，則不會收到任何通知。
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 磁碟區群組的名稱\<LogicalVolumeName > 所建立的邏輯磁碟區的名稱和\<資料夾名稱 > 資料夾的名稱。 範例語法如下所示。

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    變更至 mssql 建立之資料夾的擁有權。 如果成功，則不會收到任何通知。

    ```bash
    chown mssql <FolderName>
    ```

    \<資料夾名稱 > 是已建立的資料夾名稱。 下列為範例。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    變更的群組建立到 mssql 資料夾。 如果成功，則不會收到任何通知。

    ```bash
    chown mssql <FolderName>
    ```

    \<資料夾名稱 > 是已建立的資料夾名稱。 下列為範例。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    型別`exit`不再超級使用者。

   *    若要測試，請在該資料夾中建立的資料庫。 如下所示的範例會使用 sqlcmd 建立資料庫，切換至該內容，確認檔案存在於作業系統層級，然後再刪除暫存位置。 您可以使用 SSMS。
  
    ![50 ExampleCreateSSMS][9]

   *    取消掛接共用 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 磁碟區群組的名稱\<LogicalVolumeName > 所建立的邏輯磁碟區的名稱和\<資料夾名稱 > 資料夾的名稱。 範例語法如下所示。

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. 該唯一 Pacemaker 可以啟動磁碟區群組，請設定伺服器。

    ```bash
    sudo lvmconf --enable-halvm --services –startstopservices
    ```
 
15. 產生伺服器上的磁碟區群組的清單。 列出的任何不是 iSCSI 磁碟可供系統，例如用於作業系統磁碟。

    ```bash
    sudo vgs
    ```

16. 修改檔案 /etc/lvm/lvm.conf 啟動組態區段。 設定下列行：

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker > 不會使用 fci 的步驟為 20，輸出中的磁碟區群組的清單。 將以引號括住和個別的每個以逗號分隔。 下列為範例。

    ![55 ListOfVGs][11]
 
 
17. Linux 啟動時，它將會掛接檔案系統。 若要確保只有 Pacemaker 可以掛上的 iSCSI 磁碟，重建根檔案系統映像。 

    執行下列命令，這可能需要一些時間才能完成。 如果成功，會回收到任何訊息。

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. 重新啟動伺服器。

19. 在 FCI 中會參與另一部伺服器，執行步驟 1-6。 這將在 iSCSI 目標的 SQL server。 
 
20. 產生伺服器上的磁碟區群組的清單。 它應該會顯示先前建立的磁碟區群組。 

    ```bash
    sudo vgs
    ``` 
23. 啟動 SQL Server 並確認它可以啟動此伺服器上。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. 停止 SQL Server 並確認它已關閉。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. 重複步驟 1 到 6，為即將加入 FCI 中的其他伺服器上。

現在您已經準備好要設定 FCI。

|Distribution |主題 
|----- |-----
|**Red Hat Enterprise Linux HA 的附加元件** |[設定](sql-server-linux-shared-disk-cluster-configure.md)<br/>[操作](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server 高可用性的附加元件** |[設定](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>後續的步驟

[設定容錯移轉叢集執行個體的 SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

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

