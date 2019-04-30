---
title: 將查詢提示附加至計畫指南 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 2131f796-6359-4f9e-9047-da0b3d4dedaf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 89af21c2c591db2dff678be7aaf8c064e728b9ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151069"
---
# <a name="attach-query-hints-to-a-plan-guide"></a>將查詢提示附加至計畫指南
  在計畫指南中所使用的有效查詢提示組合。 當計畫指南能配合查詢時，系統會先將計畫指南之提示子句中指定的 OPTION 子句加入查詢中，然後再編譯和最佳化查詢。 如果配合計畫指南的查詢已經有 OPTION 子句，在計畫指南中所指定的查詢提示將會取代查詢中的提示。 不過，若要讓計畫指南配合已經有 OPTION 子句的查詢，您必須在指定查詢文字以符合 sp_create_plan_guide 陳述式時，包含查詢的 OPTION 子句。 如果您要將計畫指南中所指定的提示加入查詢中已存在的提示，您不應該取代它們，而是必須在計畫指南的 OPTION 子句中同時指定原始提示和其他提示。  
  
> [!CAUTION]  
>  不當使用查詢提示的計畫指南可能會造成編譯、執行或效能上的問題。 計畫指南應該只能由資深的開發人員與資料庫管理員使用。  
  
## <a name="common-query-hints-used-in-plan-guides"></a>計畫指南中常用的查詢提示  
 可從計畫指南獲益的查詢通常是以參數為基礎，而且有可能執行的效果很差，因為它們使用快取的查詢計畫，這些參數值並不代表最糟榚的情況值或最具代表性的狀況值。 OPTIMIZE FOR 與 RECOMPILE 查詢提示可用以處理此問題。 OPTIMIZE FOR 指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在最佳化查詢時使用參數的特定值。 RECOMPILE 指示伺服器在執行後捨棄查詢計畫，以強制查詢最佳化工具在下次執行相同的查詢時，重新編譯新的查詢計畫。 如需範例，請參閱 [計畫指南](plan-guides.md)。  
  
 此外，您可以指定 INDEX、FORCESCAN 和 FORCESEEK 資料表提示做為查詢提示。 將這些提示指定為查詢提示時，其行為模式就與內嵌資料表或檢視提示相同。 INDEX 提示會強制查詢最佳化工具只使用指定的索引來存取參考之資料表或檢視內的資料。 FORCESEEK 提示會強制最佳化工具只使用索引搜尋作業，以存取參考之資料表或檢視內的資料。 這些提示提供額外的計畫指南功能，並讓您對於使用此計畫指南的查詢最佳化有更大的影響。  
  
  
