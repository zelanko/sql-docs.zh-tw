---
title: 在 Active Directory 網域中部署多個叢集
titleSuffix: SQL Server Big Data Cluster
description: 了解如何在單一 Active Directory 網域中部署多個 SQL Server 巨量資料叢集。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 144b769ce42b192099678cda4cfe6fb2935c1c2f
ms.sourcegitcommit: af663bdca0df8a1f34a14667390662f6f0e17766
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/19/2020
ms.locfileid: "94924165"
---
# <a name="deploy-multiple-big-data-clusters-2019-in-the-same-active-directory-domain"></a>在相同的 Active Directory 網域中部署多個 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

此文章說明 SQL Server 2019 CU5 的更新，其可讓您部署多個 SQL Server 2019 巨量資料叢集，並與相同的 Active Directory 網域整合。

在 SQL 2019 CU5 之前，有兩個問題讓您無法在一個 AD 網域中部署多個 BDC。

- 服務主體名稱與 DNS 網域發生命名衝突
- 網域帳戶主體名稱

## <a name="object-name-collisions"></a>物件名稱衝突

### <a name="service-principal-names-spn-and-dns-domain-naming-conflict"></a>服務主體名稱 (SPN) 與 DNS 網域發生命名衝突

以部署階段提供的網域名稱作為 AD DNS 網域使用。 這表示 Pod 可以使用此 DNS 網域，在內部網路中彼此連線。 此外，使用者也可使用此 DNS 網域連線到 BDC 端點。 如此一來，針對 BDC 內之服務所建立的服務主體名稱 (SPN)，將會具有符合此 AD DNS 網域規定的 Kubernetes Pod、服務或端點名稱。 若使用者在網域中部署第二個叢集，因為這兩個叢集之間的 Pod 名稱與 DNS 網域名稱沒有差異，所以產生的 SPN 會有相同的 FQDN。 例如，假設 AD DNS 網域是 `contoso.local`。 Pod `master-0` 之主要集區 SQL Server 所產生的其中一個 SPN 會是 `MSSQLSvc/master-0.contoso.local:1433`。 在使用者嘗試部署的第二個叢集中，只要 `master-0` 的 Pod 名稱相同，而使用者也將提供相同的 AD DNS 網域 (``contoso.local``，就會產生相同的 SPN 字串。 Active Directory 會禁止在第二個叢集中建立導致部署失敗的衝突 SPN。

### <a name="domain-account-principal-names"></a>網域帳戶主體名稱

在部署網域為 Active Directory 的 BDC 期間，在 BDC 內執行的服務會產生多個帳戶主體。 這些基本上都是 AD 使用者帳戶。 在 SQL 2019 CU5 之前，這些帳戶的名稱在叢集之間都不是唯一的。 此資訊清單會嘗試在兩個不同的叢集中，為 BDC 的特定服務建立相同的使用者帳戶名稱。 第二個部署的叢集會在 AD 中發生衝突，無法建立其帳戶。

## <a name="resolution-for-collisions"></a>衝突的解決方式

### <a name="solution-to-solve-the-problem-with-spns-and-dns-domain---sql-2019-cu5"></a>解決 SPN 與 DNS 網域問題的解決方案 - SQL 2019 CU5

由於任兩個叢集中的 SPN 必須不同，所以在部署階段傳入的 DNS 網域名稱也必須不同。 您可以使用部署組態檔新引入的設定，指定不同的 DNS 名稱：`subdomain`。 若兩個叢集之間的子網域不同，而且內部通訊可能會透過這個子網域進行，則 SPN 將會包含達到所需唯一性的子網域。

>[!NOTE]
>透過子網域設定所傳遞的值不是新的 AD 網域，而是內部使用的 DNS 網域。

再以主要集區 SQL Server SPN 為例說明。 若子網域是 `bdc`，則先前討論的 SPN 會變更為 `MSSQLSvc/master-0.bdc.contoso.local:1433`。  

您可選擇是否在 Active Directory 組態規格中，自訂新引入的子網域參數值。 根據預設，BDC 叢集名稱或命名空間名稱將用來計算子網域設定的值。 當使用者想要覆寫子網域名稱時，可以使用在 Active Directory 組態規格中引入的新子網域參數來執行此動作。

### <a name="solution-to-solve-the-problem-regarding-account-names-uniqueness"></a>解決帳戶名稱唯一性相關問題的解決方案

為了將帳戶名稱更新為保證唯一性的配置，我們引入了帳戶首碼的概念。 帳戶首碼是帳戶名稱的一部分，在任兩個叢集之間都是唯一的。 帳戶名稱的其餘部分是給定之服務的常數。 帳戶名稱的新格式看起來會像 `<prefix>-<name>-<podId>`。 

>[!NOTE]
>Active Directory 要求帳戶名稱不得超過 20 個字元。 BDC 叢集必須使用 8 個字元區隔 Pod 與 StatefulSet。 所以只有 12 個字元可供帳戶首碼使用

自訂帳戶名稱是選擇性的。 使用 Active Directory 組態規格中的 `accountPrefix` 參數。SQL Server 2019 CU5 在組態規格中引入了 `accountPrefix`。根據預設，子網域名稱可作為帳戶首碼使用。 若子網域名稱超過 12 個字元，則會使用子網域名稱的前 12 個字元的子字串作為帳戶首碼。

子網域只適用於 DNS。 因此，新的 LDAP 使用者帳戶名稱是 `bdc-ldap@contoso.local`。 帳戶名稱不會是 `bdc-ldap@bdc.contoso.local`。

## <a name="semantics"></a>語意

總而言之，這些都是 SQL 2019 CU5 中為網域的多個叢集所新增的參數語意：

### `subdomain`

- 選擇性欄位
- 資料類型：字串
- 定義：要用於此 BDC 叢集的唯一 DNS 子網域。 部署在 Active Directory 網域中的每個叢集，此值都應該不同。  
- 預設值：若未提供，將會使用叢集名稱作為預設值
- 最大長度：每個標籤為 63 個字元 (標籤中的每個字串以點分隔)。
- 備註：端點 DNS 名稱應該使用 FQDN 中的子網域。

### `accountPrefix`

- 選擇性欄位
- 資料類型：字串
- 定義：BDC 叢集將產生 AD 帳戶的唯一首碼。 部署在 Active Directory 網域中的每個叢集，此值都應該不同。
- 預設值：若未提供，將會使用子網域名稱作為預設值。 若未提供子網域，將會使用叢集名稱作為子網域名稱，因此叢集名稱也會繼承為 accountPrefix。 若有提供子網域，而且是多部分名稱 (包含一或多個點)，則使用者必須提供 accountPrefix。 
- 最大長度：12 個字元 

## <a name="impact-on-ad-domain-and-dns-server"></a>對 AD 網域與 DNS 伺服器的影響 

AD 網域或網域控制站無須進行任何變更，即可在相同的 Active Directory 網域中部署多個 BDC。 當註冊外部端點 DNS 名稱時，系統會自動在 DNS 伺服器中建立 DNS 子網域。 

## <a name="impact-on-setting-up-the-deployment-configuration-file-used-for-the-bdc-deployment"></a>對設定用於 BDC 部署之部署組態檔的影響 

控制平面組態 *control.json* 中的 *activeDirectory* 區段，將有兩個新的選擇性參數：`subdomain` 與 `accountPrefix`。 只有想要覆寫預設行為時，才提供這些設定的值，也就是每個叢集使用各自的叢集名稱。 叢集名稱與命名空間名稱相同。

此外，只要所選的端點 DNS 名稱是完整名稱，且在部署於相同網域中的任兩個巨量資料叢集間不會發生衝突，就可以使用。 您也可以選擇使用子網域參數值，確保 DNS 名稱在不同叢集間都是不同的。  例如，請考慮閘道端點。 若您想要使用 `gateway` 作為端點的名稱，並在 BDC 部署期間自動在 DNS 伺服器中註冊，請使用 `gateway.bdc1.contoso.local` 作為 DNS 名稱。 若 `bdc1` 是子網域，且 `contoso.local` 是 AD DNS 網域名稱， 則其他可接受的值為：`gateway-bdc1.contoso.local`，或僅為 `gateway.contoso.local`。

## <a name="examples"></a>範例

若您想要覆寫子網域與 accountPrefix，以下是 Active Directory 安全性組態的範例。 

```json
    "security": { 
        "activeDirectory": { 
            "ouDistinguishedName":"OU=contosoou,DC=contoso,DC=local", 
            "dnsIpAddresses": [ "10.10.10.10" ], 
            "domainControllerFullyQualifiedDns": [ "contoso-win2016-dc.contoso.local" ], 
            "domainDnsName":"contoso.local", 
            "subdomain": "bdc", 
            "accountPrefix": "myprefix", 
            "clusterAdmins": [ "contosoadmins" ], 
            "clusterUsers": [ "contosousers1", "contosousers2" ] 
        } 
    } 
  
```

以下是控制平面端點的端點規格範例。 只要 DNS 名稱是唯一且完整的名稱，您就可以使用任何 DNS 名稱的值：
  
```json
        "endpoints": [ 
            { 
                "serviceType": "NodePort", 
                "port": 30080, 
                "name": "Controller", 
                "dnsName": "control-bdc1.contoso.local" 
            }, 
            { 
                "serviceType": "NodePort", 
                "port": 30777, 
                "name": "ServiceProxy", 
                "dnsName": "monitor-bdc1.contoso.local" 
            } 
        ] 
  
```

## <a name="questions"></a>問題

### <a name="do-you-need-to-create-separate-ous-for-different-clusters"></a>您需要為不同的叢集建立個別的 OU 嗎？

這並非必要，但是建議使用。 為個別叢集提供個別的 OU，可協助您管理所產生的使用者帳戶。

### <a name="how-to-revert-back-to-the-pre-cu5-behavior-in-sql-2019"></a>如何在 SQL 2019 中還原回 CU5 之前的行為？

在某些情況下，您可能無法容納新引入的 `subdomain` 參數。 例如，您必須部署 CU5 之前的版本，但您已經升級了 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]。 雖然這不太可能，但是若必須還原到 CU5 之前的行為，可在 `control.json` 的 Active Directory 區段中，將 `useSubdomain` 參數設為 `false`。

針對這種情況，下列範例將 `useSubdomain` 設定為 `false`。

```console
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false" 
```

## <a name="next-steps"></a>後續步驟

[針對 SQL Server 巨量資料叢集 Active Directory 整合進行疑難排解](troubleshoot-active-directory.md)
