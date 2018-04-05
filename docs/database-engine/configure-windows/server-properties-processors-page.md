---
title: 伺服器屬性 (處理器頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66d79603535b4a31bed89623d8408d1993073516
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="server-properties---processors-page"></a>伺服器屬性 - 處理器頁面
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 使用此頁面來檢視或修改處理器選項。 只有在安裝了一個以上的處理器時，處理器相似性設定才會啟用。  
  
## <a name="options"></a>選項。  
 **處理器相似性**  
 將處理器指派給特定的執行緒，以避免執行處理器重新載入，並減少在處理器間進行執行緒的移轉。 如需詳細資訊，請參閱 [affinity mask 伺服器組態選項](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)。  
  
 **I/O 相似性**  
 將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟 I/O 繫結到指定 CPU 的子集。 如需詳細資訊，請參閱 [affinity I/O mask 伺服器組態選項](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)。  
  
 **自動設定所有處理器的處理器相似性遮罩**  
 允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定處理器相似性。  
  
 **自動設定所有處理器的 I/O 相似性遮罩**  
 允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定 I/O 相似性。  
  
 **最大工作者執行緒**  
 0 允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能動態設定工作者執行緒的數目。 此設定對大多數系統都是最佳的。 然而，視系統組態而定，將此選項設定成特定的值，有時候可以提高效能。 如需詳細資訊，請參閱 [設定 max worker threads 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)。  
  
 **提高 SQL Server 優先權**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否要使用比同一台電腦上之其他處理序更高的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 排序優先權來執行。 如需詳細資訊，請參閱 [設定 priority boost 伺服器組態選項](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)。  
  
 **使用 Windows Fibers (輕量型共用)**  
 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務使用 Windows Fibers 而不用執行緒。 請注意，這只有在 Windows 2003 Server Edition 中才可以使用。 如需詳細資訊，請參閱 [輕量型共用伺服器組態選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。  
  
 **設定的值**  
 針對此窗格中的選項，顯示設定的值。 如果您變更這些值，請按一下 **[執行中的值]** ，即可查看變更是否已生效。 如果沒有的話，就必須先重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
 **[執行中的值]**  
 針對此窗格中的選項，檢視目前執行中的值。 這些值是唯讀的。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
