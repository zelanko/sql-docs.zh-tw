---
title: 專案設定 （移轉） (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 82f8857f-7ab1-4738-ab6e-b1e95ea94924
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ff7d8035fef2e766c598231b43f667355b088688
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "40392930"
---
# <a name="project-settings-migration-sybasetosql"></a>專案設定 (移轉) (SybaseToSQL)
[移轉] 頁面**專案設定** 對話方塊中包含自訂如何 SSMA 會移轉的資料從 Sybase Adaptive Server Enterprise (ASE) 來設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
[移轉] 窗格位於兩者**專案設定**並**預設專案設定**對話方塊。  
  
-   若要指定所有的 SSMA 專案設定**工具**功能表上，選取**預設專案設定**，選取 移轉專案類型，則需要檢視 / 變更設定**移轉目標版本**下拉式清單按一下**一般**底部的左的窗格和 **移轉**。  
  
-   若要指定目前的專案中，設定**工具**功能表上，選取**專案設定**，按一下 **一般**底部的左窗格中，然後按一下  **移轉**。  
  
## <a name="date-correction-options"></a>日期 [修正] 選項  
  
|詞彙|定義|  
|--------|--------------|  
|**取代不支援的日期**|指定是否 SSMA 應該更正日期早於最早[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**日期 (01 1753 年 1 月)。<br /><br />若要保留目前的日期值，請選取**不執行任何動作**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會接受之前 01 年 1 月 1753年的日期的日期時間資料行中。 如果您使用較舊的日期，您必須將日期時間值轉換為字元。<br /><br />若要將 NULL 轉換之前 01 年 1 月 1753年的日期，請選取**取代為 NULL**。<br /><br />若要支援的日期取代之前 01 年 1 月 1753年的日期，請選取**最近支援的日期取代**。<br /><br />**預設模式**： 不執行任何動作<br /><br />**開放式模式**： 不執行任何動作<br /><br />**完整模式**： 取代為最接近的支援的日期|  
  
## <a name="migration-engine"></a>移轉引擎  
  
|詞彙|定義|  
|--------|--------------|  
|**移轉引擎**|指定在資料移轉期間使用的資料庫引擎。 用戶端端資料移轉是指從來源並將該資料插入 SQL Server 的大量擷取資料的 SSMA 用戶端。 伺服器端資料移轉是指 SSMA 資料移轉引擎 （大量複製程式） 上 SQL Server 中執行的 SQL Agent 作業，從來源擷取資料，並直接插入 SQL Server，以避免額外用戶端躍點 （更佳的效能）。<br /><br />**預設模式**： 用戶端端資料移轉引擎<br /><br />**開放式模式**： 用戶端端資料移轉引擎<br /><br />**完整模式**： 用戶端端資料移轉引擎|  
  
> [!IMPORTANT]  
> 當**移轉引擎**選項設定為**伺服器端資料移轉引擎**]、 [新的專案設定選項**使用 32 位元伺服器端資料移轉引擎**會顯示. 它會指定是否要將 32 位元或 64 位元的大量複製程式 (BCP) 公用程式用來移轉資料。  
  
## <a name="miscellaneous-options"></a>其他選項  
  
|詞彙|定義|  
|--------|--------------|  
|**批次大小**|指定批次在資料移轉期間使用的大小。<br /><br />**預設模式**: 10000<br /><br />**開放式模式**: 10000<br /><br />**完整模式**: 10000|  
|**檢查條件約束**|指定當資料插入 SQL Server 資料表，SSMA 是否應該檢查條件約束。<br /><br />**預設模式**: False<br /><br />**開放式模式**: False<br /><br />**完整模式**: False|  
|**資料移轉逾時**|指定在資料移轉期間使用的逾時<br /><br />**預設模式**: 15<br /><br />**開放式模式**: 15<br /><br />**完整模式**: 15|  
|**擴充的資料移轉選項**|在個別的詳細資料 索引標籤會顯示每個資料表的額外的資料移轉選項。<br /><br />**預設模式**： 隱藏<br /><br />**開放式模式**： 隱藏<br /><br />**完整模式**： 隱藏|  
|**引發觸發程序**|指定當它將資料加入至 SQL Server 資料表，SSMA 是否應該引發插入觸發程序。<br /><br />**預設模式**: False<br /><br />**開放式模式**: False<br /><br />**完整模式**: False|  
|**保留識別**|指定 SSMA 是否要將資料加入至 SQL Server 時保存 Sybase 識別值。 值為 False 會導致可由目的地指派的識別值。<br /><br />**預設模式**: True<br /><br />**開放式模式**: True<br /><br />**完整模式**: True|  
|**保留 Null**|指定是否 SSMA 會保留來源資料中的 null 值時，它將資料加入 SQL Server，不論在 SQL Server 中指定的預設值。<br /><br />**預設模式**: True<br /><br />**開放式模式**: True<br /><br />**完整模式**: True|  
|**錯誤時**|發生錯誤時，就會停止資料移轉。 它有三個選項：<br /><br />**停止移轉：** 停止資料移轉作業<br /><br />**請繼續進行下一個表格：** 會停止目前的資料表資料移轉並繼續進行下一個<br /><br />**請繼續進行下一個批次：** 會停止目前的批次的資料移轉並繼續進行下一個<br /><br />**預設模式**： 繼續進行下一個批次<br /><br />**開放式模式**： 繼續進行下一個批次<br /><br />**完整模式**： 繼續進行下一個批次|  
|**四捨五入的數字的小數部分**|指定是否要修剪 decimal 與 numeric 資料的小數部分的整數類型的移轉期間，或如果小數點後為非一般會顯示錯誤訊息<br /><br />**預設模式**： 否<br /><br />**開放式模式**： 否<br /><br />**完整模式**： 否|  
|**Sybase Unicode 位元組由小到大**|指定針對 Sybase Unicode 字串位元組由小到大的型別。 針對此特定的設定，就可以設定下列選項：<br /><br />位元組由小到大<br /><br />Big endian<br /><br />**預設模式**: Little endian<br /><br />**開放式模式**: Little endian<br /><br />**完整模式**: Little endian|  
|**資料表鎖定**|指定時它會將資料加入資料表資料移轉期間 SSMA 是否鎖定資料表。 大量複製作業期間取得大量更新鎖定。 如果值為 False，則鎖定會設定資料列層級。<br /><br />**預設模式**: True<br /><br />**開放式模式**: True<br /><br />**完整模式**: True|  
|**使用資料指標**|從來源資料庫使用資料指標，如果設定這個選項時，會擷取資料。<br /><br />**預設模式**: False<br /><br />**開放式模式**: False<br /><br />**完整模式**: False|  
  
## <a name="parallel-data-migration"></a>平行處理資料移轉  
  
|詞彙|定義|  
|--------|--------------|  
|**平行處理資料移轉模式**|指定 「 分叉 」 執行緒用來啟用平行處理資料移轉的模式。 在 Auto 模式中 SSMA 會選擇將資料移轉的分支的執行緒 (預設為 10) 數目。 在 [自訂] 模式中，使用者可以指定將資料移轉的分支的執行緒數目 （最小值為 1 和最大值為 100）。 目前，只有用戶端端資料移轉引擎支援平行處理資料移轉。<br /><br />**預設模式**： 自動<br /><br />**開放式模式**： 自動<br /><br />**完整模式**： 自動|  
  
> [!IMPORTANT]  
> 當**平行的資料移轉模式**選項設定為**自訂**]、 [新的專案設定選項**執行緒計數**會顯示。 它會指定用於資料移轉的執行緒數目。  
  
