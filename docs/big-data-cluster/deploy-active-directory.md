---
title: 以 Active Directory 模式部署
titleSuffix: SQL Server Big Data Cluster
description: 了解如何升級 Active Directory 網域中的 SQL Server 巨量資料叢集。
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 02/28/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e2ce3fd5655655686d6fb27f628f6bdb3d22ceb1
ms.sourcegitcommit: 7e544aa10f66bb1379bb5675fc063b2097631823
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/29/2020
ms.locfileid: "78200959"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode"></a>以 Active Directory 模式部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文件描述如何在 Active Directory 驗證模式中部署 SQL Server 2019 巨量資料叢集 (BDC)，這將會使用現有 AD 網域進行驗證。

## <a name="background"></a>背景

若要啟用 Active Directory (AD) 驗證，BDC 會自動建立叢集中各種服務所需的使用者、群組、機器帳戶和服務主體名稱 (SPN)。 若要提供這些帳戶的一些內含項目，並允許範圍權限，請在部署期間提名一個組織單位 (OU)，將會在其中建立所有 BDC 相關的 AD 物件。 在叢集部署之前建立此 OU。

若要在 Active Directory 中自動建立所有必要的物件，BDC 在部署期間需要一個 AD 帳戶。 此帳戶必須有權限在提供的 OU 內建立使用者、群組和機器帳戶。

以下步驟假設您已經有 Active Directory 網域控制站。 如果您沒有網域控制站，下列[指南](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx) \(英文\) 包含的步驟可能有幫助。

## <a name="create-ad-objects"></a>建立 AD 物件

使用 AD 整合部署 BDC 之前，請執行下列事項：

1. 建立將會儲存所有 BDC AD 物件的組織單位 (OU)。 您也可以在部署時，選擇提名現有 OU。
1. 為 BDC 建立 AD 帳戶，或使用現有帳戶，並提供正確的權限給此 BDC AD 帳戶。

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>為 BDC 網域服務帳戶在 AD 中建立使用者

巨量資料叢集需要具有特定權限的帳戶。 在繼續之前，請確定您已有現有 AD 帳戶，或建立一個新帳戶，讓巨量資料叢集能夠用來設定必要物件。

若要在 AD 中建立新使用者，您可以在網域或 OU 上按一下滑鼠右鍵，然後選取 [新增]   > [使用者]  ：

![image12](./media/deploy-active-directory/image12.png)

在本文中，將稱呼此使用者「BDC 網域服務帳戶」  。

### <a name="creating-an-ou"></a>建立 OU

在網域控制站上，開啟 [Active Directory 使用者及電腦]  。 在左面板上，以滑鼠右鍵按一下您要建立 OU 的目錄，然後選取 [新增] -\> [組織單位]  ，然後遵循精靈的提示建立 OU。 或者，您可以使用 PowerShell 建立 OU：

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

在本文的範例中，我們將 OU 命名為：`bdc`

![image13](./media/deploy-active-directory/image13.png)

![image14](./media/deploy-active-directory/image14.png)

### <a name="setting-permissions-the-bdc-ad-account"></a>設定 BDC AD 帳戶的權限

不論您已經建立新 AD 使用者，或使用現有 AD 使用者，該使用者都需要有特定權限。 當 BDC 控制器將叢集加入 AD 時，將會使用此使用者帳戶。

BDC 網域服務帳戶 (DSA) 必須能在 OU 中建立使用者、群組和電腦帳戶。 在下列步驟中，我們已經將 BDC 網域服務帳戶命名為 `bdcDSA`。 您可以為此帳戶選擇任何名稱。

1. 在網域控制站上，開啟 [Active Directory 使用者及電腦] 

1. 在左面板中，瀏覽到您的網域，再到 `bdc` 要使用的 OU

1. 以滑鼠右鍵按一下 OU，然後選取 [屬性]  。

1. 移至 [安全性] 索引標籤 (請務必藉由在 OU 上按一下滑鼠右並選取 [進階功能]  ，再選取 [檢視]  )

    ![image15](./media/deploy-active-directory/image15.png)

