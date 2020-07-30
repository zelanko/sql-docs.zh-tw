---
title: MSSQL_ENG020572 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020572 error
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2512642e023b45a3bc5a420d90775b33dae5bd5b
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363258"
---
# <a name="mssql_eng020572"></a>MSSQL_ENG020572
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|20572|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|訂閱者 '%s' 訂閱的發行項 '%s' (在發行集 '%s' 中)，已經在驗證失敗後重新初始化。|  
  
## <a name="explanation"></a>說明  
 訂閱者端的資料是依據發行者端的資料進行驗證，而資料不相符，因此驗證失敗。 在指定應該執行驗證時，您選取了如果驗證失敗則訂閱應該重新初始化的選項。 重新初始化訂閱涉及了在訂閱者端套用新的快照集。 如需驗證的相關資訊，請參閱 [Validate Replicated Data](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  
  
## <a name="user-action"></a>使用者動作  
 在訂閱者端套用新快照集之後，發行者端和訂閱者端的資料將會相符。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
