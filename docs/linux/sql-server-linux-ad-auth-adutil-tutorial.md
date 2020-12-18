---
title: 使用 adutil 為 Linux 上的 SQL Server 設定 Active Directory 驗證
description: 逐步教學：使用 adutil 為 Linux 上的 SQL Server 設定 Active Directory 驗證
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.date: 12/10/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 462c48c7d0ade07c62a154927c352962f454cc46
ms.sourcegitcommit: 18e2f0706e03d0b2b6324845244fbafaa077a8dd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2020
ms.locfileid: "97103277"
---
# <a name="tutorial-configure-active-directory-authentication-with-sql-server-on-linux-using-adutil"></a>教學課程：使用 adutil 為 Linux 上的 SQL Server 設定 Active Directory 驗證

> [!NOTE]
> **adutil** 目前為 **公開預覽** 狀態

本教學課程說明如何使用 adutil 為 Linux 上的 SQL Server 設定 Active Directory (AD) 驗證。 如需另一種使用 ktpass 設定 AD 驗證的方法，請參閱[教學課程：在 Linux 上的 SQL Server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。

本教學課程包含下列工作：

> [!div class="checklist"]
> - 安裝 adutil-preview
> - 將 Linux 電腦加入 AD 網域
> - 為 SQL Server 建立 AD 使用者，並使用 adutil 工具來設定 ServicePrincipalName (SPN)
> - 建立 SQL Server 服務 keytab 檔案
> - 將 SQL Server 設定為使用 keytab 檔案
> - 使用 Transact-SQL 建立以 AD 為基礎的 SQL Server 登入
> - 使用 AD 驗證連線到 SQL Server

## <a name="prerequisites"></a>Prerequisites

設定 AD 驗證之前，必須具備下列條件：

- 網路中擁有 AD 網域控制站 (Windows)。
- 在 Linux 主機電腦上安裝 adutil-preview 工具。 根據將要安裝 adutil-preview 的 Linux 發行版，依其版本遵循下列章節。

## <a name="install-adutil-preview"></a>安裝 adutil-preview

在 Linux 主機電腦上，使用下列命令來安裝 adutil-preview。

> [!NOTE]
> 在此預覽版本中，我們知道對於某些 Linux 發行版，如果嘗試安裝 adutil 時沒有 `ACCEPT_EULA` 參數，則無法順利安裝。 建議使用 `ACCEPT_EULA=Y` 設定來安裝 adutil-preview 工具。 您可在安裝前，先閱讀預覽 [EULA](https://go.microsoft.com/fwlink/?linkid=2151376)。 我們正積極處理這個問題，此問題應會在 GA 版本中完成修正。

### <a name="rhel"></a>RHEL

1. 下載 Microsoft Red Hat 存放庫組態檔。

    ```bash
    sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/8/prod.repo
    ```

1. 如果已安裝舊版的 adutil，請移除所有舊版的 adutil 套件。

    ```bash
    sudo yum remove adutil
    ```

1. 執行下列命令以安裝 adutil-preview。 `ACCEPT_EULA=Y` 會接受 adutil 的預覽 EULA。 EULA 會位於路徑 '/usr/share/adutil/'。

    ```bash
    sudo ACCEPT_EULA=Y yum install -y adutil-preview
    ```

### <a name="ubuntu"></a>Ubuntu

1. 註冊 Microsoft Ubuntu 存放庫。

    ```bash
    sudo curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
    ```

1. 如果已安裝舊版的 adutil，請使用下列命令移除所有舊版的 adutil 套件

    ```bash
    sudo apt-get remove adutil
    ```

1. 執行下列命令以安裝 adutil-preview。 `ACCEPT_EULA=Y` 會接受 adutil 的預覽 EULA。 EULA 會位於路徑 '/usr/share/adutil/'。

    ```bash
    sudo ACCEPT_EULA=Y apt-get install -y adutil-preview
    ```

### <a name="sles"></a>SLES

1. 將 Microsoft SQL Server 存放庫新增至 Zypper。

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
    ```

1. 如果已安裝舊版的 adutil，請移除所有舊版的 adutil 套件。

    ```bash
    sudo zypper remove adutil
    ```

1. 執行下列命令以安裝 adutil-preview。 `ACCEPT_EULA=Y` 會接受 adutil 的預覽 EULA。 EULA 會位於路徑 '/usr/share/adutil/'。

    ```bash
    sudo ACCEPT_EULA=Y zypper install -y adutil-preview
    ```

## <a name="domain-machine-preparation"></a>準備網域機器

請確定已在 Linux 主機 IP 位址的 Active Directory 中，新增轉送主機 (A) 項目。 在本教學課程中，`myubuntu` 主機機器的 IP 位址為 `10.0.0.10`。 我們會在 Active Directory 中新增轉送主機項目，如下所示。 此項目可確保當使用者連線至 myubuntu.contoso.com 時，能夠連接到正確的主機。

:::image type="content" source="media/sql-server-linux-ad-auth-adutil-tutorial/host-a-record.png" alt-text="新增主機記錄":::

在本教學課程中，我們會在 Azure 中使用具有三個 VM 的環境。 其中一部 VM 作為 Windows 網域控制站 (DC)，其網域名稱為 `contoso.com`。 此網域控制站的名稱為 `adVM.contoso.com`。 第二部機器是執行 Windows 10 Desktop 且稱為 `winbox` 的 Windows 機器，其作為用戶端機上盒，並已安裝 SQL Server Management Studio (SSMS)。 第三部機器是名為 `myubuntu` 的 Ubuntu 18.04 LTS 機器，其裝載了 SQL Server。

## <a name="join-the-linux-host-machine-to-your-ad-domain"></a>將 Linux 主機機器加入 AD 網域

將 SQL Server Linux 主機加入 Active Directory 網域控制站。 如需如何加入 Active Directory 網域的資訊，請參閱[將 Linux 主機上的 SQL Server 加入 Active Directory 網域](sql-server-linux-active-directory-join-domain.md)。

## <a name="create-an-ad-user-for-sql-server-and-set-the-serviceprincipalname-spn-using-the-adutil-tool"></a>為 SQL Server 建立 AD 使用者，並使用 adutil 工具來設定 ServicePrincipalName (SPN)

1. 使用 `kinit` 命令取得或更新 Kerberos TGT (票證授權票證)。 針對 `kinit` 命令使用具特殊權限的帳戶。 此帳戶必須具有連線到網域的權限，且必須能夠在網域中建立帳戶和 SPN。

    > [!IMPORTANT]
    > 執行此命令之前，主機機器應該已經加入網域，如上一個步驟所示。

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
    > 您可使用下列三種方式中的任意一種來指定密碼：
    >
    > - 密碼旗標：--password \<password\>
    > - 環境變數 - `ADUTIL_ACCOUNT_PWD`
    > - 互動式輸入
    >
    > 密碼輸入方法的優先順序會遵循上方所列選項順序。 建議使用環境變數或互動式輸入來提供密碼，因為這兩者相較於密碼旗標要更為安全。

    您可使用如上所示的辨別名稱 (`-distname`) 來指定帳戶的名稱，也可以使用組織單位 (OU) 名稱。 若同時指定這兩種名稱，則 OU 名稱 (`--ou`) 會優先於辨別名稱。 您可執行下列命令以取得更多詳細資料：

    ```bash
    adutil user create --help
    ```

3. 向以上建立的主體註冊 SPN。 使用機器 FQDN。 在本教學課程中，我們會使用 SQL Server 的預設連接埠 1433， 但連接埠號碼可能有所不同。

    ```bash
    adutil spn addauto -n sqluser -s MSSQLSvc -H myubuntu.contoso.com -p 1433
    ```

    > [!NOTE]
    >
    > - `addauto` 會自動建立 SPN，但前提是 kinit 帳戶有足夠的權限。
    > - `-n`：要指派給 SPN 的帳戶名稱。
    > - `-s`：要用來產生 SPN 的服務名稱。 因為此為 SQL Server 服務相關案例，所以服務名稱為 `MSSQLSvc`。
    > - `-H`：要用來產生 SPN 的主機名稱。 如果未指定，則會使用本機主機的 FQDN。 在本案例中，主機名稱為 `myubuntu`，FQDN 為 `myubuntu.contoso.com`。
    > - `-p`：要用來產生 SPN 的連接埠。 如果未指定，則會在不使用連接埠的情況下產生 SPN。 只有當 SQL Server 接聽預設連接埠 1433 時，本案例中的 SQL 連線才會正常運作。

## <a name="create-the-sql-server-service-keytab-file"></a>建立 SQL Server 服務 keytab 檔案

建立 keytab 檔案，在該檔案中，先前所建立的 4 個 SPN 皆各有一個項目，而使用者也擁有一個項目。

```bash
adutil keytab createauto -k /var/opt/mssql/secrets/mssql.keytab -p 1433 -H myubuntu.contoso.com --password 'P@ssw0rd' -s MSSQLSvc 
```

> [!NOTE]
>
> - `-k`：欲建立 `mssql.keytab` 檔案的路徑。 在上述範例中，目錄 `/var/opt/mssql/secrets/` 應該已經存在於主機上。
> - `-p`：要用來產生 SPN 的連接埠。 如果未指定，則會在不使用連接埠的情況下產生 SPN。
> - `-H`：要用來產生 SPN 的主機名稱。 如果未指定，則會使用本機主機的 FQDN。 在本案例中，主機名稱為 `myubuntu`，FQDN 為 `myubuntu.contoso.com`。
> - `-s`：要用來產生 SPN 的服務名稱。 因為此為 SQL Server 服務相關案例，所以服務名稱為 `MSSQLSvc`。
> - `--password`：這是稍早所建立具特殊權限 AD 使用者帳戶的密碼。
> - `-e` 或 `--enctype`：keytab 項目的加密類型。 使用以逗號分隔的值清單。 如果未指定，則會顯示互動式提示。

當提供加密類型的選項時，即可選擇一個以上的加密類型。 在此範例中，我們會選擇 `aes256-cts-hmac-sha1-96` 與 `arcfour-hmac`。 請確定主機與網域支援所選的加密類型。

如果想要以非互動方式選擇加密類型，您可在上述命令中，使用 -e 引數來指定所選的加密類型。 如需 adutil 命令的其他說明，請執行以下命令。

```bash
adutil keytab createauto --help
```

> [!NOTE]
> `arcfour-hmac` 是弱式加密，且不建議在生產環境中使用此加密類型。

在 keytab 中為主體名稱與其密碼新增項目，以供 SQL Server 用來連線到 AD：

```bash
adutil keytab create -k /var/opt/mssql/secrets/mssql.keytab -p sqluser --password 'P@ssw0rd!'
```

> [!NOTE]
>
> - `-k`：欲建立 `mssql.keytab` 檔案的路徑。
> - `-p`：要新增至 keytab 的主體。

adutil keytab 建立/自動建立不會覆寫先前的檔案，只會附加至檔案 (如果檔案已經存在)。

請確定所建立的 keytab 是由 `mssql` 使用者所擁有，且只有 `mssql` 使用者具有該檔案的讀取/寫入存取權。 您可執行 `chown` 與 `chmod` 命令，如下所示：

```bash
chown mssql. /var/opt/mssql/secrets/mssql.keytab
chmod 440 /var/opt/mssql/secrets/mssql.keytab
```

## <a name="configure-sql-server-to-use-the-keytab"></a>將 SQL Server 設定為使用 keytab

執行以下命令，將 SQL Server 設定為使用在上一個步驟中建立的 keytab，並將具特殊權限的 AD 帳戶設為以上建立的使用者。 在範例中，使用者名稱為 `sqluser`。

```bash
/opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
/opt/mssql/bin/mssql-conf set network.privilegedadaccount sqluser
```

## <a name="restart-sql-server"></a>重新啟動 SQL Server

執行以下命令，以重新啟動 SQL Server 服務：

```bash
sudo systemctl restart mssql-server
```

## <a name="create-ad-based-sql-server-logins-in-transact-sql"></a>在 Transact-SQL 中建立以 AD 為基礎的 SQL Server 登入

連線到 SQL Server 並執行下列命令來建立登入，並確認登入已確實列出。

```sql
create login [contoso\amvin] From Windows
SELECT name FROM sys.server_principals;
```

## <a name="connect-to-sql-server-using-ad-authentication"></a>使用 AD 驗證連線到 SQL Server。

若要使用 [SSMS](../ssms/download-sql-server-management-studio-ssms.md) 或 [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md) 進行連線，請使用 Windows 認證登入 SQL Server。

您也可以透過 [sqlcmd](../tools/sqlcmd-utility.md) 之類的工具來使用 Windows 驗證連線到 SQL Server。

```bash
sqlcmd -E -S 'myubuntu.contoso.com'
```

## <a name="next-steps"></a>後續步驟

- [將 Linux 主機上的 SQL Server 加入 Active Directory 網域](sql-server-linux-active-directory-auth-overview.md)
- 如果想要了解如何使用 Linux 上的 SQL Server 容器來設定 AD 驗證，請參閱[使用 Linux 上的 SQL Server 容器來設定 Active Directory 驗證](sql-server-linux-containers-ad-auth-adutil-tutorial.md)
