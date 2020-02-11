---
title: Oracle 發行者的管理考量 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], administrative considerations
- administering replication, Oracle publishing
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 42791ed9e60ad633ee1331dfc8326d58c0546000
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63022559"
---
# <a name="administrative-considerations-for-oracle-publishers"></a>Oracle 發行者的管理考量
  在設定「Oracle 發行者」並且複寫變更追蹤機制到位之後，Oracle 資料庫系統的管理員仍可使用標準 Oracle 資料庫公用程式並執行一般的系統管理工作。 但是，您應該留意執行特定管理工作對已發行資料的影響。  
  
 卸除或修改為複寫發行的資料行，或者卸除或修改任何複寫物件除外，這些考量不會套用至快照式發行集。  
  
## <a name="importing-and-loading-data"></a>匯入與載入資料  
 為 Oracle 上的交易式發行集變更追蹤使用觸發程序。 僅在出現更新、插入或刪除時引發複寫觸發程序的情況下，方可將對已發行資料表所作的變更複寫給「訂閱者」。 Oracle 公用程式 Oracle Import 與 SQL*Loader 均有在使用這些公用程式將資料列插入複寫資料表時，決定是否引發觸發程序的選項。  
  
### <a name="oracle-import"></a>Oracle Import  
 使用 Oracle Import，您可以將選項 **忽略** 設定為 y 或 n (預設值為 n)。 如果 **忽略** 設定為 n，則資料表將卸除並在匯入期間重新建立。 這將會移除複寫觸發程序並停用複寫。 如果將 **忽略** 設定為 y，匯入會嘗試將資料列載入現有的資料表，這將引發複寫觸發程序。 因此，在使用「匯入」工具匯入複寫資料表時，務必將 **忽略** 設定為 y。  
  
### <a name="sqlloader"></a>SQL*Loader  
 使用 SQL\*Loader，您可以將選項**導向**設定為 true 或 false (預設值為 false)。 如果將 **導向** 設定為 false，資料列會使用傳統的 INSERT 陳述式插入，這將引發複寫觸發程序。 如果將 **導向** 設定為 true，載入將最佳化，並且不引發觸發程序。 因此，在使用 SQL*Loader 工具載入複寫資料表時，務必將 **導向** 設定為 false。  
  
## <a name="making-changes-to-published-objects"></a>變更已發行物件  
 執行下列動作無需特殊考量：  
  
-   在已發行資料表上重建索引。  
  
-   將使用者觸發程序新增至已發行資料表。  
  
 下列動作要求您停止已發行資料表上的所有活動：  
  
-   移動已發行資料表。  
  
 下列動作要求您卸除發行集、執行作業，然後重新建立發行集：  
  
-   截斷已發行資料表。  
  
-   重新命名已發行資料表。  
  
-   將資料行新增至已發行資料表。  
  
-   卸除或修改為複寫發行的資料行。  
  
-   執行非記錄作業。  
  
## <a name="dropping-or-modifying-replication-objects"></a>卸除或修改複寫物件  
 如果您卸除或修改任何「發行者」層級追蹤資料表、觸發程序、順序或預存程序，則必須卸除並重新設定「發行者」。 如需這些物件的部分清單，請參閱[在 Oracle 發行者端建立的物件](objects-created-on-the-oracle-publisher.md)。  
  
 如需卸除並重新設定「發行者」的詳細資訊，請參閱主題＜ [Troubleshooting Oracle Publishers](troubleshooting-oracle-publishers.md)＞中的「變更要求重新設定發行者」一節。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](configure-an-oracle-publisher.md)   
 [Oracle 發行者的設計考量與限制](design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle 發行概觀](oracle-publishing-overview.md)  
  
  
