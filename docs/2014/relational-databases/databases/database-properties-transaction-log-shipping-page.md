---
title: 資料庫屬性 (交易記錄傳送頁面) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.databaseproperties.logshipping.f1
ms.assetid: 72c4e539-fe11-4d57-b977-65b418d5916f
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 33cfa1efca7dcefae3dac55a7fc2806cb9d4fc2a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135185"
---
# <a name="database-properties-transaction-log-shipping-page"></a>資料庫屬性 (交易記錄傳送頁面)
  使用此頁面即可設定和修改資料庫記錄傳送的屬性。  
  
 如需記錄傳送概念的說明，請參閱 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
## <a name="options"></a>選項。  
 **將此啟用為記錄傳送組態的主要資料庫**  
 啟用此資料庫為記錄傳送的主要資料庫。 先選取它，然後設定此頁面上的其他選項。 如果您清除此核取方塊，就會卸除此資料庫的記錄傳送組態。  
  
 **備份設定**  
 按一下 [備份設定] 即可設定備份排程、位置、警示及封存參數。  
  
 **備份排程**  
 顯示主要資料庫目前選取的備份排程。 按一下 **[備份設定]** 即可修改這些設定。  
  
 **上次建立的備份**  
 指出主要資料庫上次備份交易記錄的時間和日期。  
  
 **次要伺服器執行個體與資料庫**  
 列出此主要資料庫目前設定的次要伺服器與資料庫。 反白顯示資料庫，然後按一下 **[...]** 即可修改與次要資料庫相關聯的參數。  
  
 **[加入]**  
 按一下 [加入]，即可將次要資料庫加入此主要資料庫的記錄傳送組態。  
  
 **移除**  
 從這個記錄傳送組態中，移除選取的資料庫。 先選取資料庫，然後按一下 **[移除]**。  
  
 **使用監視伺服器執行個體**  
 設定此記錄傳送組態的監視伺服器執行個體。 選取 **[使用監視伺服器執行個體]** 核取方塊，然後按一下 **[設定]** 即可指定監視伺服器執行個體。  
  
 **監視伺服器執行個體**  
 指出此記錄傳送組態目前設定的監視伺服器執行個體。  
  
 **[設定]**  
 設定記錄傳送組態的監視伺服器執行個體。 按一下 **[設定]** 即可設定此監視伺服器執行個體。  
  
 **指令碼組態**  
 使用選取的參數，產生用來設定記錄傳送的指令碼。 按一下 **[指令碼組態]**，然後選擇指令碼的輸出目的地。  
  
> [!IMPORTANT]  
>  您必須叫用 **[次要資料庫設定]** 對話方塊，才能編寫次要資料庫的指令碼設定。 叫用此對話方塊將可連接至次要伺服器，並擷取產生指令碼所需之次要資料庫的目前設定。  
  
## <a name="see-also"></a>另請參閱  
 [記錄傳送預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql)   
 [記錄傳送資料表 &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/log-shipping-tables-transact-sql)  
  
  
