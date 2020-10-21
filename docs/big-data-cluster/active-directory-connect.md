---
title: 在 Active Directory 模式中連線
titleSuffix: SQL Server Big Data Cluster
description: 了解如何連線到 Active Directory 網域中的 SQL Server 巨量資料叢集。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bd8da3642d0a650ea10c54b7ed8e46a54fba2971
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91898676"
---
# <a name="connect-big-data-clusters-2019-active-directory-mode"></a>連線 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]：Active Directory 模式

本文描述如何連線到在 Active Directory 模式中部署的 SQL Server 巨量資料叢集端點。 本文中的工作需要您具有在 Active Directory 模式中部署的 SQL Server 巨量資料叢集。 如果您沒有叢集，請參閱[在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-deploy.md)。

## <a name="overview"></a>概觀

使用 AD 驗證登入 SQL Server 主要執行個體。

若要確認對 SQL Server 執行個體的 AD 連線，請使用 `sqlcmd`連線到 SQL 主要執行個體。 在部署時，系統會為提供的群組自動建立登入 (`clusterUsers` 和 `clusterAdmins`)。

如果您使用 Linux，請先以 AD 使用者的身分執行 `kinit`，然後執行 `sqlcmd`。 如果您使用 Windows，只要以所需的使用者身分，從**已加入網域的用戶端機器**登入即可。

## <a name="connect-to-master-instance-from-linuxmac"></a>從 Linux/Mac 連線到主要執行個體

```bash
kinit <username>@<domain name>
sqlcmd -S <DNS name for master instance>,31433 -E
```

## <a name="connect-to-master-instance-from-windows"></a>從 Windows 連線到主要執行個體

```cmd
sqlcmd -S <DNS name for master instance>,31433 -E
```

## <a name="log-in-to-sql-server-master-instance-using-azure-data-studio-or-ssms"></a>使用 Azure Data Studio 或 SSMS 登入 SQL Server 主要執行個體

從已加入網域的用戶端，您可以開啟 SSMS 或 Azure Data Studio 並連線到主要執行個體。 這與使用 AD 驗證連線到任何 SQL Server 執行個體的體驗相同。

從 SSMS：

![SSMS 中的 [連線至 SQL Server] 對話方塊](./media/deploy-active-directory/image23.png)

從 Azure Data Studio：

![Azure Data Studio 中的 [連線至 SQL Server] 對話方塊](./media/deploy-active-directory/image24.png)}

## <a name="log-in-to-controller-with-ad-authentication"></a>使用 AD 驗證來登入控制器

### <a name="connect-to-controller-with-ad-authentication-from-linuxmac"></a>從 Linux/Mac 使用 AD 驗證連線到控制器

您可透過兩個選項以使用 `azdata` 和 AD 驗證來連線到控制器端點。 您可使用 *--endpoint/-e* 參數：

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
```

或者，您可使用 *--namespace/-n* 參數進行連線，此為巨量叢集名稱：

```bash
kinit <username>@<domain name>
azdata login -n <clusterName> --auth ad
```

### <a name="connect-to-controller-with-ad-authentication-from-windows"></a>從 Windows 使用 AD 驗證連線到控制器

```cmd
azdata login -e https://<controller DNS name>:30080 --auth ad
```

## <a name="use-ad-authentication-to-knox-gateway-webhdfs"></a>將 AD 驗證用於 Knox 閘道 (webHDFS)

您也可以透過 Knox 閘道端點，使用 curl 發出 HDFS 命令。 這需要對 Knox 進行 AD 驗證。 以下 curl 的命令會透過 Knox 閘道發出 webHDFS REST 呼叫，以建立稱為 `products` 的目錄

```bash
curl -k -v --negotiate -u : https://<Gateway DNS name>:30443/gateway/default/webhdfs/v1/products?op=MKDIRS -X PUT
```

## <a name="next-steps"></a>後續步驟

[針對 SQL Server 巨量資料叢集 Active Directory 整合進行疑難排解](troubleshoot-active-directory.md)

[概念：在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-deployment-background.md)
