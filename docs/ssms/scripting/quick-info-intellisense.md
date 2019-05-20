---
title: 快速資訊 (IntelliSense) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1ce292a91733de2d1e5010d1ba1c1585ff72685a
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2019
ms.locfileid: "65821992"
---
# <a name="quick-info-intellisense"></a>快速資訊 (IntelliSense)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 的 **[快速資訊]** 選項會顯示程式碼中之任何識別碼的完整宣告。 當您將滑鼠指標移到識別碼上方時，系統就會在黃色的快顯視窗中顯示它的宣告。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，資料庫引擎和 XML 查詢編輯器中會提供 **[快速諮詢]** 。  
  
## <a name="transact-sql-quick-info"></a>Transact-SQL 快速諮詢  
 **[快速諮詢]** 會在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中顯示兩種資訊。 不是處於偵錯模式時， **[快速諮詢]** 會顯示運算式宣告。 處於偵錯模式時， **[快速諮詢]** 會改為顯示運算式的名稱及其目前值。  
  
 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中， **[快速資訊]** 僅適用於 IntelliSense 支援的這些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法部分。 例如，如果您將滑鼠指標移到某個物件的識別碼上方，但是該物件具有 IntelliSense 不支援的資料類型，[快速資訊] 快顯視窗就會包含表示不支援此資料類型的訊息。  
  
## <a name="see-also"></a>另請參閱  
 [IntelliSense 所支援的 Transact-SQL 語法](../../relational-databases/scripting/transact-sql-syntax-supported-by-intellisense.md)  
  
  
