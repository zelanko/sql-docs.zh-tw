---
title: 設定資料庫引擎執行個體 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 61c4482299d8e6fa9c70353eb80be5feaf5b9662
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799453"
---
# <a name="configure-database-engine-instances-sql-server"></a>設定 Database Engine 執行個體 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  每個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體都必須設定成符合針對執行個體所裝載之資料庫定義的效能和可用性需求。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 包含的組態選項可控制如資源使用狀況等行為，或是如稽核或觸發程序遞迴等功能的可用性。  
  
## <a name="instance-configuration"></a>執行個體組態  
 將資料庫部署至實際執行環境時，通常會有服務等級合約 (SLA) 定義資料庫所需效能層級和資料庫所需可用性層級這類區域。 SLA 的條款通常會驅動執行個體的組態需求。  
  
 執行個體通常是在安裝之後立即進行設定。 初始組態通常是透過規劃要部署至執行個體之資料庫類型的 SLA 需求所決定。 部署資料庫之後，資料庫管理員會監視執行個體的效能，並在效能標準顯示執行個體不符合 SLA 需求時，視需要調整組態設定。  
  
## <a name="configuration-tasks"></a>組態工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述各種執行個體組態選項以及如何檢視或變更這些選項。|[伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
|描述如何檢視及設定執行個體中新資料和記錄檔的預設位置。|[檢視或變更資料及記錄檔的預設位置 &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)|  
|描述如何設定 SQL Server 使用軟體 NUMA。|[軟體 NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)|  
|描述如何將 TCP/IP 通訊埠對應到非統一記憶體存取 (NUMA) 節點相似性。|[將 TCP/IP 通訊埠對應到 NUMA 節點 &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)|  
|描述如何啟用 Windows 鎖定記憶體中的分頁原則。 此原則決定哪些帳戶可以使用處理序將資料保留在實體記憶體中，以防止系統將資料傳送到磁碟上的虛擬記憶體。|[啟用鎖定記憶體分頁選項 &#40;Windows&#41;](../../database-engine/configure-windows/enable-the-lock-pages-in-memory-option-windows.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 執行個體 &#40;SQL Server&#41;](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  
