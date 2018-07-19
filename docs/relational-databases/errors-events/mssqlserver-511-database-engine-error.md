---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8b96f5575b233424e34a8beee7ab2276847532f3
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34321442"
---
# <a name="mssqlserver511"></a>MSSQLSERVER_511
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|511|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|ROW_TOOBIG|  
|訊息文字|當 %d 大小的資料列大於允許的最大 %d 時，便無法建立它。|  
  
## <a name="explanation"></a>說明  
您嘗試執行的作業超出資料列大小的上限。 通常資料列大小的上限為 8,060 個位元組。 某些儲存格式包含的負擔可能會減少資料可使用的資料列大小。 例如，當您使用疏鬆資料行時，資料列大小的上限為 8,018 個位元組。 加入或移除資料列的某些作業及變更資料行之資料類型的某些作業需要將資料列重寫到資料頁面，然後移除原始的資料列。 在這些作業中，資料列大小的有效限制為上限的一半。 這是因為原始的資料列和修改過的資料列短期內都必須包含在資料頁面上。  
  
## <a name="user-action"></a>使用者動作  
如果可能的話，請縮減此資料列的大小。  
  
如果您認為問題是因為資料列的就地更新所造成，您必須使用多個步驟變更資料表。 建立新的資料表，然後將資料傳送到新的資料表內。 然後刪除原始資料表並將新的資料表重新命名，或是截斷原始資料表、修改原始資料表內的資料列，然後將資料移回其中。  
  
