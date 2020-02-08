---
title: 部署主機守護者服務
description: 部署主機守護者服務以取得具有安全記憶體保護區的 Always Encrypted。
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6794f5fd57d1c89e7c1989e79b5072a8c15cf43e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "74320051"
---
# <a name="deploy-the-host-guardian-service-for-include-ssnoversion-mdincludesssnoversion-mdmd"></a>針對 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 部署主機守護者服務

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

此文章描述如何針對 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 將主機守護者服務 (HGS) 部署為證明服務。
在開始之前，請務必閱讀[規劃主機守護者服務證明](./always-encrypted-enclaves-host-guardian-service-plan.md)一文以取得先決條件的完整清單和架構指引。

## <a name="step-1-set-up-the-first-hgs-computer"></a>步驟 1:設定第一部 HGS 電腦

主機守護者服務 (HGS) 會在一或多部電腦上以叢集服務的形式執行。
在此步驟中，您將會在第一部電腦上設定新的 HGS 叢集。
如果您已經擁有 HGS 叢集，且正在為它新增額外的電腦以取得高可用性，請跳到[步驟 2：將更多 HGS 電腦新增至叢集](#step-2-add-more-hgs-computers-to-the-cluster)。

在開始之前，請確定您使用的電腦是執行 Windows Server 2019 Standard 或 Datacenter 版本、您具有本機系統管理員權限，而且該電腦尚未加入 Active Directory 網域。

1. 以本機系統管理員身分登入第一部 HGS 電腦，然後開啟已提高權限的 Windows PowerShell 主控台。 執行下列命令以安裝主機守護者服務角色。 電腦將會自動重新啟動以套用變更。

    ```powershell
    Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
    ```

2. 在 HGS 電腦重新啟動之後，請在已提高權限的 Windows PowerShell 主控台中執行下列命令，以安裝新的 Active Directory 樹系：

    ```powershell
    # Select the name for your new Active Directory root domain.
    # Make sure the name does not conflict with, and is not subordinate to, any existing domains on your network.
    $HGSDomainName = 'bastion.local'

    # Specify a Directory Services Restore Mode password that can be used to recover your domain in safe mode.
    # This password is not, and will not change, your admin account password.
    # Save this password somewhere safe and include it in your disaster recovery plan.
    $DSRMPassword = Read-Host -AsSecureString -Prompt "Directory Services Restore Mode Password"

    Install-HgsServer -HgsDomainName $HgsDomainName -SafeModeAdministratorPassword $DSRMPassword -Restart
    ```

    您的 HGS 電腦將會再次重新啟動以完成設定 Active Directory 樹系。 在您下一次登入時，您的系統管理員帳戶將會是網域系統管理員帳戶。 我們建議檢閱 [Active Directory Domain Services 作業文件](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/ad-ds-operations) \(部分機器翻譯\)，以取得管理及保護您新樹系的詳細資訊。

3. 接下來，您將會在已提高權限的 Windows PowerShell 主控台中執行下列命令，來設定 HGS 叢集並安裝證明服務：

    ```powershell
    # Note: the name you provide here will be shared by all HGS nodes and used to point your SQL Server computers to the HGS cluster.
    # For example, if you provide "attsvc" here, a DNS record for "attsvc.yourdomain.com" will be created for every HGS computer.
    Initialize-HgsAttestation -HgsServiceName 'hgs'
    ```

## <a name="step-2-add-more-hgs-computers-to-the-cluster"></a>步驟 2:將更多 HGS 電腦新增至叢集

在設定您的第一部 HGS 電腦及叢集之後，您可以新增額外的 HGS 伺服器以提供高可用性。
如果您只要設定一部 HGS 伺服器 (例如用於開發/測試環境)，您可以跳到步驟 3。

和第一步 HGS 電腦相同，請確定您要加入叢集的電腦是執行 Windows Server 2019 Standard 或 Datacenter 版本、您具有本機系統管理員權限，而且該電腦尚未加入 Active Directory 網域。

1. 以本機系統管理員身分登入電腦，然後開啟已提高權限的 Windows PowerShell 主控台。 執行下列命令以安裝主機守護者服務角色。 電腦將會自動重新啟動以套用變更。

    ```powershell
    Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
    ```

2. 檢查電腦上的 DNS 用戶端設定，以確定它可以解析 HGS 網域。 下列命令應該會傳回您 HGS 伺服器的 IP 位址。 如果您無法解析 HGS 網域，您可能需要更新您網路介面卡上的 DNS 伺服器資訊，以使用 HGS DNS 伺服器進行名稱解析。

    ```powershell
    # Change 'bastion.local' to the domain name you specified in Step 1.2
    nslookup bastion.local

    # If it fails, use sconfig.exe, option 8, to set the first HGS computer as your preferred DNS server.
    ```

3. 在電腦重新啟動之後，請在已提高權限的 Windows PowerShell 主控台中執行下列命令，以將該電腦加入由第一部 HGS 伺服器所建立的 Active Directory 網域。 您將會需要 AD 網域的網域系統管理員認證以執行此命令。 命令完成之後，電腦將會重新啟動，並成為 HGS 網域的 Active Directory 網域控制站。

    ```powershell
    # Provide the fully qualified HGS domain name
    $HGSDomainName = 'bastion.local'

    # Provide a domain administrator's credential for the HGS domain
    $DomainAdminCred = Get-Credential

    # Specify a Directory Services Restore Mode password that can be used to recover your domain in safe mode.
    # This password is not, and will not change, your admin account password.
    # Save this password somewhere safe and include it in your disaster recovery plan.
    $DSRMPassword = Read-Host -AsSecureString -Prompt "Directory Services Restore Mode Password"

    Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $DomainAdminCred -SafeModeAdministratorPassword $DSRMPassword -Restart
    ```

4. 在電腦重新啟動之後，請使用網域系統管理員認證登入。 開啟已提高權限的 Windows PowerShell 主控台，並執行下列命令以設定證明服務。 由於證明服務為叢集感知，它將會從其他叢集成員複製其設定。 在任何 HGS 節點上對證明原則所做的變更都會套用到所有其他叢集。

    ```powershell
    # Provide the IP address of an existing, initialized HGS server
    # If you are using separate networks for cluster and application traffic, choose an IP address on the cluster network.
    # You can find the IP address of your HGS server by signing in and running "ipconfig /all"
    Initialize-HgsAttestation -HgsServerIPAddress '172.16.10.20'
    ```

5. 針對您想要新增至 HGS 叢集的每一部電腦重複步驟 2。

## <a name="step-3-configure-a-dns-forwarder-to-your-hgs-cluster"></a>步驟 3：針對您的 HGS 叢集設定 DNS 轉寄站

HGS 會執行自己的 DNS 伺服器，其中包含解析證明服務所需的名稱記錄。
您的 SQL Server 電腦將會無法解析這些記錄，直到您將網路的 DNS 伺服器設定為將要求轉送到 HGS DNS 伺服器為止。

設定 DNS 轉寄站的程序會依廠商而有所不同，所以我們建議連絡您的網路系統管理員以取得適用於您特定網路的正確指引。

如果您正在使用適用於您公司網路的 Windows Server DNS 伺服器角色，您的 DNS 系統管理員可以針對 HGS 網域建立條件式轉寄站，來僅轉送針對 HGS 網域的要求。
例如，如果您的 HGS 伺服器使用 "bastion.local" 網域名稱，且具有 172.16.10.20、172.16.10.21 及 172.16.10.22 的 IP 位址，您可以在公司 DNS 伺服器上執行下列命令來設定條件式轉寄站：

```powershell
# Tip: make sure to provide every HGS server's IP address
# If you use separate NICs for cluster and application traffic, use the application traffic NIC IP addresses here
Add-DnsServerConditionalForwarderZone -Name 'bastion.local' -ReplicationScope "Forest" -MasterServers "172.16.10.20", "172.16.10.21", "172.16.10.22"
```

## <a name="step-4-configure-the-attestation-service"></a>步驟 4：設定證明服務

HGS 支援兩種證明模式：TPM 證明，用來對每部 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦的完整性和身分識別進行密碼編譯驗證；以及主機金鑰證明，用來對 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦的身分識別進行簡單驗證。
如果您尚未選取證明模式，請查看[規劃指南](./always-encrypted-enclaves-host-guardian-service-plan.md#attestation-modes)中的證明資訊，以取得每種模式安全性保證和使用案例的詳細資料。

此節中的步驟將會針對特定的證明模式設定基本證明原則。
您將會在步驟 4 中註冊主機特定資訊。
如果您在未來需要變更證明模式，請搭配所需的證明模式重複步驟 3 和 4。

### <a name="switch-to-tpm-attestation"></a>切換至 TPM 證明

若要在 HGS 上設定 TPM 證明，您需要具有網際網路存取的電腦，以及至少一部具有 TPM 2.0 rev 1.16 晶片的 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦。

若要設定 HGS 以使用 TPM 模式，請開啟已提高權限的 PowerShell 主控台並執行下列命令：

```powershell
Set-HgsServer -TrustTpm
```

當 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦嘗試證明時，您叢集中的所有 HGS 電腦現在都會使用 TPM 模式。

在您可以向 HGS 註冊您 SQL Server 電腦的 TPM 資訊之前，您必須安裝來自您 TPM 廠商的簽署金鑰 (EK) 根憑證。
每部實體 TPM 在原廠都會設定唯一的簽署金鑰，該金鑰附有能識別製造商的簽署金鑰憑證。
此憑證可確保您的 TPM 為正版。
HGS 會在您向 HGS 註冊新 TPM 時，透過比較憑證鏈結和受信任的根憑證清單來驗證簽署金鑰憑證。

Microsoft 會發佈已知良好的 TPM 廠商根憑證清單，讓您可以匯入 HGS 受信任的 TPM 根憑證存放區。
如果您的 SQL Server 電腦已虛擬化，您需要連絡您的雲端服務提供者或虛擬化平台廠商，以取得如何取得您虛擬 TPM 簽署金鑰之憑證鏈結的相關資訊。

若要針對實體 TPM 從 Microsoft 下載受信任的 TPM 根憑證套件，請完成下列步驟：

1. 在具有網際網路存取的電腦上，從 [https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925) 下載最新的 TPM 根憑證套件

2. 確認 cab 檔案的簽章以確保它的真實性。

    ```powershell
    # Note: replace the path below with the correct one to the file you downloaded in step 1
    Get-AuthenticodeSignature ".\TrustedTpm.cab"
    ```

    > [!WARNING]
    > 如果簽章無效，請不要繼續，並連絡 Microsoft 支援服務以獲得協助。

3. 將 cab 檔案展開至新的目錄。

    ```powershell
    mkdir .\TrustedTpmCertificates
    expand.exe -F:* ".\TrustedTpm.cab" ".\TrustedTpmCertificates"
    ```

4. 在新的目錄中，您將能看見每個 TPM 廠商的目錄。 您可以刪除您未使用之廠商的目錄。

5. 將整個 "TrustedTpmCertificates" 目錄複製到您的 HGS 伺服器。

6. 在 HGS 伺服器上開啟已提高權限的 PowerShell 主控台，然後執行下列命令以匯入所有 TPM 根和中繼憑證：

    ```powershell
    # Note: replace the path below with the correct location of the TrustedTpmCertificates folder on your HGS computer
    cd "C:\scratch\TrustedTpmCertificates"
    .\setup.cmd
    ```

7. 針對每部 HGS 電腦重複步驟 5 和 6。

如果您從您的 OEM、雲端服務提供者，或是虛擬化平台廠商取得中繼和根 CA 憑證，您可以直接將憑證匯入相對應的本機電腦憑證存放區：`TrustedHgs_RootCA` 或 `TrustedHgs_IntermediateCA`。 例如，在 PowerShell 中：

```powershell
# Imports MyCustomTpmVendor_Root.cer to the local machine's "TrustedHgs_RootCA" store
Import-Certificate -FilePath ".\MyCustomTpmVendor_Root.cer" -CertStoreLocation "Cert:\LocalMachine\TrustedHgs_RootCA"
```

### <a name="switch-to-host-key-attestation"></a>切換至主機金鑰證明

若要使用主機金鑰證明，請在 HGS 伺服器上已提高權限的 PowerShell 主控台中執行下列命令：

```powershell
Set-HgsServer -TrustHostKey
```

當 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦嘗試證明時，您叢集中的所有 HGS 電腦現在都會使用主機金鑰模式。

## <a name="step-5-configure-the-hgs-https-binding"></a>步驟 5：設定 HGS HTTPS 繫結

在預設安裝中，HGS 只會公開 HTTP (連接埠 80) 繫結。
您可以設定 HTTPS (連接埠 443) 繫結來加密 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦和 HGS 之間的所有通訊。
我們建議所有 HGS 的生產執行個體都使用 HTTPS 繫結。

1. 從您的憑證授權單位取得 TLS 憑證，並使用來自步驟 1.3 的完整 HGS 服務名稱作為主體名稱。 如果您不知道自己的服務名稱，則可以在任何 HGS 電腦上執行 `Get-HgsServer` 來找到它。 如果您的 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦使用不同的 DNS 名稱來連線至您的 HGS 叢集 (例如，如果 HGS 位於具有不同位址的網路負載平衡器後方)，您可以將替代 DNS 名稱新增到主體替代名稱清單中。

2. 在 HGS 電腦上，使用 [Set-HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/set-hgsserver) \(英文\) 來啟用 HTTPS 繫結，並指定在上述步驟中取得的 TLS 憑證。 如果您的憑證已經安裝在電腦上的本機憑證存放區中，請使用下列命令來向 HGS 註冊它：

    ```powershell
    # Note: you'll need to know the thumbprint for your certificate to configure HGS this way
    Set-HgsServer -Http -Https -HttpsCertificateThumbprint "54A043386555EB5118DB367CFE38776F82F4A181"
    ```

    如果您已將憑證 (搭配私密金鑰) 匯出至受密碼保護的 PFX 檔案中，您可以執行下列命令來向 HGS 註冊它：

    ```powershell
    $PFXPassword = Read-Host -AsSecureString -Prompt "PFX Password"
    Set-HgsServer -Http -Https -HttpsCertificatePath "C:\path\to\hgs_tls.pfx" -HttpsCertificatePassword $PFXPassword
    ```

3. 針對叢集中的每部 HGS 電腦重複步驟 1 和 2。 TLS 憑證不會自動在 HGS 節點之間複寫。 此外，每部 HGS 電腦都可以擁有自己的唯一 TLS 憑證，前提是主體必須符合 HGS 服務名稱。

## <a name="next-steps"></a>後續步驟

- [向 HGS 註冊電腦](./always-encrypted-enclaves-host-guardian-service-register.md)
