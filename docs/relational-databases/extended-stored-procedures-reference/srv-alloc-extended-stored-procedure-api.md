---
title: srv_alloc (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_alloc
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_alloc
ms.assetid: 91505c59-a273-452f-b71d-5e8205c21863
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0b7f2627c61b96bb0efa5c19886c554268c2cd2f
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030945"
---
# <a name="srvalloc-extended-stored-procedure-api"></a>srv_alloc (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
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
  
## <a name="remarks"></a>Remarks  
 **srv_alloc** 函式相當於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows API **GlobalAlloc** 函式。 一般 Windows API C 執行階段記憶體管理函數可用在擴充預存程序 API 應用程式中。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
  
