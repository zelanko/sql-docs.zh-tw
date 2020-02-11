---
title: 連接到伺服器 (Oracle)，連接屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.oracleconnection.connectionprops.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 479b0d562ffb78bc0003ca320eea0a85ab172430
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721687"
---
# <a name="connect-to-server-oracle-connection-properties"></a>連接到伺服器 (Oracle)，連接屬性
  使用 [**連接到伺服器**] 對話方塊的 [**連接屬性**] 索引標籤，即可指定**閘道**的發行選項或**完成**。 識別發行者之後，除非卸除並重新設定發行者，否則無法變更此選項。 如需詳細資訊，請參閱[設定 Oracle 發行者](non-sql/configure-an-oracle-publisher.md)。  
  
## <a name="options"></a>選項。  
 **發行者類型**  
 選取 **[閘道]** 或 **[完整]**。 [**完成**] 選項的設計目的是要提供快照式和交易式發行集，以及一組完整的 Oracle 發佈支援功能。 
  **[閘道]** 選項可以在複寫作為系統之間的閘道時，提供特定的設計最佳化以提升效能。 如果您計畫在多個交易式發行集內發行相同的資料表，就無法使用 **[閘道]** 選項。 如果您選取 **[閘道]**，則資料表最多只能在一個交易式發行集裡出現，但可以在任意數目的快照式發行集裡出現。  
  
 **設定**  
 指定在發生超時[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]錯誤之前，散發者應該嘗試連接到「Oracle 發行者」的時間長度。  
  
## <a name="see-also"></a>另請參閱  
 [Oracle 發行相關術語字彙](non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Oracle 發行者的效能微調](non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
