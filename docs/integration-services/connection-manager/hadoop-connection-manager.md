---
title: Hadoop 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4cf042d2ab9c2d3e7c492fa008282cbcbe730f8e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735112"
---
# <a name="hadoop-connection-manager"></a>Hadoop 連接管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Hadoop 連線管理員可以使用您為屬性指定的值，讓 SQL Server Integration Services (SSIS) 套件連線至 Hadoop 叢集。  
  
## <a name="configure-the-hadoop-connection-manager"></a>設定 Hadoop 連接管理員  
  
1.  在 [加入 SSIS 連線管理員]  對話方塊中，選取 [Hadoop]   > [加入]  。 [Hadoop 連線管理員編輯器]  對話方塊隨即開啟。  
  
2.  若要設定相關的 Hadoop 叢集資訊，請選擇左窗格中的 [WebHCat]  或 [WebHDFS]  索引標籤。
  
3.  如果您啟用 [WebHCat]  選項，以在 Hadoop 上叫用 Hive 或 Pig 工作，請執行下列動作： 
  
    1.  對於 [WebHCat 主機]  ，輸入裝載 WebHCat 服務的伺服器。  
  
    2.  對於 [WebHCat 連接埠]  ，輸入 WebHCat 服務的連接埠 (預設為 50111)。  
  
    3.  選取用於存取 WebHCat 服務的 [驗證]  方法。 可用的值為：[基本]  和 [Kerberos]  。  
  
         ![搭配基本驗證的 Hadoop Connection Manager Editor 螢幕擷取畫面](../../integration-services/connection-manager/media/hadoop-cm-basic.png "搭配基本驗證的 Hadoop Connection Manager Editor 螢幕擷取畫面")  
  
         ![搭配 Kerberos 驗證的 Hadoop Connection Manager Editor 螢幕擷取畫面](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "搭配 Kerberos 驗證的 Hadoop Connection Manager Editor 螢幕擷取畫面")  
  
    4.  對於 [WebHCat 使用者]  ，輸入已授權可存取 WebHCat 的 [使用者]  。  
  
    5.  如果您選取 [Kerberos]  驗證，請輸入使用者的 [密碼]  和 [網域]  。  
  
4.  如果您啟用 [WebHDFS]  選項，以從 HDFS 中複製資料或將資料複製至 HDFS，請執行下列動作： 
  
    1.  對於 [WebHDFS 主機]  ，輸入裝載 WebHDFS 服務的伺服器。  
  
    2.  對於 [WebHDFS 連接埠]  ，輸入 WebHDFS 服務的連接埠 (預設為 50070)。  
  
    3.  選取用於存取 WebHDFS 服務的 [驗證]  方法。 可用的值為：[基本]  和 [Kerberos]  。  
  
    4.  對於 [WebHDFS 使用者]  ，輸入已授權可存取 HDFS 的使用者。  
  
    5.  如果您選取 [Kerberos]  驗證，請輸入使用者的 [密碼]  和 [網域]  。  
  
5.  選取 [測試連線]  。 (只會測試您已啟用的連接)。  
  
6.  選取 [確定]  關閉對話方塊。  

