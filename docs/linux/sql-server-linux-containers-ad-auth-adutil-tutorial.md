---
title: 使用 adutil 為 Linux 上的 SQL Server 容器設定 Active Directory 驗證
description: 逐步教學：使用 adutil 為 Linux 上的 SQL Server 容器設定 Active Directory 驗證
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.date: 12/10/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 318fb046adc25cc2ff485b14974bb756e586162b
ms.sourcegitcommit: 18e2f0706e03d0b2b6324845244fbafaa077a8dd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2020
ms.locfileid: "97103278"
---
# <a name="tutorial-configure-active-directory-authentication-with-sql-server-on-linux--containers"></a>教學課程：為 Linux 上的 SQL Server 容器設定 Active Directory 驗證

> [!NOTE]
> **adutil** 目前為 **公開預覽** 狀態

本教學課程說明如何設定 Linux 上的 SQL Server 容器，以支援 Active Directory (AD) 驗證 (也稱為整合式驗證)。 如需概觀，請參閱[適用於 Linux 上 SQL Server 的 Active Directory 驗證](sql-server-linux-active-directory-auth-overview.md)。

本教學課程包含下列工作：

> [!div class="checklist"]
> - 安裝 adutil-preview
> - 將 Linux 主機加入 AD 網域
> - 為 SQL Server 建立 AD 使用者，並使用 adutil 工具以設定 ServicePrincipalName (SPN)
> - 建立 SQL Server 服務金鑰表檔案
> - 建立 SQL Server 容器所要使用的 mssql.conf 和 krb5.conf 檔案
> - 掛接組態檔並部署 SQL Server 容器
> - 使用 Transact-SQL 建立以 AD 為基礎的 SQL Server 登入
> - 使用 AD 驗證連線到 SQL Server

## <a name="prerequisites"></a>Prerequisites

設定 AD 驗證之前，您必須具備下列條件：

