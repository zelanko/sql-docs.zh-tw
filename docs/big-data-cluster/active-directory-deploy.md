---
title: 以 Active Directory 模式部署
titleSuffix: SQL Server Big Data Cluster
description: 了解如何升級 Active Directory 網域中的 SQL Server 巨量資料叢集。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fb42be7b0affc351a013e29af9370d1a109e3d93
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91898707"
---
# <a name="deploy-sql-server-big-data-cluster-in-active-directory-mode"></a>以 Active Directory 模式部署 SQL Server 巨量資料叢集

本文描述如何在 Active Directory 模式中部署 SQL Server 巨量資料叢集。 完成本文中的步驟需要存取 Active Directory 網域。 在繼續之前，您必須先完成[在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-prerequisites.md) 一文中所述的要求。

## <a name="prepare-deployment"></a>準備部署

針對與 AD 整合的 BDC 部署，必須提供一些額外資訊，才能在 AD 中建立 BDC 相關物件。

藉由使用 `kubeadm-prod` 設定檔 (或從 CU5 版本開始可使用 `openshift-prod`)，您將會自動擁有 AD 整合所需安全性相關資訊和端點相關資訊的預留位置。

此外，您還需要提供[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]將會用來在 AD 中建立必要物件的認證。 這些認證會以環境變數的形式提供。

## <a name="set-security-environment-variables"></a>設定安全性環境變數

下列環境變數提供 BDC 網域服務帳戶 (將用來設定 AD 整合) 的認證。 此後，BDC 也使用此帳戶來維護 BDC 相關的 AD 物件。

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>提供安全性和端點參數

