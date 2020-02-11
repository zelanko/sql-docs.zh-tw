---
title: srv_willconvert (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_willconvert
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0af2ec4471dc24af0fdb02576adad312ed35069f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62740698"
---
# <a name="srv_willconvert-extended-stored-procedure-api"></a>srv_willconvert (擴充預存程序 API)
    
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 決定 ODS 程式庫中是否提供特定資料類型轉換。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL srv_willconvert (  
int  
srctype  
,  
int  
desttype   
);  
  
```  
  
## <a name="arguments"></a>引數  
 *srctype*  
 表示要轉換之資料的資料類型。 此參數可以是任何擴充預存程序 API 資料類型。  
  
 *desttype*  
 表示轉換來源資料的目標資料類型。 此參數可以是任何擴充預存程序 API 資料類型。  
  
## <a name="returns"></a>傳回值  
 支援資料類型轉換時為 TRUE；不支援資料類型轉換時則為 FALSE。  
  
## <a name="remarks"></a>備註  
 如需每種資料類型的描述，請參閱[資料類型 &#40;擴充預存程序 API&#41;](data-types-extended-stored-procedure-api.md)。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_convert &#40;擴充預存程式 API&#41;](srv-convert-extended-stored-procedure-api.md)  
  
  