## <a name="connect-with-kerberos-authentication"></a>使用 Kerberos 驗證進行連線
有兩個選項可設定內部部署環境，以便讓您使用 Hadoop 連線管理員搭配 Kerberos 驗證。 您可以選擇較適合您情況的選項。
-   選項 1：[將 SSIS 電腦加入 Kerberos 領域](#kerberos-join-realm)
-   選項 2：[啟用 Windows 網域和 Kerberos 領域之間的相互信任](#kerberos-mutual-trust)

### <a name="option-1-join-the-ssis-computer-to-the-kerberos-realm"></a><a name="kerberos-join-realm"></a>選項 1：將 SSIS 電腦加入 Kerberos 領域

#### <a name="requirements"></a>需求：

-   閘道電腦必須加入 Kerberos 領域，且無法加入任何 Windows 網域。

#### <a name="how-to-configure"></a>如何設定：

在 SSIS 電腦上：

1.  執行 **Ksetup** 公用程式來設定 Kerberos 金鑰發佈中心 (KDC) 伺服器和領域。

    電腦必須設定為工作群組成員，因為 Kerberos 領域與 Windows 網域不同。 如下列範例中所示，設定 Kerberos 領域並新增 KDC 伺服器。 視需要使用您的領域來取代 `REALM.COM`。

    ```console
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    ```

    執行這些命令之後，請重新啟動電腦。

2.  使用 **Ksetup** 命令來確認設定。 輸出看起來應如下列範例所示：

    ```console
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
    ```

### <a name="option-2-enable-mutual-trust-between-the-windows-domain-and-the-kerberos-realm"></a><a name="kerberos-mutual-trust"></a>選項 2：啟用 Windows 網域和 Kerberos 領域之間的相互信任

#### <a name="requirements"></a>需求：
-   閘道電腦必須加入 Windows 網域。
-   您需要更新網域控制站設定的權限。

#### <a name="how-to-configure"></a>如何設定：

> [!NOTE]
> 在下列教學課程中，視需要使用您的領域和網域控制站來取代 `REALM.COM` 和 `AD.COM`。

在 KDC 伺服器上：

1.  編輯 **krb5.conf** 檔案中的 KDC 設定。 參考下列設定範本，以允許 KDC 信任 Windows 網域。 根據預設，設定會位於 **/etc/krb5.conf**。

    ```console
    [logging]
    default = FILE:/var/log/krb5libs.log
    kdc = FILE:/var/log/krb5kdc.log
    admin_server = FILE:/var/log/kadmind.log

    [libdefaults]
    default_realm = REALM.COM
    dns_lookup_realm = false
    dns_lookup_kdc = false
    ticket_lifetime = 24h
    renew_lifetime = 7d
    forwardable = true

    [realms]
    REALM.COM = {
        kdc = node.REALM.COM
        admin_server = node.REALM.COM
        }
    AD.COM = {
        kdc = windc.ad.com
        admin_server = windc.ad.com
        }

    [domain_realm]
    .REALM.COM = REALM.COM
    REALM.COM = REALM.COM
    .ad.com = AD.COM
    ad.com = AD.COM

    [capaths]
    AD.COM = {
        REALM.COM = .
        }
    ```

    設定之後，請重新啟動 KDC 服務。

2.  在 KDC 伺服器上準備名為 **krbtgt/REALM.COM\@AD.COM** 的主體。 使用下列命令：

    `Kadmin> addprinc krbtgt/REALM.COM@AD.COM`

3.  在 **hadoop.security.auth_to_local** HDFS 服務設定檔案中，新增 `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`。

在網域控制站上：

1.  執行下列 **Ksetup** 命令來新增領域項目：

    ```console
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

2.  建立 Windows 網域對 Kerberos 領域的信任關係。 在下列範例中，`[password]` 是主體 **krbtgt/REALM.COM\@AD.COM**的密碼。

    `C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /password:[password]`

3.  選取要搭配 Kerberos 使用的加密演算法。

    1. 移至 [伺服器管理員]   > [群組原則管理]   > [網域]  。 從該處移至 [群組原則物件]   > [預設值或作用中網域原則]   > [編輯]  。

    2. 在 [群組原則管理編輯器]  快顯視窗中，移至 [電腦設定]   > [原則]   > [Windows 設定]  。 從該處移至 [安全性設定]   > [本機原則]   > [安全性選項]  。 設定[網路安全性:  設定 Kerberos 允許的加密類型]。

    3. 選取您要用來連線到 KDC 的加密演算法。 通常您可以選取任何選項。

        ![Kerberos 加密類型的螢幕擷取畫面](media/hadoop-connection-manager/config-encryption-types-for-kerberos.png)

    4. 使用 **Ksetup** 命令來指定用於特定領域的加密演算法。

        `C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96`

4.  若要在 Windows 網域中使用 Kerberos 主體，請建立網域帳戶和 Kerberos 主體之間的對應關係。

    1. 移至 [系統管理工具]   > [Active Directory 使用者和電腦]  。

    2. 選取 [檢視]   > [進階功能]  ，以設定進階功能。

    3. 找出您想要建立對應的帳戶，以滑鼠右鍵按一下以檢視 [名稱對應]  ，然後選取 [Kerberos 名稱]  索引標籤。

    4. 加入來自領域的主體。

        ![[安全性識別對應] 對話方塊的螢幕擷取畫面](media/hadoop-connection-manager/map-security-identity.png)

在閘道電腦上：

執行下列 **Ksetup** 命令來新增領域項目。

```console
C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
```

## <a name="see-also"></a>另請參閱  
 [Hadoop Hive 工作](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Hadoop Pig 工作](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Hadoop 檔案系統工作](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