除了認證的環境變數之外，您也需要提供安全性和端點資訊，AD 整合才能運作。 所需的參數會自動成為 `kubeadm-prod`/`openshift-prod` [部署設定檔](deployment-guidance.md#configfile)的一部分。

AD 整合需要下列參數。 使用本文稍後在下面顯示的 `config replace` 命令，將這些參數新增至 `control.json` 和 `bdc.json` 檔案。 以下所有範例都使用範例網域 `contoso.local`。

- `security.activeDirectory.ouDistinguishedName`：要新增叢集部署所建立所有 AD 帳戶的組織單位 (OU) 辨別名稱。 如果網域稱為 `contoso.local`，則 OU 辨別名稱為：`OU=BDC,DC=contoso,DC=local`。

- `security.activeDirectory.dnsIpAddresses`：包含網域的 DNS 伺服器 IP 位址清單。 

- `security.activeDirectory.domainControllerFullyQualifiedDns`:網域控制站的 FQDN 清單。 FQDN 包含網域控制站的機器/主機名稱。 如果您有多個網域控制站，您可以在這裡提供清單。 範例： `HOSTNAME.CONTOSO.LOCAL`.

  > [!IMPORTANT]
  > 當多個網域控制站正在為網域提供服務時，請使用主要網域控制站 (PDC) 作為安全性設定中 `domainControllerFullyQualifiedDns` 清單內的第一個項目。若要取得 PDC 名稱，請在命令提示字元中鍵入 `netdom query fsmo`，然後按下 **ENTER**。

- `security.activeDirectory.realm`**選擇性參數**：在大部分的情況下，領域等於網域名稱。 如果它們不相同，請使用此參數來定義領域的名稱 (例如 `CONTOSO.LOCAL`)。 為這個參數提供的值必須是完整名稱。

  > [!IMPORTANT]
  > 目前，BDC 不支援 Active Directory 網域名稱與 Active Directory 網域的 **NETBIOS** 名稱不同的設定。

- `security.activeDirectory.domainDnsName`:將用於叢集的 DNS 網域名稱 (例如 `contoso.local`)。

- `security.activeDirectory.clusterAdmins`:此參數接受一個 AD 群組。 AD 群組範圍必須是通用或全域。 此群組的成員將具備 `bdcAdmin` 叢集角色，使其在叢集內具備系統管理員權限。 這表示這些成員將具備 [SQL Server 中的 `sysadmin` 權限](../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles)、[HDFS 中的 `superuser` 權限](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#The_Super-User)，以及在連線到控制器端點時具備系統管理員權限。

  >[!IMPORTANT]
  >開始部署之前，請在 AD 中建立此群組。 如果此 AD 群組的範圍是網域本機，則部署會失敗。

- `security.activeDirectory.clusterUsers`:大型資料叢集中屬於一般使用者 (無系統管理員權限) 的 AD 群組清單。 此清單可包含範圍為通用或全域群組的 AD 群組。 其不能是網域本機群組。

此清單中的 AD 群組會對應到 `bdcUser` 巨量資料叢集角色，且需要授與 SQL Server 存取權 (請參閱 [SQL Server 權限](../relational-databases/security/permissions-hierarchy-database-engine.md))，或 HDFS (請參閱 [HDFS 權限指南](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#:~:text=Permission%20Checks%20%20%20%20Operation%20%20,%20%20N%2FA%20%2029%20more%20rows%20))。 當連線到控制器端點時，這些使用僅能使用 `azdata bdc endpoint list` 命令列出叢集內可用的端點。

如需如何更新此設定 AD 群組的詳細資料，請參閱[在 Active Directory 模式中管理巨量資料叢集存取](manage-user-access.md)。

  >[!TIP]
  >若要在連線到 Azure Data Studio 中的 SQL Server 主機時啟用 HDFS 瀏覽體驗，必須為具有 bdcUser 角色的使用者授與 VIEW SERVER STATE 權限，因為 Azure Data Studio 會使用 `sys.dm_cluster_endpoints` DMV 取得所需的 Knox 閘道端點以連線到 HDFS。

  >[!IMPORTANT]
  >開始部署之前，請先在 AD 中建立這些群組。 若這些 AD 群組的範圍是網域本機，則部署會失敗。

  >[!IMPORTANT]
  >若網域使用者擁有大量的群組成員資格，則建議使用自訂的 *bdc.json* 部署組態檔來調整閘道設定 `httpserver.requestHeaderBuffer` 的值 (預設值為 `8192`)，以及 HDFS 設定 `hadoop.security.group.mapping.ldap.search.group.hierarchy.levels` (預設值為 `10`)。 這是避免連線閘道逾時，以及包含 431 (*要求標頭欄位過大*) 狀態代碼 HTTP 回應的最佳做法。 此為組態檔區段，其示範如何定義這些設定的值，以及更多群組成員資格的建議值：

```json
{
    ...
    "spec": {
        "resources": {
            ...
            "gateway": {
                "spec": {
                    "replicas": 1,
                    "endpoints": [{...}],
                    "settings": {
                        "gateway-site.gateway.httpserver.requestHeaderBuffer": "65536"
                    }
                }
            },
            ...
        },
        "services": {
            ...
            "hdfs": {
                "resources": [...],
                "settings": {
                  "core-site.hadoop.security.group.mapping.ldap.search.group.hierarchy.levels": "4"
                }
            },
            ...
        }
    }
}
```

  >[!IMPORTANT]
  >請先在 AD 中建立為以下設定提供的群組，再開始進行部署。 若這些 AD 群組的範圍是網域本機，則部署會失敗。

- `security.activeDirectory.appOwners`**選擇性參數**：AD 群組的清單，這些群組具備建立、刪除和執行任何應用程式的權限。 此清單可包含範圍為通用或全域群組的 AD 群組。 其不能是網域本機群組。

- `security.activeDirectory.appReaders`**選擇性參數**：AD 群組的清單，這些群組具備執行任何應用程式的權限。 此清單可包含範圍為通用或全域群組的 AD 群組。 其不能是網域本機群組。

下表顯示應用程式管理的授權模型：

|   授權的角色   |   azdata command   |
|----------------------|--------------------|
|   appOwner           | azdata app create  |
|   appOwner           | azdata app update  |
|   appOwner, appReader| azdata app list    |
|   appOwner, appReader| azdata app describe|
|   appOwner           | azdata app delete  |
|   appOwner, appReader| azdata app run     |

- `security.activeDirectory.subdomain`:**選擇性參數**：此參數是在 SQL Server 2019 CU5 版本中引進，以用來支援針對相同的網域部署多個巨量資料叢集。 使用這項設定即可為每一個部署的巨量資料叢集指定不同 DNS 名稱。 若未在 `control.json` 檔案的 Active Directory 區段中指定此參數的值，則將會使用巨量資料叢集名稱 (與 Kubernetes 命名空間名稱相同) 來計算子網域設定的值。 

  >[!NOTE]
  >透過子網域設定所傳遞不是新的 AD 網域，而只是 BDC 叢集於內部使用的 DNS 網域。

  >[!IMPORTANT]
  >您需要將 **azdata CLI** 升級到最新的 SQL Server 2019 CU5 版本才能利用這些新功能，並在相同的網域中部署多個巨量資料叢集。

  請參閱[概念：在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-deployment-background.md)，以取得與在相同 Active Directory 網域內部署多個巨量資料叢集相關的詳細資料。

- `security.activeDirectory.accountPrefix`:**選擇性參數**：此參數是在 SQL Server 2019 CU5 版本中引進，以用來支援針對相同的網域部署多個巨量資料叢集。 這項設定保證各種巨量資料叢集服務其帳戶名稱都是唯一的，而其在任意兩個叢集間都必須是不同的。 自訂帳戶前置名稱為選擇性，且根據預設會使用子網域名稱作為帳戶的前置詞。 若子網域名稱超過 12 個字元，則會使用子網域名稱的前 12 個字元作為帳戶的前置詞。  

  >[!NOTE]
  >Active Directory 要求帳戶名稱不得超過 20 個字元。 BDC 叢集必須使用 8 個字元區隔 Pod 與 StatefulSet。 這代表帳戶前置詞限制為 12 個字元

[檢查 AD 群組範圍](/powershell/module/addsadministration/get-adgroup)，以判斷該範圍是否為 DomainLocal。

如果您尚未初始化部署設定檔案，您可以執行此命令來取得設定的複本。 以下範例使用 `kubeadm-prod` 設定檔，但同樣適用於 `openshift-prod`。

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

若要在 `control.json` 檔案中設定上述參數，請使用下列 `azdata` 命令。 該命令會取代設定，並在部署之前提供您自己的值。

> [!IMPORTANT]
> 在 SQL Server 2019 CU2 版本中，部署設定檔案的安全性組態區段結構已略有變更，且所有 Active Directory 相關設定都位於 `control.json` 檔案其 `security` 下 JSON 樹狀目錄的新 `activeDirectory` 中。

>[!NOTE]
> 除了為本節中描述的子網域提供不同值之外，您也必須在相同 Kubernetes 叢集中部署多個 BDC 時針對 BDC 端點使用不同的連接埠號碼。 這些連接埠號碼可在部署時透過[部署組態](deployment-custom-configuration.md)設定檔設定。

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

僅限從 SQL Server 2019 CU5 版本開始，您也可以選擇覆寫 `subdomain` 和 `accountPrefix` 設定的預設值。

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.subdomain=[\"bdctest\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.accountPrefix=[\"bdctest\"]"
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

除了上述資訊之外，您還需要為不同叢集端點提供 DNS 名稱。 在部署時，系統會自動在您的 DNS 伺服器中建立使用所提供 DNS 名稱的 DNS 項目。 當您連線到不同叢集端點時，將會使用這些名稱。 例如，若 SQL 主要執行個體的 DNS 名稱是 `mastersql`，且考慮到子網域將會在 `control.json` 中使用叢集名稱的預設值，則可使用 `mastersql.contoso.local,31433` 或 `mastersql.mssql-cluster.contoso.local,31433` (取決於在部署組態檔中針對端點 DNS 名稱提供的值)，以從工具連線到主要執行個體。 

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

> [!IMPORTANT]
> 只要所選的端點 DNS 名稱是完整名稱，且不會和任意兩個在相同網域中部署的巨量資料叢集衝突，則可使用所選的端點 DNS 名稱。 您也可以選擇使用 `subdomain` 參數值來確保 DNS 名稱在不同叢集間都是不同的。 例如：

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.<subdomain e.g. mssql-cluster>.contoso.local"
```

您可以在這裡找到適用於[使用 AD 整合在單一節點 Kubernetes 叢集 (kubeadm) 上部署 SQL Server 巨量資料叢集](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad) \(英文\) 的範例指令碼。

> [!Note]
> 在某些情況下，您可能無法採用新引進的 `subdomain` 參數。 例如，您必須部署一個 CU5 之前的版本，且您已經升級了 **azdata CLI**。 雖然這不太可能，但是若需要還原到 CU5 之前的行為，可在 `control.json` 的 Active Directory 區段將 `useSubdomain` 參數設為 `false`。  執行這個動作的命令如下：

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false"
```

您現在應該已設定使用 Active Directory 整合進行 BDC 部署的所有必要參數。

您現在可以使用 `azdata` 命令和 kubeadm-prod 部署設定檔，部署與 Active Directory 整合的 BDC 叢集。 如需如何部署 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] 的完整文件，請瀏覽[如何在 Kubernetes 上部署 SQL Server 巨量資料叢集](deployment-guidance.md)。

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>確認網域控制站的反向 DNS 項目

請確定網域控制站本身的反向 DNS 項目 (PTR 記錄) 已在 DNS 伺服器中註冊。 您可以藉由在網域控制站上執行網域名稱的 `nslookup`，以確認它可以解析為網域控制站的 IP 位址。

## <a name="known-issues-and-limitations"></a>已知問題和限制

**SQL Server 2019 CU5 中要注意的限制**

- 目前，[記錄搜尋] 儀表板和 [計量] 儀表板不支援 AD 驗證。 在部署時設定的基本使用者名稱和密碼，可用來進行這些儀表板的驗證。 所有其他叢集端點都支援 AD 驗證。

- 安全 AD 模式目前只能在 `kubeadm` 和 `openshift` 部署環境上運作，而無法在 AKS 或 ARO 上運作。 根據預設，`kubeadm-prod` 和 `openshift-prod` 部署設定檔包含安全性區段。

- 在 SQL Server 2019 CU5 版本前，只允許每個網域 (Active Directory) 一個 BDC。 從 CU5 版本開始，您可在每個網域啟用多個 BDC。

- 安全性設定中指定的任何 AD 群組都不能設定 DomainLocal 範圍。 您可以遵循[這些指示](/powershell/module/addsadministration/get-adgroup)，以檢查 AD 群組的範圍。

- 可用來登入 BDC 的 AD 帳戶允許在為 BDC 設定的相同網域中使用。 不支援啟用來自其他受信任網域的登入。

## <a name="next-steps"></a>後續步驟

[連線 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]：Active Directory 模式](active-directory-connect.md)

[針對 SQL Server 巨量資料叢集 Active Directory 整合進行疑難排解](troubleshoot-active-directory.md)

[概念：在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-deployment-background.md)
