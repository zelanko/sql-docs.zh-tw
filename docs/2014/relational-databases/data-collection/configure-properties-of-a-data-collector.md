---
title: 設定資料收集器的屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dc.datacollectionprop.advanced.f1
- sql12.swb.dc.datacollectionprop.general.f1
ms.assetid: cf98f57d-5a6d-4bc3-bf10-783e460fc63d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37df9ccdd0bc2b44384bb9fd3d130c8d3bf8ca36
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62873434"
---
# <a name="configure-properties-of-a-data-collector"></a>設定資料收集器的屬性
  本主題討論如何設定資料收集器的屬性。  
  
## <a name="data-collection-properties-general-tab"></a>資料收集屬性 (一般索引標籤)  
 使用這個頁面可設定管理資料倉儲的設定，並指定在收集而來的資料上傳到資料倉儲之前，應該將這些資料儲存在哪裡。  
  
 **啟用資料收集**  
 選取此選項可啟用資料收集。 這與執行 sp_syscollector_enable_collector 預存程序有相同的效果。 清除此核取方塊會停用資料收集，而且與執行 sp_syscollector_disable_collector 預存程序有相同的效果。  
  
 **Server**  
 顯示將主控管理資料倉儲的伺服器名稱。  
  
 **資料庫名稱**  
 顯示用於管理資料倉儲的關聯式資料庫名稱。  
  
 **測試連接**  
 使用設定資料收集時所提供的資訊，測試與指定之 [伺服器]  的連接。  
  
 **快取目錄**  
 指定在收集而來的資料上傳到管理資料倉儲之前，應該將這些資料儲存在收集資料之系統上的哪一個目錄。 如果未指定 [快取目錄]  ，資料收集器會嘗試尋找 %TEMP% 和 %TMP% 環境變數的位置，並使用其中一個位置當做暫存區的預設位置。 如果未設定這些環境變數，就會發生錯誤，而且系統會提示您建立快取目錄。  
  
## <a name="data-collection-properties-advanced-tab"></a>資料收集屬性 (進階索引標籤)  
 使用這個頁面可針對管理資料倉儲的連接來設定重試設定。  
  
 **上傳失敗時的重試次數**  
 指定當上傳失敗時，重試上傳到管理資料倉儲的次數。 預設值是 1。  
  
## <a name="see-also"></a>另請參閱  
 [管理資料收集](data-collection.md)   
 [設定管理資料倉儲 &#40;SQL Server Management Studio&#41;](configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
