---
title: 快速資訊 (IntelliSense)
description: 了解如何使用 IntelliSense 的 [快速諮詢] 選項來顯示程式碼中任何識別碼的完整宣告。 在 SQL Server Management Studio 中，此選項可在資料庫引擎編輯器和 XML 查詢編輯器中使用。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Quick Info option [IntelliSense]
- declarations [IntelliSense]
- IntelliSense [SQL Server], Quick Info
- identifier declarations [IntelliSense]
ms.assetid: 3c8b59f4-1922-4bde-844f-5f2306514d96
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a0f2d426c940950b114687f39d7a94bedbb75cf
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036424"
---
# <a name="quick-info-intellisense"></a>快速資訊 (IntelliSense)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 的 **[快速資訊]** 選項會顯示程式碼中之任何識別碼的完整宣告。 當您將滑鼠指標移到識別碼上方時，系統就會在黃色的快顯視窗中顯示它的宣告。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，資料庫引擎和 XML 查詢編輯器中會提供 **[快速諮詢]** 。  
  
## <a name="transact-sql-quick-info"></a>Transact-SQL 快速諮詢  
 **[快速諮詢]** 會在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中顯示兩種資訊。 不是處於偵錯模式時， **[快速諮詢]** 會顯示運算式宣告。 處於偵錯模式時， **[快速諮詢]** 會改為顯示運算式的名稱及其目前值。  
  
 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中， **[快速資訊]** 僅適用於 IntelliSense 支援的這些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法部分。 例如，如果您將滑鼠指標移到某個物件的識別碼上方，但是該物件具有 IntelliSense 不支援的資料類型，[快速資訊]**** 快顯視窗就會包含表示不支援此資料類型的訊息。  
  
## <a name="see-also"></a>另請參閱  
 [IntelliSense 所支援的 Transact-SQL 語法](./transact-sql-syntax-supported-by-intellisense.md)  
  
