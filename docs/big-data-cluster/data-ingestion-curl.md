---
title: 使用 curl 將資料載入 SQL Server 2019 CTP 2.0 上的 HDFS |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 05ce2d4d848b7c244d672f6ab43cbcf09224e63f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48796176"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-2019-ctp-20"></a>使用 curl 將資料載入 SQL Server 2019 CTP 2.0 上的 HDFS

這篇文章說明如何使用**curl**將資料載入 SQL Server 2019 CTP 2.0 上的 HDFS。

## <a name="obtain-the-service-external-ip"></a>取得服務的外部 IP

當部署完成之後，且其存取權會經歷 Knox 時，會啟動 WebHDFS。 Knox 端點會公開透過 Kubernetes 服務 （適用於目前） 呼叫**服務-安全性-l b**。若要建立 WebHDFS URL，您必須使用 CURL 上傳/下載檔案，您必須將**服務-安全性-l b**服務外部 IP 位址和您的叢集名稱。 您可以執行此命令，以取得服務-安全性-l b 服務外部 IP 位址：

```bash
kubectl get service service-security-lb -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> `<cluster name>`以下是您提供執行 mssqlctl 時叢集的名稱建立叢集`<cluster name>`。

## <a name="construct-the-url-to-access-webhdfs"></a>建構的 URL 來存取 WebHDFS

現在，您可以建構 URL 才能存取 WebHDFS，如下所示：

`https://<service-security-lb service external IP address>:30433/gateway/default/webhdfs/v1/`

例如：

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>列出檔案

清單下的檔案**hdfs: / / airlinedata**使用下列 curl 命令：

```bash
curl -i -k -u root:root-password -X GET 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>將本機檔案放到 HDFS

若要將新的檔案**test.csv** airlinedata 目錄的本機目錄中 (**Content-type**是必要參數) 使用下列 curl 命令：

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>建立目錄

若要建立目錄**測試**下方`hdfs:///`使用下列命令：

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 的巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 的巨量資料叢集？](big-data-cluster-overview.md)。