---
title: 查詢選項執行 （一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.general.f1
ms.assetid: 858a0263-2f04-4692-b8bf-63e93c998ead
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 955dcff3399f6936fb5b1f8042dae4658a55a11f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844770"
---
# <a name="query-options-execution-general-page"></a>查詢選項執行 (一般頁面)
  使用此頁面來指定執行 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢的選項。 若要存取此對話方塊，請以滑鼠右鍵按一下查詢編輯器視窗的主體，然後按一下 [查詢選項]。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **SET ROWCOUNT**  
 預設值 0 指出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將等候結果，直到所有結果都收到為止。 如果您要 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在取得指定的資料列數後停止查詢，請提供大於 0 的值。 若要關閉此選項 (以便傳回所有資料列)，請指定 SET ROWCOUNT 0。  
  
 **SET TEXTSIZE**  
 2,147,483,647 個位元組的預設值表示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將提供完整的資料欄位，直到 `text`、`ntext`、`nvarchar(max)` 及 `varchar(max)` 資料欄位的上限。 這不會影響 XML 資料類型。 提供較小的數值，即可在有大量數值時，限制傳回的結果數量。 資料行若大於提供的數值，就會被截斷。  
  
 **執行逾時**  
 指出取消查詢之前要等候的秒數。 值為 0 表示無盡的等候，或沒有逾時。  
  
 **批次分隔符號**  
 鍵入您用來將 Transact-SQL 陳述式分隔成批次的文字。 預設為 GO。  
  
 **預設會以 SQLCMD 模式開啟新查詢**  
 選取此核取方塊，即可以 SQLCMD 模式開啟新查詢。 只有在透過 [工具] 功能表開啟此對話方塊時，才可以看見此核取方塊。  
  
 當您選取此選項時，請注意以下限制：  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器中的 IntelliSense 會關閉。  
  
-   由於查詢編輯器不會從命令列執行，所以您無法傳入命令列參數 (如變數)。  
  
-   由於查詢編輯器無法回應作業系統提示，所以您必須非常小心，不要執行互動式陳述式。  
  
 **重設為預設值**  
 將此頁面上的所有值重設為原始預設值。  
  
  
