---
title: 在套用快照集之前及之後執行指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
- scripts [SQL Server replication]
ms.assetid: 9a6872c2-9bed-477f-9d2f-332d640edcf2
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e05c172b5cd73b81969544b4e72b7895826b5d69
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665066"
---
# <a name="execute-scripts-before-and-after-the-snapshot-is-applied"></a>在套用快照集之前及之後執行指令碼
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以指定在套用快照集之前或之後在「訂閱者」端執行指令碼。 指令碼在很多情況下都會用到，例如在各「訂閱者」端建立登入和結構描述 (物件擁有者) 時。  
  
 為各指令碼指定檔案位置後，每次進行快照集處理時，「快照集代理程式」便會將指令碼檔案複製到目前的快照集資料夾中。 套用快照集時，「散發代理程式」或「合併代理程式」會在執行任何複寫物件指令碼之前，先執行前快照集指令碼。 並在套用所有其他複寫物件指令碼及資料之後，執行後快照集指令碼。 快照集應用程式完成且指令碼檔案成功執行之後，會從「訂閱者」的工作目錄中移除指令碼檔案。  
  
 啟動 **sqlcmd** 公用程式即可執行指令碼。 部署指令碼之前，請使用 **sqlcmd** 執行指令碼，以確保能按預期執行。 在套用快照集前後執行的指令碼內容必須能夠重複。 例如，如果在指令碼中建立資料表，應先檢查該資料表是否已存在，如果存在，再採取適當動作。 指令碼必須能夠重複，因為當您需要重新初始化已套用了指令碼的訂閱時，該指令碼便會在新快照集於重新初始化期間套用時重新被套用。  
  
 若要壓縮快照集檔案 (將其儲存為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 檔案格式)，指令碼也會壓縮並儲存到 CAB 檔案中。 將壓縮的快照集檔傳送給「訂閱者」並解壓縮至「訂閱者」的工作目錄後，將執行任何指示為前快照集指令碼的指令碼。 同樣地，在套用快照集的最後一個步驟中，也會在「訂閱者」端解壓縮並執行後快照集指令碼。  
  
 **若要在套用快照集之前及之後執行指令碼**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]： [如何：在套用快照集的前後執行指令碼 \(SQL Server Management Studio\)](../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   複寫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式設計：[設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [快照集選項](../../relational-databases/replication/snapshot-options.md)  
  
  
