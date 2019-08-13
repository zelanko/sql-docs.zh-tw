---
title: 使用 curl 將資料載入 HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: 使用 curl 將資料載入 SQL Server 2019 巨量資料叢集上的 HDFS。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aae991c6dfdade4145f1e5578273e3b6aeb83299
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958636"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-big-data-clusters"></a>使用 curl 將資料載入 SQL Server 巨量資料叢集上的 HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用 **curl** 將資料載入 SQL Server 2019 巨量資料叢集 (預覽) 上的 HDFS。

## <a name="obtain-the-service-external-ip"></a>取得服務外部 IP

當部署完成時會啟動 WebHDFS，並透過 Knox 進行存取。 Knox 端點是透過名為 **gateway-svc-external** 的 Kubernetes 服務公開。  若要建立必要的 WebHDFS URL 來上傳/下載檔案，您需要 **gateway-svc-external** 服務外部 IP 位址和巨量資料叢集的名稱。 您可以執行下列命令，取得 **gateway-svc-external** 服務外部 IP 位址：

```bash
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> 這裡的 `<big data cluster name>` 是您在部署組態檔中指定的叢集名稱。 預設名稱為 `mssql-cluster`。

## <a name="construct-the-url-to-access-webhdfs"></a>建構 URL 來存取 WebHDFS

現在，您可以建構 URL 來存取 WebHDFS，如下所示：

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

例如：

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>列出檔案

若要列出 **hdfs:///airlinedata** 下的檔案，請使用下列 curl 命令：

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>將本機檔案放入 HDFS

若要將新的 **test.csv** 檔案從本機目錄放到 airlinedata 目錄，請使用下列 curl 命令 (**Content-Type** 參數是必要的)：

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>建立目錄

若要在 `hdfs:///` 下建立目錄 **test**，請使用下列命令：

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>後續步驟

如需 SQL Server 巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 巨量資料叢集](big-data-cluster-overview.md)。
