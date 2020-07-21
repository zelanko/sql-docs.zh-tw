---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ad3c332e571a0fbeea09d4a22035a2f32d9ba0b0
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551281"
---
# <a name="mssqlserver_511"></a>MSSQLSERVER_511
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|511|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|ROW_TOOBIG|  
|訊息文字|當 %d 大小的資料列大於允許的最大 %d 時，便無法建立它。|  
  
## <a name="explanation"></a>說明  
 您嘗試執行的作業超出資料列大小的上限。 通常資料列大小的上限為 8,060 個位元組。 某些儲存格式包含的負擔可能會減少資料可使用的資料列大小。 例如，當您使用疏鬆資料行時，資料列大小的上限為 8,018 個位元組。 加入或移除資料列的某些作業及變更資料行之資料類型的某些作業需要將資料列重寫到資料頁面，然後移除原始的資料列。 在這些作業中，資料列大小的有效限制為上限的一半。 這是因為原始的資料列和修改過的資料列短期內都必須包含在資料頁面上。  
  
> [!WARNING]  
>  每個非 Null 的 **varchar(max)** 或 **nvarchar(max)** 資料行都需要額外 24 位元組的固定配置，而不利於排序作業期間 8,060 位元組的資料列限制。 因此可能會對資料表中可建立的非 Null **varchar(max)** 或 **nvarchar(max)** 資料行數目建立隱含限制。 建立資料表時 (高於最大資料列大小超過允許上限 8060 位元組所引發的一般警告) 或插入資料時，不會提供任何特殊錯誤。 如此大型的資料列可能會在某些一般作業 (如叢集索引鍵更新) 期間造成錯誤 (如錯誤 512)，或讓使用者直到執行作業前都無法預期多種完整資料行集。  
  
## <a name="user-action"></a>使用者動作  
 如果可能的話，請縮減此資料列的大小。  
  
 如果您認為問題是因為資料列的就地更新所造成，您必須使用多個步驟變更資料表。 建立新的資料表，然後將資料傳送到新的資料表內。 然後刪除原始資料表並將新的資料表重新命名，或是截斷原始資料表、修改原始資料表內的資料列，然後將資料移回其中。  
  
  