1. 按一下 [新增]  並新增 **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] DSA** 使用者

    ![image16](./media/deploy-active-directory/image16.png)

    ![image17](./media/deploy-active-directory/image17.png)

1. 選取 **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] DSA** 使用者並清除所有權限，然後按一下 [進階] 

1. 按一下 [新增] 

    ![image18](./media/deploy-active-directory/image18.png)

    - 按一下 [選取主體]  、插入 **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA**，然後按一下 [確定]

    - 將 [類型]  設定為 [允許] 

    - 將 [套用至]  設定為 [此物件及所有子系物件] 

        ![image19](./media/deploy-active-directory/image19.png)

    - 向下捲動到底部，然後按一下 [全部清除] 

    - 捲動回頂端，然後選取：
       - **讀取全部內容**
       - **寫入全部內容**
       - **建立電腦物件**
       - **刪除電腦物件**
       - **建立群組物件**
       - **刪除群組物件**
       - **建立使用者物件**
       - **刪除使用者物件**

    - 按一下 [檔案] &gt; [新增] &gt; [專案] 

- 按一下 [新增] 

    - 按一下 [選取主體]  、插入 **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA**，然後按一下 [確定]

    - 將 [類型]  設定為 [允許] 

    - 將 [套用至]  設定為 [子系電腦物件] 

    - 向下捲動到底部，然後按一下 [全部清除] 

    - 捲動回頂端，然後選取 [重設密碼] 

    - 按一下 [檔案] &gt; [新增] &gt; [專案] 

- 按一下 [新增] 

    - 按一下 [選取主體]  、插入 **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA**，然後按一下 [確定]

    - 將 [類型]  設定為 [允許] 

    - 將 [套用至]  設定為 [子系使用者物件] 

    - 向下捲動到底部，然後按一下 [全部清除] 

    - 捲動回頂端，然後選取 [重設密碼] 

    - 按一下 [檔案] &gt; [新增] &gt; [專案] 

- 再按兩次 [確定]  ，關閉開啟的對話方塊

## <a name="prepare-deployment"></a>準備部署

針對與 AD 整合的 BDC 部署，必須提供一些額外資訊，才能在 AD 中建立 BDC 相關物件。

藉由使用 `kubeadm-prod` 設定檔，您將會自動擁有 AD 整合所需的安全性相關資訊和端點相關資訊的預留位置。

此外，您還需要提供[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]將會用來在 AD 中建立必要物件的認證。 這些認證會以環境變數的形式提供。

## <a name="set-security-environment-variables"></a>設定安全性環境變數

下列環境變數提供 BDC 網域服務帳戶 (將用來設定 AD 整合) 的認證。 此後，BDC 也使用此帳戶來維護 BDC 相關的 AD 物件。

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>提供安全性和端點參數

