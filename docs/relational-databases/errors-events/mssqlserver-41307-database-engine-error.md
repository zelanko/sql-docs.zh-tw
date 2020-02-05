---
title: MSSQLSERVER_41307 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41307 (Database Engine error)
ms.assetid: 56f56410-b07d-4379-b01c-702c95761070
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e7080c7814fdbff436bbc7e27bb5cba4c2da227e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68043466"
---
# <a name="mssqlserver_41307"></a>MSSQLSERVER_41307
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41307|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|HK_HEKATON_ROW_LIMIT|  
|訊息文字|已超過記憶體最佳化資料表的 *number* 個位元組資料列大小限制。 請簡化資料表定義。|  
  
## <a name="explanation"></a>說明  
記憶體最佳化資料表的資料列大小限制為 8,060 個位元組。 如需詳細資訊，請參閱 [記憶體最佳化資料表中的資料表和資料列大小](~/relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
