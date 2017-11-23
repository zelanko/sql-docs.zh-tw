---
title: "備份及載入 AP PDW 硬體概觀"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "若要部署您端對端的資料倉儲方案 Analytics Platform System (AP) 與 SQL Server Parallel Data Warehouse (PDW)，您需要建立計畫來備份資料倉儲及載入資料。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 3a2ae046-f8d8-4a5c-b3c1-6ecee005df6c
caps.latest.revision: "9"
ms.openlocfilehash: 0bdf529aacf1644f55cd44da3d0a7590e509a323
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="backup-and-loading-hardware-overview"></a>備份及載入硬體概觀
若要部署您端對端的資料倉儲方案 Analytics Platform System (AP) 與 SQL Server Parallel Data Warehouse (PDW)，您需要建立計畫來備份資料倉儲及載入資料。 您可以使用該指引來取得和設定備份及載入的伺服器，以滿足您的業務需求。  
  
## <a name="acquire-and-configure-backup-servers"></a>取得和設定備份伺服器  
![備份程序](media/backup-process.png "備份程序")  
  
若要備份的 PDW 資料庫，您需要一或多個備份的伺服器。 您可以使用現有的硬體或購買新硬體。 如需詳細資訊，請參閱[取得和設定備份伺服器](acquire-and-configure-backup-server.md)。 這些指示包含[備份伺服器容量規劃工作表](backup-capacity-planning-worksheet.md)可協助您規劃備份解決方案。  
  
## <a name="acquire-and-configure-loading-servers"></a>取得和設定載入伺服器  
![載入處理序](media/loading-process.png "載入程序")  
  
若要載入資料，您需要一或多個載入伺服器。 您可以使用您自己現有的 ETL 或其他伺服器，或者，您可以購買新的伺服器。 如需詳細資訊，請參閱[取得和設定來載入伺服器](acquire-and-configure-loading-server.md)。 這些指示包含[載入伺服器容量規劃工作表](loading-server-capacity-planning-worksheet.md)可協助您規劃載入正確的方案。  
  
## <a name="see-also"></a>請參閱＜  
[備份和還原的概觀](backup-and-restore-overview.md)  
[負載概觀](load-overview.md)  
  
