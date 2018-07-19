---
title: CURRENT_REQUEST_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CURRENT_REQUEST_ID_TSQL
- CURRENT_REQUEST_ID
dev_langs:
- TSQL
helpviewer_keywords:
- CURRENT_REQUEST_ID
ms.assetid: 949f6e5f-bf5f-49d6-a763-c443d1d51fe2
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2761901c3b04b0b38fc92f08238a968d8efb6786
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37791809"
---
# <a name="currentrequestid-transact-sql"></a>CURRENT_REQUEST_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

此函數會傳回目前工作階段中的目前要求識別碼。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CURRENT_REQUEST_ID()  
```  
  
## <a name="return-types"></a>傳回類型
**smallint**
  
## <a name="remarks"></a>Remarks  
若要尋找確切目前工作階段的相關資訊，請使用 @@SPID。 如需目前要求的正確資訊，請使用 CURRENT_REQUEST_ID()。
  
## <a name="see-also"></a>另請參閱
[@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)
  
  
