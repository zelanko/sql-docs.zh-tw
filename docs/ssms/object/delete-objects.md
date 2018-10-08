---
title: 刪除物件 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.deleteobjects.f1
helpviewer_keywords:
- Delete Objects dialog box
ms.assetid: 49541441-179c-40d3-ba0c-01bcae545984
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0bbf560a9e38627e695cafb1463519a82979939f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640838"
---
# <a name="delete-objects"></a>刪除物件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
使用此對話方塊來刪除資料庫或資料庫物件。  
  
## <a name="uielement-list"></a>UIElement 清單  
**要刪除的物件**  
顯示將要刪除之物件的名稱、類型、擁有者和狀態，以及有關執行期間發生錯誤的任何訊息。  
  
> [!NOTE]  
> 在資料庫上執行 [刪除] 相當於在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中發出 DROP DATABASE。  
  
**顯示相依性**  
按一下即可同時顯示相依於目前所選取物件的物件，以及目前物件相依的物件 (向上和向下相依性)。 [顯示相依性] 對話方塊中所顯示的資訊是唯讀的。  
  
> [!NOTE]  
> [顯示相依性] 按鈕並不會出現在所有類型的資料庫物件上。 若要檢視相依性，但[顯示相依性] 按鈕無法使用時，請以滑鼠右鍵按一下物件總管中的物件，然後按一下 [檢視相依性]。  
  
**刪除資料庫的備份與還原記錄資訊**  
只出現於資料庫已刪除時，此核取方塊會導致主旨資料庫的備份與還原記錄從 **msdb** 資料庫中刪除。  
  
**關閉現有的連接**  
只出現於資料庫已刪除時，此核取方塊會結束主旨資料庫的連接。  
  
