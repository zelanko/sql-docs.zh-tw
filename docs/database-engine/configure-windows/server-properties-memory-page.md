---
title: 伺服器屬性 (記憶體頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.memory.f1
ms.assetid: 46a77d4e-ab92-49d3-a14b-423462e50715
caps.latest.revision: 45
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d0ef063330e48f28b25bef55c467140fa0326534
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32870993"
---
# <a name="server-properties---memory-page"></a>伺服器屬性 - 記憶體頁面
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此頁面來檢視或修改伺服器記憶體選項。 **[最小伺服器記憶體]** 設定為 0 且 **[最大伺服器記憶體]** 設為 2147483647 MB 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就可在任何特定時間利用最佳的記憶體數量，但受作業系統和其他應用程式目前所使用的記憶體數量所限制。 隨著電腦與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的負載有所變更，記憶體的配置也會變更。 您可以進一步將這個動態記憶體配置限制為下列所指定的最小值和最大值。  
  
## <a name="options"></a>選項。  
 **最小伺服器記憶體 (以 MB 為單位)**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 至少應使用最小配置記憶體數量來啟動，且不會釋放低於此值的記憶體。 根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的大小和活動來設定此值。 請一律將這個選項設定為合理的值，以確保作業系統不會向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要求太多記憶體，而影響 Windows 效能。  
  
 **最大伺服器記憶體 (以 MB 為單位)**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動和執行時可以配置的最大記憶體數量。 如果您知道會有多個應用程式與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同時執行，且您要確保有足夠的記憶體來執行這些應用程式，就可以將此組態選項設定為特定的值。 如果這些其他應用程式 (例如 Web 或電子郵件伺服器) 只視需要要求記憶體，那麼就不要設定此選項，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在它們需要記憶體時釋放出來。 不過，應用程式通常是在啟動時使用可以取得的任何記憶體，而且不會在需要時再要求更多記憶體。 如果以這種方式運作的應用程式與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]同時在同一部電腦上執行的話，請設定此選項的值，以保證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會配置應用程式所需的記憶體。 您可以為 [最大伺服器記憶體]  指定的最小記憶體數量是 128 MB (舊版 32 位元系統是 64 MB)。  
  
 **索引建立記憶體 (以 KB 為單位，0 = 動態記憶體)**  
 指定索引建立排序期間要使用的記憶體數量 (以 KB 為單位)。 預設值零會啟用動態配置，不需要進一步調整就可適用於大部分情況；不過使用者也可以輸入介於 704 到 2147483647 之間的不同值。  
  
> [!NOTE]  
>  從 1 到 703 的值是不允許的。 如果輸入此範圍的值，欄位會使用 704 覆寫輸入的值。  
  
 **每個查詢的最小記憶體 (以 KB 為單位)**  
 指定用來執行查詢的記憶體數量配置 (以 KB 為單位)。 使用者可以設定介於 512 到 2147483647 之間的值。 預設值為 1024 KB。  
  
 **設定的值**  
 針對此窗格中的選項，顯示設定的值。 如果您變更這些值，請按一下 **[執行中的值]** ，即可查看變更是否已生效。 如果沒有的話，就必須先重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
 **[執行中的值]**  
 針對此窗格中的選項，顯示目前執行中的值。 這些值是唯讀的。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
