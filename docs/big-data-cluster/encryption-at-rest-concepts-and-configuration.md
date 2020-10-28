---
title: 待用加密
titleSuffix: SQL Server Big Data Clusters
description: 了解 SQL Server 2019 巨量資料叢集上的待用加密。
author: dacoelho
ms.author: dacoelho
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/19/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: de0bc20d7551e8d42c5dc1463fada6ffcbb6a0fd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257148"
---
# <a name="encryption-at-rest-concepts-and-configuration-guide"></a>待用加密概念和設定指南

從 SQL Server 巨量資料叢集 CU8 開始，您可以使用完整的待用加密功能集，向儲存在平台中的所有資料提供應用程式層級加密。 本指南記載 SQL Server 巨量資料叢集待用加密功能集的概念、架構和設定。

SQL Server 巨量資料叢集會將資料儲存在下列兩個位置：

* __SQL Server__ 主要執行個體
* 存放集區和 Spark 使用的 __HDFS__ 。

為了能夠以透明的方式加密 SQL Server 巨量資料叢集中的資料，可行的方法有兩種：

* __磁碟區加密__ 。 這種方法會由 Kubernetes 平台提供支援，而且應該是巨量資料叢集部署的最佳做法。 本指南未涵蓋磁碟區加密。 請參閱您的 Kubernetes 平台或設備文件，以取得如何為將用於 SQL Server 巨量資料叢集的磁碟區正確加密的指南。
* __應用程式層級加密__ 。 此架構是指先由處理資料的應用程式加密資料，再將資料寫入到磁碟中。 如果將磁碟區公開，除非目的地系統也設定了相同的加密金鑰，否則攻擊者將無法在別處還原資料成品。 

SQL Server 巨量資料叢集的待用加密功能集可支援 SQL Server 和 HDFS 元件應用程式層級加密的核心案例。

其會提供下列功能：

* __系統管理的待用加密__ 。 這項功能可在 CU8 中使用。
* __使用者管理的待用加密 (BYOK)__ ，同時包含服務管理和外部金鑰提供者整合。 目前僅支援服務管理的使用者建立金鑰。

## <a name="key-definitions"></a>關鍵定義

### <a name="sql-server-big-data-clusters-key-management-service-kms"></a>SQL Server 巨量資料叢集金鑰管理服務 (KMS)

控制器裝載的服務，負責管理 SQL Server BDC 叢集待用加密功能集的金鑰和憑證。 這項服務支援下列功能：

* 安全地管理和儲存用於待用加密的金鑰和憑證。
* Hadoop KMS 相容性。 其可作為 BDC 上 HDFS 元件的金鑰管理服務。
* SQL Server TDE 憑證管理。

目前不支援下列功能：
* *金鑰版本設定支援* 。 

在本文件的其餘部分，我們會將這項服務稱為 __BDC KMS__ 。 此外，也會使用 __BDC__ 一詞來指稱 __SQL Server 巨量資料叢集__ 計算平台。

### <a name="system-managed-keys-and-certificates"></a>系統管理的金鑰和憑證

BDC KMS 服務會管理 SQL Server 和 HDFS 的所有金鑰和憑證。

### <a name="user-provided-certificates"></a>使用者提供的憑證

要由 BDC KMS 管理、使用者所提供的金鑰和憑證，通常稱為攜帶您自己的金鑰 (BYOK)。

### <a name="external-providers"></a>外部提供者

與用於外部委派的 BDC KMS 相容的外部金鑰解決方案。 目前不支援這項功能。

## <a name="encryption-at-rest-on-sql-server-big-data-clusters-cu8"></a>SQL Server 巨量資料叢集 CU8 上的待用加密

SQL Server 巨量資料叢集 CU8 是待用加密功能集的初始版本。 請仔細閱讀本文件，以完整評估您的案例。

此功能集引進了 __BDC KMS 控制器服務__ ，以便為 SQL Server 和 HDFS 上的待用資料加密提供系統管理的金鑰和憑證。 這些金鑰和憑證會由服務來管理，本文件會提供有關如何與服務互動的操作指引。

* __SQL Server__ 執行個體會利用著名的[透明資料加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md) 功能。
* __HDFS__ 會使用每個 Pod 內的原生 Hadoop KMS 來與控制器上的 BDC KMS 互動。 這會啟用 HDFS 加密區域，以在 HDFS 上提供安全的路徑。

### <a name="sql-server-instances"></a>SQL Server 執行個體

