---
title: 追蹤屬性 （一般索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.pro.traceproperties.general.f1
helpviewer_keywords:
- Trace Properties dialog box
ms.assetid: 25227268-143b-477e-aac9-8268bcaf2078
caps.latest.revision: 23
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99621b4d142e6d1686c908783ba63628109eae5e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221938"
---
# <a name="trace-properties-general-tab"></a>追蹤屬性 (一般索引標籤)
  使用 **[追蹤屬性]** 對話方塊的 **[一般]** 索引標籤，來檢視或指定追蹤的屬性。  
  
## <a name="options"></a>選項。  
 **追蹤名稱**  
 指定追蹤的名稱。  
  
 **追蹤提供者名稱**  
 顯示要追蹤之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體名稱。 此欄位自動以連接時指定的伺服器名稱來擴展。 若要變更追蹤提供者的名稱，請按一下 **[取消]** 以關閉對話方塊，並啟動新追蹤。  
  
 **追蹤提供者類型**  
 顯示提供追蹤的伺服器類型。 追蹤定義檔案自動擴展 **[追蹤提供者類型]** 欄位。 您無法修改此欄位。  
  
 **version**  
 顯示提供追蹤的伺服器版本。 追蹤定義檔案自動擴展 **[版本]** 欄位。 您無法修改此欄位。  
  
 **使用範本**  
 從範本目錄中選取範本。 目錄會使用專為目前追蹤提供者類型所建立的預設範本以及使用者自訂範本，進行目錄的擴展。  
  
 **儲存至檔案**  
 將追蹤資料擷取到 .trc 檔。 儲存追蹤資料對日後檢閱與分析很有用。  
  
 **設定最大檔案大小 (MB)**  
 如果您選擇將追蹤資料儲存至檔案，您必須指定追蹤檔案的大小上限。 預設值為 5 MB。 只由存放檔案的檔案系統 (NTFS, FAT) 限制大小上限。  
  
 \<圖形 >**將儲存為**  
 選取儲存之後，您可以選取此圖示以變更檔案名稱。  
  
 **啟用檔案換用**  
 選取以啟用其他檔案的建立，以在達到檔案大小上限時接受追蹤資料。 每個新檔案名稱皆包含原始 .trc 檔案名稱，並循序編號。 例如，一旦達到檔案大小上限， **NewTrace.trc** 隨即關閉，並開啟新檔案 **NewTrace_1.trc**，接著是 **NewTrace_2.trc**等等。 依預設，將追蹤儲存至檔案時，檔案換用為已啟用。  
  
 **伺服器處理追蹤資料**  
 指定執行追蹤的伺服器應處理追蹤資料。 使用此選項會降低追蹤所造成的效能負擔。 如果選取此選項，即使在負荷過重的狀況下仍不會略過任何事件。 如果清除此核取方塊，則 SQL Server Profiler 會執行此處理，而在負荷過重的狀況下有可能不追蹤某些事件。  
  
 **儲存至資料表**  
 將追蹤資料擷取到資料庫資料表。 儲存追蹤資料對日後檢閱與分析很有用。 不過，將追蹤資料儲存至資料表，可能導致儲存追蹤的伺服器負擔過重。 可能的話，不要將追蹤資料表儲存在被追蹤的同一部伺服器上。  
  
 \<圖形 >**目的地資料表**  
 選取將追蹤資料儲存至資料庫資料表之後，您可以選取此圖示以變更資料表名稱。  
  
 **設定最大資料列數 (單位: 千)**  
 指定儲存資料的最大資料列數。 預設為 1000 個資料列。  
  
 **啟用追蹤停止時間**  
 設定追蹤結束與自動關閉的日期和時間。  
  
## <a name="see-also"></a>另請參閱  
 [建立追蹤 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
