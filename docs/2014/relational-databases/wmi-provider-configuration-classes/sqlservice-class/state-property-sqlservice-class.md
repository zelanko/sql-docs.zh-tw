---
title: State 屬性（SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- State Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cd91cccfdeef2cab9e4fdfae73bc69a996d652fc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85013638"
---
# <a name="state-property-sqlservice-class"></a>State 屬性 (SqlService 類別)
  取得或設定服務的目前狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.State [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定服務狀態的 uint32 值。  
  
 它可以是下列其中一個值。  
  
 1  
 已停止。 服務已停止。  
  
 2  
 開始暫止。 服務正在等候開始。  
  
 3  
 停止暫止。 服務正在等候停止。  
  
 4  
 執行中。 服務正在執行中。  
  
 5  
 繼續暫止。 服務正在等候繼續。  
  
 6  
 暫停暫止。 服務正在等候暫停。  
  
 7  
 已暫停。 服務已暫停。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
