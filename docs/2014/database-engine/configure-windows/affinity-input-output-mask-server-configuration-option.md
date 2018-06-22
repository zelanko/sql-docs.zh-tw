---
title: affinity Input-Output mask 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- affinity I/O mask option
- processor affinity [SQL Server]
- binding processors [SQL Server]
- CPU affinity mask option
ms.assetid: 9950a8c9-9fe0-4003-95df-6f0d1becb0e7
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e3581012106e10eeac623028f2785205838f5f96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022217"
---
# <a name="affinity-input-output-mask-server-configuration-option"></a>affinity Input-Output mask 伺服器組態選項
  為了完成多工作業， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 與 Windows Server 2003 有時會在不同的處理器之間移動處理序執行緒。 雖然從作業系統的觀點來看很有效率，但是在繁重的系統負載下，這項活動可能會降低 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的效能，因為每個處理器快取會重複重新載入資料。 將處理器指派給特定的執行緒，可藉由去除處理器的重新載入，而在這些狀況下增進效能；執行緒與處理器之間的這種關聯，稱為處理器相似性。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 透過兩個相似性遮罩選項支援處理器相似性： **affinity mask** (也稱為 **CPU affinity mask**) 與 **affinity I/O mask**。 如需 **affinity mask** 選項的詳細資訊，請參閱 [affinity mask 伺服器組態選項](affinity-mask-server-configuration-option.md)。 擁有 33 到 64 個處理器的 CPU 與 I/O 相似性支援需要分別另外使用 [affinity64 mask 伺服器組態選項](affinity64-mask-server-configuration-option.md) 與 [affinity64 Input-Output mask 伺服器組態選項](affinity64-input-output-mask-server-configuration-option.md) 。  
  
> [!NOTE]  
>  擁有 33 到 64 個處理器之伺服器的相似性支援只能在 64 位元的作業系統上使用。  
  
 **affinity I/O mask** 選項會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟 I/O 繫結到指定的 CPU 子集。 在高階的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上交易處理 (OLTP) 環境中，此延伸模組可強化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行緒發行 I/O 的效能。 這項增強功能並不支援個別磁碟或磁碟控制器的硬體相似性。  
  
 **affinity I/O mask** 的值可指定在多處理器的電腦中，有哪些 CPU 適合處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟 I/O 作業。 遮罩是一種點陣圖，其中最右邊的位元會指定最低順位 CPU(0)，緊鄰其左側的位元則指定次低順位 CPU(1)，依此類推。 若要設定 32 個以上的處理器，請同時設定 **affinity I/O mask** 與 **affinity64 I/O mask**。  
  
 **affinity I/O mask** 的值如下所示：  
  
-   在多處理器的電腦中，1 位元組的 **affinity I/O mask** 最多可涵蓋 8 個 CPU。  
  
-   在多處理器的電腦中，2 位元組的 **affinity I/O mask** 最多可涵蓋 16 個 CPU。  
  
-   在多處理器的電腦中，3 位元組的 **affinity I/O mask** 最多可涵蓋 24 個 CPU。  
  
-   在多處理器的電腦中，4 位元組的 **affinity I/O mask** 最多可涵蓋 32 個 CPU。  
  
-   若要處理 32 個以上的 CPU，請針對前 32 個 CPU 設定一個 4 位元組的 **affinity I/O mask** ，並針對剩餘的 CPU 設定最多 4 位元組的 **affinity64 I/O mask** 。  
  
 相似性 I/O 模式中的 1 位元，會指定對應的 CPU 適合執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟 I/O 作業；0 位元則指定不要為對應的 CPU 排程任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟 I/O 作業。 若所有的位元都設為零，或未指定 **affinity I/O mask** ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟 I/O 會排程給所有適合處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行緒的 CPU。  
  
 因為設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **affinity I/O mask** 選項是專門的作業，因此只有在必要時才使用。 在大部分情況下，Windows 2000 或 Windows Server 2003 的預設相似性都能提供最佳效能。  
  
 在指定 **affinity I/O mask** 選項時，您必須搭配使用 **affinity mask** 組態選項。 請勿同時在 **affinity I/O mask** 參數與 **affinity mask** 選項中啟用相同的 CPU。 對應到每個 CPU 的位元，應屬於下列三種情況之一：  
  
-   在 **affinity I/O mask** 選項與 **affinity mask** 選項中皆為 0。  
  
-   在 **affinity I/O mask** 選項中為 1，而在 **affinity mask** 選項中為 0。  
  
-   在 **affinity I/O mask** 選項中為 0，而在 **affinity mask** 選項中為 1。  
  
 **affinity I/O mask** 屬於進階選項。 如果您使用`sp_configure`系統預存程序來變更此設定，您可以變更**affinity I/O mask**時，才**顯示進階選項**設為 1。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，重新設定 **affinity I/O mask** 選項需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
> [!CAUTION]  
>  不要在 Windows 作業系統中設定 CPU 相似性，然後又在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中設定相似性遮罩。 這些設定嘗試達到相同的結果，如果組態不一致，可能會有無法預期的結果。 設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU 相似性時，最好使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 `sp_configure` 選項。  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用量 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
