---
title: 任務 16:與主數據管理員進行驗證 |微軟文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d9828c02625ae2bc5a85859577a237b4c4fa99c5
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484678"
---
# <a name="task-16-verifying-with-master-data-manager"></a>工作 16：使用主資料管理員驗證
  在這項工作中，您會檢查 SSIS 封裝提交的批次作業狀態，並確認資料已使用主資料管理員上傳至 MDS 伺服器。  
  
1.  啟動**主資料管理員**`http://localhost/MDS`()。 如果已開啟,請按下頂部的**Microsoft SQL 伺服器主資料服務**以切換到**首頁**。  
  
2.  點選**的管理**。  
  
3.  請注意,清單中提交了一個名為**EIMBatch**的批處理。 如果看不到以下螢幕,請單擊功能表欄上的 **「導入資料**」。  
  
     ![EIM 批次](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM 批次")  
  
4.  按一下頂部的 SQL Server **2012 主資料服務**,切換回主頁。  
  
5.  確保為 **「模型」** 選擇了**供應商**模型,並為**版本**選擇了**VERSION_1,** 然後單擊 **「資源管理器**」。。  
  
6.  您可以看到資料的 SSIS 封裝已匯入至 MDS。 數據應清除,並且沒有重複**的代碼**值(注意:Excel 中的**供應商 ID**列對應於 MDS 中的供應商實體**的代碼**屬性)。  
  
## <a name="next-step"></a>後續步驟  
 [工作 17：檢閱 SSIS 封裝所建立的 DQS 清理專案](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
