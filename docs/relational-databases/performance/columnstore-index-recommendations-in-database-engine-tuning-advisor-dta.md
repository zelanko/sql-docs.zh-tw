---
title: 資料行存放區索引建議 - Database Engine Tuning Advisor (DTA)
ms.custom: seo-dt-2019
ms.date: 01/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, columnstore index
- Database Engine Tuning Advisor, columnstore and rowstore indexes
ms.assetid: 9fba1139-82cb-4244-a41f-4337a7d0c132
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 81481c540d1d9beee820e30120dfffba8a9cfe0f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486797"
---
# <a name="columnstore-index-recommendations-in-database-engine-tuning-advisor-dta"></a>Database Engine Tuning Advisor (DTA) 中的資料行存放區索引建議
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

 
  資料倉儲和分析工作負載大大受益於[資料行存放區索引](../../t-sql/statements/create-columnstore-index-transact-sql.md)以及傳統的資料列存放區索引。 資料列存放區索引與資料行存放區索引的資料庫建置選擇，是取決於應用程式的工作負載。 在 SQL Server 2016 中，[Database Engine Tuning Advisor (DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md) 可分析您的工作負載，並建議要在資料庫上建置的資料列存放區索引和資料行存放區索引的適當組合。 
  
 SQL Server Management Studio **16.4** 版或更高版本中提供了此功能。 
  
## <a name="how-to-enable-columnstore-index-recommendations-in-database-engine-tuning-advisor-gui"></a>如何在 Database Engine Tuning Advisor GUI 中啟用資料行存放區索引建議

  
  1. 啟動 Database Engine Tuning Advisor，並開啟新的微調工作階段。
  
  2. 在 [一般]  窗格中選取要微調的資料庫和工作負載。
  
  3. 在 [微調選項] 窗格中選取 [建議資料行存放區索引]  這個核取方塊 (請參閱下圖)。
  ![DTA 資料行存放區索引微調選項](../../relational-databases/performance/media/dta-columnstore-indexes-tuning-option.gif)
 
  4. 選取其他微調選項，然後按一下 [開始分析]  按鈕。
  
  5. 完成微調之後，請在 [建議]  窗格中檢視包含任何資料行存放區索引的所有建議 (請參閱下圖)。      
  ![DTA 資料行存放區索引建議](../../relational-databases/performance/media/dta-columnstore-index-recommendation.gif)
  
  6. 按一下 [定義]  超連結，檢視可建立建議索引的 SQL 資料定義語言 (DDL) 陳述式。 依預設，DTA 會在資料行存放區索引名稱中使用後置詞 **col**，以方便識別資料行存放區索引 (請參閱下圖)。
  ![DTA 資料行存放區索引定義](../../relational-databases/performance/media/dta-columnstore-index-definition.gif) 
  
  
  ## <a name="how-to-enable-columnstore-index-recommendations-in-dtaexe-utility"></a>如何在 dta.exe 公用程式中啟用資料行存放區索引建議

若要在使用 dta.exe 命令列公用程式時啟用資料行存放區建議，請使用 **-fc** 命令列參數。

如需 dta.exe 命令列公用程式的詳細資訊，請參閱 [dta 公用程式](../../tools/dta/dta-utility.md)

## <a name="see-also"></a>另請參閱
[資料行存放區索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)       
[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)      
[教學課程：Database Engine Tuning Advisor](../../tools/dta/tutorial-database-engine-tuning-advisor.md)



  

