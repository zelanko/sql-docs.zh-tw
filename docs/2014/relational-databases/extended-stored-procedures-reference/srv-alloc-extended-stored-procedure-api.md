---
title: srv_alloc (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- srv_alloc
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_alloc
ms.assetid: 91505c59-a273-452f-b71d-5e8205c21863
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a5cc264f27814ed5d577dddfae5bc0d2cb81cc34
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236778"
---
# <a name="srvalloc-extended-stored-procedure-api"></a>srv_alloc (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 以動態方式配置記憶體。  
  
## <a name="syntax"></a>語法  
  
```  
  
void * srv_alloc ( DBINT  
size  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *size*  
 指定要配置的位元組數。  
  
## <a name="returns"></a>傳回值  
 新配置空間的指標。 如果無法配置 *size* 個位元組，就會傳回 Null 指標。  
  
## <a name="remarks"></a>備註  
 **srv_alloc** 函式相當於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows API **GlobalAlloc** 函式。 一般 Windows API C 執行階段記憶體管理函數可用在擴充預存程序 API 應用程式中。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
  