* 系統產生的憑證會安裝在要與 TDE 命令搭配使用的 SQL Server Pod 上。 系統管理憑證的命名標準是 `TDECertificate` + `timestamp`。 例如： `TDECertificate2020_09_15_22_46_27`。
* 系統不會自動加密主要執行個體 BDC 所佈建的資料庫和使用者資料庫。 DBA 可使用已安裝的憑證來加密任何資料庫。
* 系統會使用系統產生的憑證來自動加密計算集區和存放集區。
* 雖然在技術上可使用 T-SQL `EXECUTE AT` 命令，但不建議這麼做，而且目前也不支援資料集區加密。 使用這項技術來加密資料集區資料庫可能不會生效，而且加密可能不會在所需的狀態下發生。 其也會建立朝向後續版本的不相容升級路徑。
* 目前不會輪替憑證。 支援先解密再使用 T-SQL 命令以新憑證進行加密 (如果不在 HA 部署上)。
* 加密監視會透過現有適用於 TDE 的標準 SQL Server DMV 來進行。
* 支援將已啟用 TDE 的資料庫備份並還原到叢集。
* 支援 HA。 如果將 SQL Server 主要執行個體上的資料庫加密，則資料庫的所有次要複本也會一併加密。

### <a name="hdfs-encryption-zones"></a>HDFS 加密區域

* 需要 [Active Directory 整合](active-directory-prerequisites.md)才能啟用 HDFS 的加密區域功能。
* 系統產生的金鑰將會佈建在 Hadoop KMS 中。 金鑰名稱為 `securelakekey`。 在 CU8 上，預設金鑰為 256 位元，而且我們支援 256 位元的 AES 加密。
* 預設的加密區域將會使用上述系統產生的金鑰佈建在名為 `/securelake` 的路徑上。
* 使用者可以使用本指南中提供的特定指示來建立其他金鑰和加密區域。 使用者將能夠在金鑰建立期間選擇 128、192 或 256 的金鑰大小。
* 在 CU8 中無法進行 HDFS 的就地金鑰輪替。 替代方法是使用 distcp 將資料從一個加密區域移至另一個。
* 不支援在加密區域之上執行 HDFS 階層處理掛接。

## <a name="configuration-guide"></a>設定指南

SQL Server 巨量資料叢集待用加密是服務管理的功能，而且根據您的部署路徑，可能需要執行額外的步驟。

在 CU8 後，於 __新部署 SQL Server 巨量資料叢集時__ ， __預設會啟用並設定待用加密__ 。 這表示：

* BDC KMS 元件將會部署在控制器中，並會產生一組預設的金鑰和憑證。
* SQL Server 將會在開啟 TDE 的情況下進行部署，且憑證會由控制器加以安裝。
* Hadoop KMS (適用於 HDFS) 將會設定為與 BDC KMS 互動以進行加密作業。 HDFS 加密區域已設定完成並可供使用。

適用上一節所述的需求和預設行為。

如果 __將叢集升級為 CU8__ ， __請仔細閱讀下一節__ 。

### <a name="upgrading-to-cu8"></a>升級至 CU8

   > [!CAUTION]
   > 在升級至 SQL Server 巨量資料叢集之前，CU8 會執行完整的資料備份。

在現有叢集上，升級流程不會對使用者資料強制執行加密，也不會設定 HDFS 加密區域。 此行為是設計所致，而且需要針對每個元件考慮下列各項：

* __SQL Server__

    1. __SQL Server 主要執行個體__ 。 升級流程不會影響任何主要執行個體資料庫和已安裝的 TDE 憑證，但強烈建議您先備份資料庫和手動安裝的 TDE 憑證，再進行升級流程。 也建議您將這些成品儲存在 SQL Server BDC 叢集之外。
    1. __計算和存放集區__ 。 這些資料庫由系統管理、會變動，而且會在升級叢集時重新建立並自動加密。
    1. __資料集區__ 。 升級不會影響資料集區的 SQL Server 執行個體這個部分中的資料庫。

* __HDFS__

    1. __HDFS__ 。 升級流程不會觸碰加密區域之外的 HDFS 檔案和資料夾。
    1. __不會設定加密區域__ 。 Hadoop KMS 元件不會設定為使用 BDC KMS。 若要在升級後設定並啟用 HDFS 加密區域功能，請遵循下一節。

### <a name="enable-hdfs-encryption-zones-after-upgrade"></a>在升級後啟用 HDFS 加密區域

如果您將叢集升級為 CU8 (`azdata upgrade`)，並想要啟用 HDFS 加密區域，請執行下列動作。

需求：

- [Active Directory](active-directory-prerequisites.md) 整合式叢集。

