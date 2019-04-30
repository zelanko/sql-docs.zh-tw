---
title: 第 9 課：建置並執行應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f52d3f3a-0b09-4b34-9112-0b3655271587
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b87a8b4ba546c53dfd4e4e1819b3b01b4f5cf3bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278960"
---
# <a name="lesson-9-build-and-run-the-application"></a>第 9 課：建置及執行應用程式
  建立資料表的資料篩選後，下一步是要建置和執行網站應用程式。  
  
### <a name="to-build-and-run-the-application"></a>若要建置並執行應用程式  
  
1.  按 **CTRL+F5** 執行 Default.aspx 頁面，但不進行偵錯，或按 F5 執行頁面並進行偵錯。  
  
     在建置過程中，報表會進行編譯，而找到的任何錯誤 (例如報表中所使用運算式的語法錯誤) 都會加入至位於 Visual Studio 視窗底部的 **[工作清單]** 。  
  
     網頁會出現在瀏覽器中。 ReportViewer 控制項會顯示報表。 您可以使用工具列瀏覽報表、縮放，以及將報表匯出至 Excel。  
  
2.  將滑鼠停留在 **[名稱]** 資料行底下的任何資料列上方。 滑鼠游標會顯示手掌符號。  
  
3.  按一下 **[名稱]** 資料行中的值。 子報表隨即顯示，並且包含對應的篩選資料。  
  
4.  按一下 **ReportViewer**工具列中的 **[返回父報表]** 圖示，導覽回 **[父]** 報表。  
  
     ![使用 ReportViewer 鑽研 ssrs](../../2014/tutorials/media/ssrs-drillthrough-report.png "ssrs 鑽研使用 ReportViewer")  
  
5.  關閉瀏覽器即可結束。  
  
  