- 在您的網路中擁有 AD 網域控制站 (Windows)。
- 在已加入網域的 Linux 主機電腦上安裝 adutil-preview 工具。 根據您要執行以安裝 adutil-preview 工具的 Linux 發行版本，遵循以下[安裝 adutil-preview](#install-adutil-preview) 一節。

## <a name="container-deployment-and-preparation"></a>容器部署和準備

若要設定容器，您必須事先知道主機上的容器將要使用的連接埠。 預設連接埠 1433 可能會以不同的方式對應到您的容器主機。 在本教學課程中，主機上的連接埠 5433 將會對應到容器的連接埠 1433。 如需詳細資訊，請參閱[使用 Docker 執行 SQL Server 容器映像](quickstart-install-connect-docker.md)快速入門。

註冊服務主體名稱 (SPN) 時，您可以使用機器的主機名稱或容器的名稱，但應該根據您想要在外部連線至容器時所看到的內容進行設定。

請確定已在 Active Directory 中針對 Linux 主機 IP 位址新增轉送主機 (A) 項目，且對應至 SQL Server 容器的名稱。 在本教學課程中，`myubuntu` 主機電腦的 IP 位址是 `10.0.0.10`，而我的 SQL Server 容器名稱則是 `sql1`。 我們會在 Active Directory 中新增轉送主機項目，如下所示。 此項目可確保當使用者連線至 sql1.contoso.com 時，能夠連接到正確的主機。

:::image type="content" source="media/sql-server-linux-containers-ad-auth-adutil-tutorial/host-a-record.png" alt-text="新增主機記錄":::

在本教學課程中，我們會在 Azure 中使用具有三部 VM 的環境。 其中一部 VM 作為 Windows 網域控制站 (DC)，其網域名稱為 `contoso.com`。 此網域控制站的名稱為 `adVM.contoso.com`。 第二部機器是名為 `winbox` 的 Windows 機器，執行 Windows 10 Desktop，其作為用戶端機上盒，並已安裝 SQL Server Management Studio (SSMS)。 第三部機器是名為 `myubuntu` 的 Ubuntu 18.04 LTS 機器，其裝載了 SQL Server 容器。 所有機器都已加入 `contoso.com` 網域。 如需詳細資訊，請參閱[將 Linux 主機上的 SQL Server 加入 Active Directory 網域](sql-server-linux-active-directory-join-domain.md)。

> [!NOTE]
> 如您在本文稍後所見，將主機容器機器加入網域並非必要。

## <a name="install-adutil-preview"></a>安裝 adutil-preview

在 Linux 主機電腦上，使用下列命令以根據 Linux 發行版本安裝 adutil-preview。

> [!NOTE]
> 在此預覽版本中，我們知道對於某些 Linux 發行版本，如果嘗試安裝 adutil 時沒有 `ACCEPT_EULA` 參數，則無法順利安裝。 我們建議使用 `ACCEPT_EULA=Y` 設定以安裝 adutil-preview 工具。 您可以在安裝前，先閱讀預覽 [EULA](https://go.microsoft.com/fwlink/?linkid=2151376)。 我們正積極處理這個問題，此問題應會在 GA 版本中完成修正。

### <a name="rhel"></a>RHEL

1. 下載 Microsoft Red Hat 存放庫組態檔。

    ```bash
    sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/8/prod.repo
    ```

1. 如果您已安裝舊版的 adutil，請移除所有舊版的 adutil 套件。

    ```bash
    sudo yum remove adutil
    ```

1. 執行下列命令以安裝 adutil-preview。 `ACCEPT_EULA=Y` 會接受 adutil 的預覽 EULA。 EULA 則位於路徑 `/usr/share/adutil/`。

    ```bash
    sudo ACCEPT_EULA=Y yum install -y adutil-preview
    ```

### <a name="ubuntu"></a>Ubuntu

1. 註冊 Microsoft Ubuntu 存放庫。

    ```bash
    sudo curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
    ```

1. 如果您已安裝舊版的 adutil，請使用下列命令移除所有舊版的 adutil 套件

    ```bash
    sudo apt-get remove adutil
    ```

1. 執行下列命令以安裝 adutil-preview。 `ACCEPT_EULA=Y` 會接受 adutil 的預覽 EULA。 EULA 則位於路徑 `/usr/share/adutil/`。

    ```bash
    sudo ACCEPT_EULA=Y apt-get install -y adutil-preview
    ```

### <a name="sles"></a>SLES

1. 將 Microsoft SQL Server 存放庫新增至 Zypper。

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
    ```

1. 如果您已安裝舊版的 adutil，請移除所有舊版的 adutil 套件。

    ```bash
    sudo zypper remove adutil
    ```

1. 執行下列命令以安裝 adutil-preview。 `ACCEPT_EULA=Y` 會接受 adutil 的預覽 EULA。 EULA 則位於路徑 `/usr/share/adutil/`。

    ```bash
    sudo ACCEPT_EULA=Y zypper install -y adutil-preview
    ```

## <a name="creating-the-ad-user-spns-and-sql-server-service-keytab"></a>建立 AD 使用者、SPN 與 SQL Server 服務金鑰表

如果您不想讓 Linux 上的 SQL Server 容器主機成為網域的一部分，而且尚未遵循將機器加入網域的步驟，請在已屬於 AD 網域的另一個 Linux 電腦上，遵循下列步驟：

 1. 為 SQL Server 建立 AD 使用者，並使用 adutil 工具以設定 SPN。

 2. 建立並設定 SQL Server 服務金鑰表檔案。

將建立的 mssql.keytab 檔案複製到將執行 SQL Server 容器的主機電腦，並將容器設定為使用複製的 mssql.keytab。 (選擇性) 您也可以將執行 SQL Server 容器的 Linux 主機加入 AD 網域，並在同一部機器上遵循下列步驟。

### <a name="create-an-ad-user-for-sql-server-and-set-the-serviceprincipalname-using-the-adutil-tool"></a>為 SQL Server 建立 AD 使用者，並使用 adutil 工具以設定 ServicePrincipalName

若要在 Linux 的 SQL Server 容器上啟用 AD 驗證，您必須在屬於 AD 網域的 Linux 機器上執行以下所述的步驟 1-3。

1. 使用 `kinit` 命令取得或更新 Kerberos TGT (票證授權票證)。 針對 `kinit` 命令使用具特殊權限的帳戶。 此帳戶必須具有連線到網域的權限，而且必須能夠在網域中建立帳戶和 SPN。

    > [!IMPORTANT]
    > 執行此命令之前，主機應該已經加入網域，如上一個步驟所示。

    ```bash
    kinit privilegeduser@DOMAIN.COM
    ```

    範例：針對上述環境，我的具特殊權限帳戶為 `amvin@CONTOSO.COM`

    ```bash
    kinit amvin@CONTOSO.COM
    ```

2. 使用 adutil 工具，透過 SQL Server 建立將作為具特殊權限 AD 帳戶的新使用者。

   ```bash
   adutil user create --name sqluser -distname CN=sqluser,CN=Users,DC=CONTOSO,DC=COM --password 'P@ssw0rd'
   ```

    > [!NOTE]
    > 您可以使用下列三種方式中的任意一種，以指定密碼：
    >
    > - 密碼旗標：--password \<password\>
    > - 環境變數 - `ADUTIL_ACCOUNT_PWD`
    > - 互動式輸入
    >
    > 密碼輸入方法的優先順序會遵循上方所列的選項順序。 建議您使用環境變數或互動式輸入提供密碼，因為這兩者相較於密碼旗標要更為安全。

    您可以使用如上所示的辨別名稱 (`-distname`) 以指定帳戶的名稱，也可以使用組織單位 (OU) 名稱。 若您同時指定了這兩種名稱，則 OU 名稱 (`--ou`) 會優先於辨別名稱。 您可以執行下列命令以取得更多詳細資料：

    ```bash
    adutil user create --help
    ```

3. 向上方建立的使用者註冊 SPN。 您可以視需要使用主機名稱 (而不是容器名稱)，這取決於您希望連線在外部的顯示方式。 在本教學課程中，會使用連接埠 5433，而不是 1433。 這是容器的連接埠對應。 但您的連接埠號碼可能有所不同。

    ```bash
    adutil spn addauto -n sqluser -s MSSQLSvc -H sql1.contoso.com -p 5433
    ```

    > [!NOTE]
    >
    > - `addauto` 會自動建立 SPN，但前提是 kinit 帳戶有足夠的權限。
    > - `-n`：要指派給 SPN 的帳戶名稱。
    > - `-s`：要用於產生 SPN 的服務名稱。 因為此為 SQL Server 服務相關案例，所以服務名稱為 MSSQLSvc。
    > - `-H`：要用於產生 SPN 的主機名稱。 如果未指定，則會使用本機主機的 FQDN。 請一併提供容器名稱的 FQDN。 在本案例中，主機名稱為 `sql1`，FQDN 為 `sql1.contoso.com`。
    > - `-p`：要用於產生 SPN 的連接埠。 如果未指定，則會在不使用連接埠的情況下產生 SPN。 只有當 SQL Server 接聽預設連接埠 1433 時，本案例中的 SQL 連線才會正常運作。

### <a name="create-the-sql-server-service-keytab-file"></a>建立 SQL Server 服務金鑰表檔案

建立金鑰表檔案，在該檔案中，先前所建立的 4 個 SPN 皆各有一個項目，而使用者也擁有一個項目。 金鑰表檔案將會掛接至容器，因此可以在主機的任何位置上建立該檔案。 您可以安全地變更此路徑，只要在使用 docker/podman 部署容器時，產生的金鑰表正確地掛接即可。

若要為所有 SPN 建立金鑰表，我們可以使用 `createauto` 選項：

```bash
adutil keytab createauto -k /container/sql1/secrets/mssql.keytab -p 5433 -H sql1.contoso.com --password 'P@ssw0rd' -s MSSQLSvc
```

> [!NOTE]
>
> - `-k`：要建立 `mssql.keytab` 檔案的路徑。 在上述範例中，目錄 "/container/sql1/secrets” 應該已經存在於主機上。
> - `-p`：要用於產生 SPN 的連接埠。 如果未指定，則會在不使用連接埠的情況下產生 SPN。
> - `-H`：要用於產生 SPN 的主機名稱。 如果未指定，則會使用本機主機的 FQDN。 請一併提供容器名稱的 FQDN。 在本案例中，主機名稱為 `sql1`，FQDN 為 `sql1.contoso.com`。
> - `-s`：要用於產生 SPN 的服務名稱。 因為此為 SQL Server 服務相關案例，所以服務名稱為 MSSQLSvc。
> - `--password`：這是稍早所建立具特殊權限 AD 使用者帳戶的密碼。
> - `-e` 或 `--enctype`：金鑰表項目的加密類型。 使用以逗號分隔的值清單。 如果未指定，則會顯示互動式提示。

當提供加密類型的選項時，您可以選擇一個以上的加密類型。 在此範例中，我們會選擇 `aes256-cts-hmac-sha1-96` 與 `arcfour-hmac`。 請確定您選擇的加密類型受到主機與網域支援。

如果您想要以非互動方式選擇加密類型，可以在上述命令中，使用 -e 引數以指定您選擇的加密類型。 如需 adutil 命令的其他說明，請執行下列命令。

```bash
adutil keytab createauto --help
```

> [!NOTE]
> `arcfour-hmac` 是弱式加密，此加密類型不建議在實際執行環境中使用。

若要為使用者建立金鑰表，命令為：

```bash
adutil keytab create -k /container/sql1/secrets/mssql.keytab -p sqluser --password 'P@ssw0rd!'
```

> [!NOTE]
>
> - `-k`：要建立 `mssql.keytab` 檔案的路徑。 在上述範例中，目錄 "/container/sql1/secrets” 應該已經存在於主機上。
> - `-p`：要新增至金鑰表的主體。

adutil 金鑰表建立/自動建立不會覆寫先前的檔案，只會附加至檔案 (如果檔案已經存在)。

請確定在部署容器時，所建立的金鑰表具有正確的權限集。

```bash
chmod 440 /container/sql1/secrets/mssql.keytab
```

> [!NOTE]
> 此時，您可以將 mssql.keytab 從目前的 Linux 主機複製到您要部署 SQL Server 容器的 Linux 主機，並在將執行 SQL Server 容器的 Linux 主機上遵循其餘步驟。 如果上述步驟是在將部署 SQL 容器的相同 Linux 主機上執行，則請在相同的主機上，同時遵循後續步驟。

## <a name="create-the-config-files-to-be-used-by-the-sql-server-container"></a>建立 SQL Server 容器所要使用的組態檔

1. 建立包含 AD 設定的 `mssql.conf` 檔案。 這個檔案可以在主機上的任何位置建立，而且必須在 docker run 命令期間正確地掛接。 在此範例中，我們將這個 `mssql.conf` 檔案放在容器目錄 `/container/sql1 ` 下。 `mssql.conf` 的內容如下所示：

    ```output
    [network]
    privilegedadaccount = sqluser
    kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
    ```

    > [!NOTE]
    >
    > - `privilagedadaccount`：要用於 AD 驗證的特殊權限 AD 使用者。
    > - `kerberoskeytabfile`：容器中 mssql.keytab 檔案所在的路徑。

1. 建立 krb5.conf 檔案。 此範例如下所示。 這些檔案的大小寫很重要。

    ```output
    [libdefaults]
    default_realm = DOMAIN.COM

    [realms]
     CONTOSO.COM = {
         kdc = adVM.contoso.com
         admin_server = adVM.contoso.com
         default_domain = CONTOSO.COM
     }

    [domain_realm]
     .contoso.com = CONTOSO.COM
     contoso.com = CONTOSO.COM


1. Copy all files, `mssql.conf`, `krb5.conf`, `mssql.keytab` to a location that will be mounted to the SQL Server container. In this example, these files are placed on the host at the following locations: `mssql.conf` and `krb5.conf` at `/container/sql1/`. `mssql.keytab` is placed at the location `/container/sql1/secrets/`.

1. Make sure there's enough permission on these folders for the user running the docker/podman command. When the container starts, the user needs access to the folder path created. In this example, we provided the below permissions given to the folder path:

    ```bash
    sudo chmod 755 /container/sql1/
    ```

## <a name="mount-the-config-files-and-deploy-the-sql-server-container"></a>掛接組態檔並部署 SQL Server 容器

執行您的 SQL Server 容器，並掛接先前建立的正確 AD 組態檔，如下所示：

```bash
sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=\<YourStrong@Passw0rd\>" \
-p 5433:1433 --name sql1 \
-v /container/sql1:/var/opt/mssql \
-v /container/sql1/krb5.conf:/etc/krb5.conf \
-d mcr.microsoft.com/mssql/server:2019-latest
```

> [!NOTE]
> 在 SELinux 啟用主機之類的 LSM (Linux 安全性模組) 上執行容器時，您必須使用 `Z` 選項以掛接磁碟區，這會指示 Docker 以私人未共用標籤標示內容。 如需詳細資訊，請參閱 [configure the SE Linux label](https://docs.docker.com/storage/bind-mounts/#configure-the-selinux-label) (設定 SE Linux 標籤)。

我們的範例會包含下列命令：

```bash
sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=P@ssw0rd" -p 5433:1433 --name sql1 \
-v /container/sql1:/var/opt/mssql/ \
-v /container/sql1/krb5.conf:/etc/krb5.conf \
--dns-search contoso.com \
--dns 10.0.0.4 \
--add-host adVM.contoso.com:10.0.0.4 \
--add-host contoso.com:10.0.0.4 \
--add-host contoso:10.0.0.4 \
-d mcr.microsoft.com/mssql/server:2019-latest
```

> [!NOTE]
>
> - `mssql.conf` 和 `krb5.conf` 檔案位於主機檔案路徑 `/container/sql1` 中。
> - 建立的 `mssql.keytab` 則位於主機檔案路徑 `/container/sql1/secrets`。
> - 因為我們的主機電腦是在 Azure 上，所以必須將相同順序的 AD 詳細資料附加至 docker run 命令。 在我們的範例中，網域控制站 `adVM` 位於網域 `contoso.com` 中，IP 位址是 `10.0.0.4`。 網域控制站會執行 DNS 和 KDC。

## <a name="create-ad-based-sql-server-logins-in-transact-sql"></a>使用 Transact-SQL 建立以 AD 為基礎的 SQL Server 登入

連線到 SQL 容器並執行下列命令建立登入，並確認登入已確實列出。 您可以從執行 SSMS、Azure Data Studio (ADS) 或任何其他命令列介面 (CLI) 工具的用戶端機器 (Windows 或 Linux) 執行此命令。

```sql
create login [contoso\amvin] From Windows
SELECT name FROM sys.server_principals;
```

## <a name="connect-to-sql-server-using-ad-authentication"></a>使用 AD 驗證連線到 SQL Server。

若要使用 [SSMS](../ssms/download-sql-server-management-studio-ssms.md) 或 [ADS](../azure-data-studio/download-azure-data-studio.md) 進行連線，請使用 SQL Server 名稱和連接埠號碼 (名稱可以是容器名稱或主機名稱) 以 Windows 認證登入 SQL Server。 在我們的範例中，伺服器名稱會是 `sql1.contoso.com, 5433`。

您也可以使用 [sqlcmd](../tools/sqlcmd-utility.md) 之類的工具，連線到容器中的 SQL Server。

```bash
sqlcmd -E -S 'sql1.contoso.com, 5433'
```

## <a name="next-steps"></a>後續步驟

- [快速入門：使用 Docker 執行 SQL Server 容器映像](quickstart-install-connect-docker.md)
- [將 Linux 主機上的 SQL Server 加入 Active Directory 網域](sql-server-linux-active-directory-auth-overview.md)
