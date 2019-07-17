---
title: 備份及載入硬體-平行處理資料倉儲
description: 若要部署您的端對端資料倉儲解決方案 Analytics Platform System (APS) Parallel Data Warehouse (PDW)，您需要建立備份資料倉儲和載入資料的計劃。 您可以使用本指引來取得和設定將符合您的業務需求的備份及載入伺服器。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 90f142a8bb86f99ed5cf5d9ff926bdf849060324
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961410"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>備份及載入硬體概觀-平行處理資料倉儲
若要部署您的端對端資料倉儲解決方案 Analytics Platform System (APS) Parallel Data Warehouse (PDW)，您需要建立備份資料倉儲和載入資料的計劃。 您可以使用本指引來取得和設定將符合您的業務需求的備份及載入伺服器。  
  
## <a name="acquire-and-configure-backup-servers"></a>取得並設定備份伺服器  
![備份程序](media/backup-process.png "備份程序")  
  
若要備份的 PDW 資料庫，您會需要一或多個備份的伺服器。 您可以使用現有的硬體，或購買新硬體。 如需詳細資訊，請參閱 <<c0> [ 取得並設定備份伺服器](acquire-and-configure-backup-server.md)。 這些指示包含[備份伺服器容量規劃工作表](backup-capacity-planning-worksheet.md)可協助您規劃備份適合的解決方案。  
  
## <a name="acquire-and-configure-loading-servers"></a>取得並設定載入伺服器  
![載入程序](media/loading-process.png "載入程序")  
  
若要載入資料，您需要一或多個載入伺服器。 您可以使用您自己現有的 ETL 或其他伺服器，或您可以購買新的伺服器。 如需詳細資訊，請參閱 <<c0> [ 取得並設定載入伺服器](acquire-and-configure-loading-server.md)。 這些指示包含[載入伺服器容量規劃工作表](loading-server-capacity-planning-worksheet.md)可協助您規劃載入適合的解決方案。  
  
## <a name="see-also"></a>另請參閱  
[備份與還原概觀](backup-and-restore-overview.md)  
[載入概觀](load-overview.md)  
  
