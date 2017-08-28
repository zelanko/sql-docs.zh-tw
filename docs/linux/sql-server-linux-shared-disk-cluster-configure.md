---
title: "設定 SQL Server on Linux 的共用的磁碟叢集 |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/23/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: b6e6cc415b01c6021a4ba7c52433543dc58a4452
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="shared-disk-cluster-for-sql-server-on-linux"></a>SQL Server on Linux 的共用磁碟叢集

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

您可以設定共用存放裝置的高可用性叢集以 Linux 為允許 SQL Server 執行個體容錯移轉到另一個節點。 在典型的叢集中兩個或多部伺服器會連接到共用存放裝置。 伺服器是叢集節點。 容錯移轉叢集提供改善為允許兩個或多個節點之間容錯移轉至 SQL Server 的復原時間的執行個體層級的保護。 設定步驟取決於 Linux 散發套件及叢集解決方案。 下表會識別特定步驟驗證的叢集解決方案。  

|Distribution |主題 
|----- |-----
|**Red Hat Enterprise Linux HA 的附加元件** |[設定](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[操作](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server 高可用性的附加元件** |[設定](sql-server-linux-shared-disk-cluster-sles-configure.md)

