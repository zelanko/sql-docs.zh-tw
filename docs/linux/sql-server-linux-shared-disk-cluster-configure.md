---
title: "設定 SQL Server on Linux 的共用的磁碟叢集 |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 92b4cb2500d4fd8a1643488593c40e97b1ff6454
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---

# <a name="shared-disk-cluster-for-sql-server-on-linux"></a>SQL Server on Linux 的共用磁碟叢集

您可以設定共用存放裝置的高可用性叢集以 Linux 為允許 SQL Server 執行個體容錯移轉到另一個節點。 在典型的叢集中兩個或多部伺服器會連接到共用存放裝置。 伺服器是叢集節點。 容錯移轉叢集提供改善為允許兩個或多個節點之間容錯移轉至 SQL Server 的復原時間的執行個體層級的保護。 設定步驟取決於 Linux 散發套件及叢集解決方案。 下表會識別特定步驟驗證的叢集解決方案。  

|Distribution |主題 
|----- |-----
|**Red Hat Enterprise Linux HA 的附加元件** |[設定](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[操作](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server 高可用性的附加元件** |[設定](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>後續的步驟


