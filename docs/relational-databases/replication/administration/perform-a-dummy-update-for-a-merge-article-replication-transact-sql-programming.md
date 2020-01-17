---
title: 虛擬合併發行項更新 (複寫 SP)
description: 使用 Transact-SQL 複寫預存程序來執行合併式複寫中所使用之合併發行項的虛擬更新。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_mergedummyupdate
- dummy updates [SQL Server replication]
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 05c3a91d647819126261f0637e0de24d0ce3e4fd
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322029"
---
# <a name="perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming"></a>執行合併發行項的虛擬更新 (複寫 Transact-SQL 程式設計)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  合併式複寫會使用觸發程序做為複寫程序的一部分；對已發行資料表進行更新時，就會引發更新觸發程序。 在某些情況下，可以不引發觸發程序而更新資料，例如在 WRITETEXT 和 UPDATETEXT 作業期間。 在這些情況下，您需要加入虛擬 UPDATE 陳述式以明確地複寫變更。 您可以使用複寫預存程序加入虛擬 UPDATE 陳述式。  
  
### <a name="to-add-a-dummy-update-statement"></a>若要加入虛擬 UPDATE 陳述式  
  
1.  在需要虛擬更新的已發行合併資料表中的資料列上執行作業 (例如，UPDATETEXT)。  
  
2.  在伺服器端 (發行者或訂閱者)，在其中進行變更的資料庫上執行 [sp_mergedummyupdate &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md)。 針對 `@source_object` 指定在其上進行變更的資料表，並針對 `@rowguid` 指定已變更資料列的唯一識別碼。  
  
3.  同步處理訂閱來複寫已變更的資料列。  
  
  