除了認證的環境變數之外，您也需要提供安全性和端點資訊，AD 整合才能運作。 所需的參數會自動成為 `kubeadm-prod` [部署設定檔](deployment-guidance.md#configfile)的一部分。

AD 整合需要下列參數。 使用本文稍後在下面顯示的 `config replace` 命令，將這些參數新增至 `control.json` 和 `bdc.json` 檔案。 以下所有範例都使用範例網域 `contoso.local`。

- `security.activeDirectory.ouDistinguishedName`：要新增叢集部署所建立所有 AD 帳戶的組織單位 (OU) 辨別名稱。 如果網域稱為 `contoso.local`，則 OU 辨別名稱為：`OU=BDC,DC=contoso,DC=local`。

- `security.activeDirectory.dnsIpAddresses`：網域控制站的 IP 位址清單

- `security.activeDirectory.domainControllerFullyQualifiedDns`:網域控制站的 FQDN 清單。 FQDN 包含網域控制站的機器/主機名稱。 如果您有多個網域控制站，您可以在這裡提供清單。 範例： `HOSTNAME.CONTOSO.LOCAL`

- `security.activeDirectory.realm`**選擇性參數**：在大部分的情況下，領域等於網域名稱。 如果它們不相同，請使用此參數來定義領域的名稱 (例如 `CONTOSO.LOCAL`)。

- `security.activeDirectory.domainDnsName`:您網域的名稱 (例如 `contoso.local`)。

- `security.activeDirectory.clusterAdmins`:此參數接受**一個 AD 群組**。 此群組的成員將會得到叢集中的系統管理員權限。 這表示這些成員將會有 SQL Server 中的系統管理員權限、HDFS 中的超級使用者權限，以及控制器中的系統管理員權限。 **請注意，此群組必須先存在於 AD 中，才能開始部署。另請注意，此群組不能在 Active Directory 中設定 DomainLocal 範圍。設定網域本機範圍的群組將導致部署失敗。**

- `security.activeDirectory.clusterUsers`:大型資料叢集中屬於一般使用者 (無系統管理員權限) 的 AD 群組清單。 **請注意，在開始部署之前，這些群組就必須存在於 AD 中。另請注意，這些群組不能在 Active Directory 中設定 DomainLocal 範圍。設定網域本機範圍的群組將導致部署失敗。**

- `security.activeDirectory.appOwners`**選擇性參數**：AD 使用者或群組的清單，他們有權限建立、刪除和執行任何應用程式。 **請注意，在開始部署之前，這些群組就必須存在於 AD 中。另請注意，這些群組不能在 Active Directory 中設定 DomainLocal 範圍。設定網域本機範圍的群組將導致部署失敗。**

- `security.activeDirectory.appReaders`**選擇性參數**：AD 群組的清單，此群組的成員必須有執行任何應用程式的權限。 **請注意，在開始部署之前，這些群組就必須存在於 AD 中。另請注意，這些群組不能在 Active Directory 中設定 DomainLocal 範圍。設定網域本機範圍的群組將導致部署失敗。**

**如何檢查 AD 群組範圍：** 
[按一下這裡以取得檢查 AD 群組範圍的指示](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps) \(英文\)，以判斷是否是 DomainLocal。

如果您尚未初始化部署設定檔案，您可以執行此命令來取得設定的複本。

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

若要在 `control.json` 檔案中設定上述參數，請使用下列 `azdata` 命令。 該命令會取代設定，並在部署之前提供您自己的值。

 > [!IMPORTANT]
 > 在 SQL Server 2019 CU2 版本中，部署設定檔案中安全性組態區段的結構已有顯著的變更，且所有 Active Directory 相關設定都位於 *control.json* 檔案內 「安全性」  底下 JSON 樹狀目錄的新 *activeDirectory* 中。

以下範例是以使用 SQL Server 2019 CU2 為基礎。 此範例會示範如何取代部署組態中與 AD 相關的參數值。以下的網域詳細資料是範例值。

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

同樣地，在 SQL Server 2019 CU2 之前的版本中，您可以執行：

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

除了上述資訊之外，您還需要為不同叢集端點提供 DNS 名稱。 在部署時，系統會自動在您的 DNS 伺服器中建立使用所提供 DNS 名稱的 DNS 項目。 當您連線到不同叢集端點時，將會使用這些名稱。 例如，如果 SQL 主要執行個體的 DNS 名稱是 `mastersql`，您將會使用 `mastersql.contoso.local,31433` 來從工具連線到主要執行個體。

> [!NOTE]
> 請務必針對您在下方定義的名稱，在 DNS 伺服器中建立 DNS 項目。 針對 `kubeadm` 部署，舉例來說，您可以在建立 DNS 專案時，使用 Kubernetes 主要節點的 IP 位址。

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

您可以在這裡找到適用於[使用 AD 整合在單一節點 Kubernetes 叢集 (kubeadm) 上部署 SQL Server 巨量資料叢集](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad) \(英文\) 的範例指令碼。

您現在應該已設定使用 Active Directory 整合進行 BDC 部署的所有必要參數。

如需如何部署[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]的完整文件，請瀏覽[官方文件](deployment-guidance.md)。

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>確認網域控制站的反向 DNS 項目

請確定網域控制站本身的反向 DNS 項目 (PTR 記錄) 已在 DNS 伺服器中註冊。 您可以藉由在網域控制站上執行網域名稱的 `nslookup`，以確認它可以解析為網域控制站的 IP 位址。

## <a name="connect-to-cluster-endpoints-in-ad-mode"></a>以 AD 模式連線到叢集端點

使用 AD 驗證登入 SQL Server 主要執行個體。

若要確認對 SQL Server 執行個體的 AD 連線，請使用 `sqlcmd`連線到 SQL 主要執行個體。 在部署時，系統會為提供的群組自動建立登入 (`clusterUsers` 和 `clusterAdmins`)。

如果您使用 Linux，請先以 AD 使用者的身分執行 `kinit`，然後執行 `sqlcmd`。 如果您使用 Windows，只要以所需的使用者身分，從**已加入網域的用戶端機器**登入即可。

### <a name="connect-to-master-instance-from-linuxmac"></a>從 Linux/Mac 連線到主要執行個體

```bash
kinit <username>@<domain name>
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="connect-to-master-instance-from-windows"></a>從 Windows 連線到主要執行個體

```cmd
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="log-in-to-sql-server-master-instance-using-azure-data-studio-or-ssms"></a>使用 Azure Data Studio 或 SSMS 登入 SQL Server 主要執行個體

從已加入網域的用戶端，您可以開啟 SSMS 或 Azure Data Studio 並連線到主要執行個體。 這與使用 AD 驗證連線到任何 SQL Server 執行個體的體驗相同。

從 SSMS：

![影像23](./media/deploy-active-directory/image23.png)

從 Azure Data Studio：

![影像24](./media/deploy-active-directory/image24.png)}

