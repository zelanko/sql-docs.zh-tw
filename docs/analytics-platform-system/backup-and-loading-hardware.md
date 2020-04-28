---
title: 備份 & 載入硬體
description: 若要在具有平行處理資料倉儲（PDW）的分析平臺系統（AP）上部署端對端資料倉儲解決方案，您必須建立備份資料倉儲和載入資料的計畫。 使用本指南來取得並設定備份和載入伺服器，以符合您的商務需求。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4dd4fba91b1507f711a66a88f40b2fa2ea35e1ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401364"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>備份和載入硬體總覽-平行處理資料倉儲
若要在具有平行處理資料倉儲（PDW）的分析平臺系統（AP）上部署端對端資料倉儲解決方案，您必須建立備份資料倉儲和載入資料的計畫。 使用本指南來取得並設定備份和載入伺服器，以符合您的商務需求。  
  
## <a name="acquire-and-configure-backup-servers"></a>取得並設定備份伺服器  
![備份程序](media/backup-process.png "備份程序")  
  
若要備份 PDW 資料庫，您需要一或多部備份伺服器。 您可以使用自己現有的硬體，或購買新的硬體。 如需詳細資訊，請參閱[取得和設定備份伺服器](acquire-and-configure-backup-server.md)。 這些指示包含[備份伺服器容量規劃工作表](backup-capacity-planning-worksheet.md)，可協助您規劃適當的備份解決方案。  
  
## <a name="acquire-and-configure-loading-servers"></a>取得和設定載入伺服器  
![正在載入進程](media/loading-process.png "載入處理序")  
  
若要載入資料，您需要一或多個載入伺服器。 您可以使用您自己現有的 ETL 或其他伺服器，也可以購買新的伺服器。 如需詳細資訊，請參閱[取得和設定載入伺服器](acquire-and-configure-loading-server.md)。 這些指示包括 [[載入伺服器容量規劃] 工作表](loading-server-capacity-planning-worksheet.md)，可協助您規劃適當的載入解決方案。  
  
## <a name="see-also"></a>另請參閱  
[備份與還原總覽](backup-and-restore-overview.md)  
[負載總覽](load-overview.md)  
  
