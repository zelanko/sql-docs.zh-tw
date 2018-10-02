---
title: 儲存 (不允許) 對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.table.tablerecreatenosave.f1
ms.assetid: 7efda8e3-739f-4c97-a497-b8808a0acbea
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b491d5d0bf14c90d813b0fc66c0112eac1ff0e16
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635296"
---
# <a name="save-not-permitted-dialog-box"></a>儲存 (不允許) 對話方塊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[儲存]\(不允許) 對話方塊會警告您不允許儲存變更，因為您所做的變更需要卸除及重新建立所列出的資料表。  
  
下列動作可能需要重新建立資料表：  
  
-   將新的資料行加入資料表的中間  
  
-   卸除資料行  
  
-   變更資料行的 Null 屬性  
  
-   變更資料行的順序  
  
-   變更資料行的資料類型  
  
若要變更這個選項，請在 [工具] 功能表上按一下 [選項]，展開 [設計工具]，然後按一下 [資料表和資料庫設計工具]。 選取或清除 [防止儲存需要資料表重建的變更] 核取方塊。  
  