### <a name="log-in-to-controller-with-ad-authentication"></a>使用 AD 驗證來登入控制器

#### <a name="connect-to-controller-with-ad-authentication-from-linuxmac"></a>從 Linux/Mac 使用 AD 驗證連線到控制器

您可以使用 `azdata` 和 AD 驗證來連線到控制器端點。

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
```

#### <a name="connect-to-controller-with-ad-authentication-from-windows"></a>從 Windows 使用 AD 驗證連線到控制器

```cmd
azdata login -e https://<controller DNS name>:30080 --auth ad
```

### <a name="use-ad-authentication-to-knox-gateway-webhdfs"></a>將 AD 驗證用於 Knox 閘道 (webHDFS)

您也可以透過 Knox 閘道端點，使用 curl 發出 HDFS 命令。 這需要對 Knox 進行 AD 驗證。 以下 curl 的命令會透過 Knox 閘道發出 webHDFS REST 呼叫，以建立稱為 `products` 的目錄

```bash
curl -k -v --negotiate -u : https://<Gateway DNS name>:30443/gateway/default/webhdfs/v1/products?op=MKDIRS -X PUT
```

## <a name="known-issues-and-limitations"></a>已知問題和限制

**此版本中要注意的限制：**

- 目前，[記錄搜尋] 儀表板和 [計量] 儀表板不支援 AD 驗證。 已針對未來版本規劃此端點的 AD 支援。 在部署時設定的基本使用者名稱和密碼，可用來進行這些儀表板的驗證。 所有其他叢集端點都支援 AD 驗證。

- 目前，安全 AD 模式只適用於 `kubeadm` 部署環境，而不適用於 AKS 上。 根據預設，`kubeadm-prod` 部署設定檔包含安全性區段。

- 目前，每個網域 (Active Directory) 只可有一個 BDC。 已針對未來版本規劃啟用每個網域多個 BDC。

- 安全性設定中指定的任何 AD 群組都不能設定 DomainLocal 範圍。 您可以遵循[這些指示](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps)，以檢查 AD 群組的範圍。
