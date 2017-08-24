---
title: "專案設定 （移轉） (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 82f8857f-7ab1-4738-ab6e-b1e95ea94924
caps.latest.revision: 9
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 06cda31832fca59fec1a0b064d211cfabc8cdac6
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-migration-sybasetosql"></a>專案設定 （移轉） (SybaseToSQL)
[移轉] 頁面的**專案設定**對話方塊包含自訂如何 SSMA 會移轉資料從 Sybase Adaptive Server Enterprise (ASE) 來設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
[移轉] 窗格是在**專案設定**和**預設專案設定**對話方塊。  
  
-   若要指定所有的 SSMA 專案設定**工具**功能表上，選取**預設專案設定**，選取移轉專案類型設定為需要從變更 / 檢視**移轉的目標版本**下拉式清單按一下**一般**左的窗格中，然後再按一下底部**移轉**。  
  
-   若要指定目前的專案中，設定**工具**功能表上，選取**專案設定**，按一下 **一般**左的窗格中，然後再按一下底部**移轉**。  
  
## <a name="date-correction-options"></a>日期 [修正] 選項  
  
|詞彙|定義|  
|--------|--------------|  
|**取代不受支援的日期**|指定是否 SSMA 應該更正日期早於最舊的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime**日期 (01 1753 年 1 月)。<br /><br />若要保留目前的日期值，請選取**不執行任何動作**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不會接受之前 01 年 1 月 1753年的日期的日期時間資料行中。 如果您使用較舊的日期，您必須將日期時間值轉換為字元的值。<br /><br />若要將之前 01 年 1 月 1753年的日期轉換成 NULL，選取**取代 NULL**。<br /><br />若要取代支援日期之前 01 年 1 月 1753年的日期，請選取**取代為最接近的支援日期**。<br /><br />**預設模式**： 不執行任何動作<br /><br />**開放式模式**： 不執行任何動作<br /><br />**完整模式**： 取代為最接近的支援的日期|  
  
## <a name="migration-engine"></a>移轉引擎  
  
|詞彙|定義|  
|--------|--------------|  
|**移轉引擎**|指定在資料移轉期間使用的資料庫引擎。 用戶端端資料移轉是指從來源並將該資料插入 SQL Server 的大量擷取資料的 SSMA 用戶端。 伺服器端資料移轉是指 SSMA 資料移轉引擎 （大量複製程式） 上 SQL Server 中執行的 SQL 代理程式作業，從來源擷取資料，並直接插入 SQL Server，以避免額外用戶端躍點 （更佳的效能）。<br /><br />**預設模式**： 用戶端資料移轉引擎<br /><br />**開放式模式**： 用戶端資料移轉引擎<br /><br />**完整模式**： 用戶端資料移轉引擎|  
  
> [!IMPORTANT]  
> 當**移轉引擎**選項設定為**伺服器端資料移轉引擎**、 新的專案設定選項**使用 32 位元伺服器端資料移轉引擎**隨即出現。 它會指定是否使用 32 位元或 64 位元的大量複製程式 (BCP) 公用程式，來移轉資料。  
  
## <a name="miscellaneous-options"></a>其他選項  
  
|詞彙|定義|  
|--------|--------------|  
|**批次大小**|指定批次資料移轉期間使用的大小。<br /><br />**預設模式**: 10000<br /><br />**開放式模式**: 10000<br /><br />**完整模式**: 10000|  
|**檢查條件約束**|指定將資料插入 SQL Server 資料表時，SSMA 是否應該檢查條件約束。<br /><br />**預設模式**: False<br /><br />**開放式模式**: False<br /><br />**完整模式**: False|  
|**資料移轉逾時**|指定在資料移轉期間使用的逾時<br /><br />**預設模式**: 15<br /><br />**開放式模式**: 15<br /><br />**完整模式**: 15|  
|**擴充的資料移轉選項**|顯示個別的詳細資料 索引標籤中的每個資料表的額外資料移轉選項。<br /><br />**預設模式**： 隱藏<br /><br />**開放式模式**： 隱藏<br /><br />**完整模式**： 隱藏|  
|**引發觸發程序**|指定當它將資料加入至 SQL Server 資料表，SSMA 是否應該引發插入觸發程序。<br /><br />**預設模式**: False<br /><br />**開放式模式**: False<br /><br />**完整模式**: False|  
|**保留識別**|指定 SSMA 是否要將資料加入至 SQL Server 時保存 Sybase 識別值。 值為 False 會識別值依目的地指派。<br /><br />**預設模式**: True<br /><br />**開放式模式**: True<br /><br />**完整模式**: True|  
|**保留 Null**|指定是否要 SSMA 保存來源資料中的 null 值時，它將資料加入 SQL Server，不論在 SQL Server 中指定的預設值。<br /><br />**預設模式**: True<br /><br />**開放式模式**: True<br /><br />**完整模式**: True|  
|**錯誤時**|發生錯誤時，請停止資料移轉。 它有三個選項：<br /><br />**停止移轉：**停止資料移轉作業<br /><br />**繼續進行下一個資料表：**會停止目前的資料表資料移轉並繼續進行下一個<br /><br />**繼續進行下一個批次：**會停止目前的批次的資料移轉並繼續進行下一個<br /><br />**預設模式**： 繼續進行下一個批次<br /><br />**開放式模式**： 繼續進行下一個批次<br /><br />**完整模式**： 繼續進行下一個批次|  
|**四捨五入的數字的小數部分**|指定是否要修剪 decimal 和 numeric 資料的小數部分的整數類型的移轉期間，或如果為非一般的小數部分會顯示錯誤訊息<br /><br />**預設模式**： 否<br /><br />**開放式模式**： 否<br /><br />**完整模式**： 否|  
|**Sybase Unicode Endian**|指定以位元組由小到大 Sybase Unicode 字串類型。 此特定的設定，可以設定下列選項：<br /><br />由小到大<br /><br />Big endian<br /><br />**預設模式**: Little endian<br /><br />**開放式模式**: Little endian<br /><br />**完整模式**: Little endian|  
|**資料表鎖定**|指定當它將資料加入資料表資料移轉期間，SSMA 是否鎖定資料表。 大量複製作業期間，會取得大量更新鎖定。 如果值為 False 時，鎖定資料列層級設定。<br /><br />**預設模式**: True<br /><br />**開放式模式**: True<br /><br />**完整模式**: True|  
|**使用資料指標**|從使用資料指標，如果此選項設定的來源資料庫擷取資料。<br /><br />**預設模式**: False<br /><br />**開放式模式**: False<br /><br />**完整模式**: False|  
  
## <a name="parallel-data-migration"></a>平行處理資料移轉  
  
|詞彙|定義|  
|--------|--------------|  
|**平行處理資料移轉模式**|指定用來分岔執行緒，以便啟用平行的資料移轉的模式。 在 Auto 模式 SSMA 會選擇分叉移轉資料的執行緒 (預設為 10) 數目。 在 [自訂] 模式中，使用者可以指定分叉移轉資料的執行緒數目 （最小值是 1，最大值為 100）。 目前，只有用戶端資料移轉的引擎支援平行處理資料移轉。<br /><br />**預設模式**: Auto<br /><br />**開放式模式**: Auto<br /><br />**完整模式**: Auto|  
  
> [!IMPORTANT]  
> 當**平行的資料移轉模式**選項設定為**自訂**、 新的專案設定選項**執行緒計數**隨即出現。 它會指定用於資料移轉的執行緒數目。  
  

