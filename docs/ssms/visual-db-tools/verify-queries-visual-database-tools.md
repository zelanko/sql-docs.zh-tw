---
description: 驗證查詢 (Visual Database Tools)
title: 驗證查詢
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:100644
helpviewer_keywords:
- verifying queries
- queries [SQL Server], verifying
- checking queries
ms.assetid: 1382c0c0-46dc-45f9-ab38-9bba1d347eea
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 944d34dbbec6da87d4f3ebd7920d9acd2ad162c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417724"
---
# <a name="verify-queries-visual-database-tools"></a>驗證查詢 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
為避免發生問題，您可以檢查所建立的查詢，確定語法是否正確。 當您在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)輸入陳述式時，這個選項特別有用。  
  
關於驗證查詢的注意事項：  
  
-   即使在 [圖表]**** 窗格和 [準則]**** 窗格中無法表示陳述式，其語法也可以是正確的，因此能夠成功地驗證。  
  
-   [SQL 驗證] 能夠偵測某些，但不是所有的 SQL 錯誤。 如果查詢中包含在 SQL 驗證期間未偵測到的錯誤，當您執行查詢時，資料庫會偵測到錯誤。  
  
-   包含無法驗證參數的查詢。  
  
### <a name="to-verify-an-sql-statement"></a>若要驗證 SQL 陳述式  
  
-   在 [SQL]**** 窗格按一下滑鼠右鍵，然後從快速鍵功能表選取 [驗證 SQL 語法]****。  
  
## <a name="see-also"></a>另請參閱  
[執行查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[使用查詢執行基本作業 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