- [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 會以 AD 模式進行設定並登入叢集。

請遵循下列程序來重新設定具有加密區域支援的叢集。

1. 使用 `azdata` 執行升級之後，請儲存下列指令碼。

    指令碼執行需求：
        
    * 這兩個指令碼應該位於相同的目錄。 
    * `PATH 上的 `kubectl`
    * ```$HOME/.kube``` 資料夾中 Kubernetes 的 ```config``` 檔案
    
    此指令碼應該命名為 __```run-key-provider-patch.sh```__ ：

    ```console
    #!/bin/bash
    
    if [[ -z "${BDC_DOMAIN}" ]]; then
      echo "BDC_DOMAIN environment variable with the domain name of the cluster is not defined."
      exit 1
    fi
    
    if [[ -z "${BDC_CLUSTER_NS}" ]]; then
      echo "BDC_CLUSTER_NS environment variable with the cluster namespace is not defined."
      exit 1
    fi
    
    kubectl get configmaps -n test
    
    diff <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py) <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | python -m json.tool)
    
    diff <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py) <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | python -m json.tool)
    
    # Replace the config maps.
    #
    kubectl replace -n $BDC_CLUSTER_NS -o json -f <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py)
    
    kubectl replace -n $BDC_CLUSTER_NS -o json -f <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py)
    
    # Restart the pods which need to have the necessary changes with the core-site.xml
    kubectl delete pods -n $BDC_CLUSTER_NS nmnode-0-0
    kubectl delete pods -n $BDC_CLUSTER_NS storage-0-0
    kubectl delete pods -n $BDC_CLUSTER_NS storage-0-1
    
    # Wait for sometime for pods to restart
    #
    sleep 300
    
    # Check for the KMS process status.
    #
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop nmnode-0-0 -- bash -c 'ps aux | grep kms'
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop storage-0-0 -- bash -c 'ps aux | grep kms'
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop storage-0-1 -- bash -c 'ps aux | grep kms'
    ```

    此指令碼應該命名為 __```updatekeyprovider.py```__ ：

    ```python
    #!/usr/bin/env python3
    
    import json
    import re
    import sys
    import xml.etree.ElementTree as ET
    import os
    
    class CommentedTreeBuilder(ET.TreeBuilder):
        def comment(self, data):
            self.start(ET.Comment, {})
            self.data(data)
            self.end(ET.Comment)
    
    domain_name = os.environ['BDC_DOMAIN']
    
    parser = ET.XMLParser(target=CommentedTreeBuilder())
    
    core_site = 'core-site.xml'
    j = json.load(sys.stdin)
    cs = j['data'][core_site]
    csxml = ET.fromstring(cs, parser=parser)
    props = [prop.find('value').text for prop in csxml.findall(
        "./property/name/..[name='hadoop.security.key.provider.path']")]
    
    kms_provider_path=''
    
    for x in range(5):
        if len(kms_provider_path) != 0:
            kms_provider_path = kms_provider_path + ';'
        kms_provider_path = kms_provider_path + 'nmnode-0-0.' + domain_name
    
    if len(props) == 0:
        prop = ET.SubElement(csxml, 'property')
        name = ET.SubElement(prop, 'name')
        name.text = 'hadoop.security.key.provider.path'
        value = ET.SubElement(prop, 'value')
        value.text = 'kms://https@' + kms_provider_path + ':9600/kms'
        cs = ET.tostring(csxml, encoding='utf-8').decode('utf-8')
    
    j['data'][core_site] = cs
    
    kms_site = 'kms-site.xml.tmpl'
    ks = j['data'][kms_site]
    
    kp_uri_regex = re.compile('(<name>hadoop.kms.key.provider.uri</name>\s*<value>\s*)(.*)(\s*</value>)', re.MULTILINE)
    
    def replace_uri(match_obj):
        key_provider_uri = 'bdc://https@hdfsvault-svc.' + domain_name
        if match_obj.group(2) == 'jceks://file@/var/run/secrets/keystores/kms/kms.jceks' or match_obj.group(2) == key_provider_uri:
            return match_obj.group(1) + key_provider_uri + match_obj.group(3)
        return match_obj.group(0)
    
    ks = kp_uri_regex.sub(replace_uri, ks)
    
    j['data'][kms_site] = ks
    print(json.dumps(j, indent=4, sort_keys=True))
    ```

    使用適當參數執行 __```run-key-provider-patch.sh```__ 。 

## <a name="next-steps"></a>後續步驟

若要深入了解如何有效使用待用加密 SQL Server 巨量資料叢集，請參閱下列文章：

- [待用加密 - SQL Server TDE](encryption-at-rest-sql-server-tde.md)
- [待用加密 - HDFS 加密區域](encryption-at-rest-hdfs-encryption-zones.md)

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列概觀：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
