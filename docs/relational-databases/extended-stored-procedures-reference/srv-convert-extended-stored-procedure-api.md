---
title: srv_convert (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_convert
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_convert
ms.assetid: 216b4a31-786e-4361-8a33-e5f6e9790f90
caps.latest.revision: 33
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4812174e3a736a05475ceaf901bc86bf7949436d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="srvconvert-extended-stored-procedure-api"></a>srv_convert (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 將資料從某個資料類型變成另一個資料類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_convert (  
SRV_PROC *  
srvproc  
,  
int  
srctype  
,  
void *  
src  
,  
DBINT  
srclen  
,  
int  
desttype  
,  
void *  
  dest  
,  
DBINT  
destlen  
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼。 此結構包含了擴充預存程序 API 用來管理應用程式與用戶端之間之通訊和資料的所有控制資訊。 如果提供了 *srvproc* 控制代碼，則當發生錯誤時會將它傳遞給擴充預存程序 API 錯誤處理函式。  
  
 *srctype*  
 指定要轉換之資料的資料類型。 此參數可以是任何擴充預存程序 API 資料類型。  
  
 *src*  
 這是要轉換之資料的指標。 此參數可以是任何擴充預存程序 API 資料類型。  
  
 *srclen*  
 指定要轉換之資料的長度 (以位元組為單位)。 如果 *srclen* 為 0，**srv_convert** 會將 null 值放在目的地變數內。 除非它是 0，否則固定長度的資料類型會忽略這個參數，此時假設來源資料為 NULL。 如果是 SRVCHAR 資料類型的資料，-1 的長度表示字串是以 null 結束。  
  
 *desttype*  
 指定要將來源轉換成那一種資料類型。 此參數可以是任何擴充預存程序 API 資料類型。  
  
 *dest*  
 這是接收已轉換之資料的目的地變數的指標。 如果此指標為 NULL，**srv_convert** 會呼叫使用者提供的錯誤處理常式 (如果有的話)，並傳回 -1。  
  
 如果 *desttype* 為 SRVDECIMAL 或 SRVNUMERIC，則 *dest* 參數必須是 DBNUMERIC 或 DBDECIMAL 結構的指標，而且此結構的有效位數及小數位數欄位已設定為您想要的值。 您可以使用 DEFAULTPRECISION 來指定預設有效位數，並使用 DEFAULTSCALE 來指定預設小數位數。  
  
 *destlen*  
 指定目的地變數的長度 (以位元組為單位)。 固定長度的資料類型會忽略這個參數。 如果是 SRVCHAR 類型的目的地變數，*destlen* 的值必須是目的地緩衝區空間的總長度。 如果 SRVCHAR 或 SRVBINARY 類型的目的地變數長度為 -1，這表示可用的空間很充足。 如果是 *srvchar* 類型的目的地變數，則 -1 的長度會造成字元字串以 null 結束。  
  
## <a name="returns"></a>傳回值  
 如果資料類型轉換成功，則為轉換之資料的長度 (以位元組為單位)。 當 **srv_convert** 遇到所不支援的轉換要求時，它會呼叫開發人員提供的錯誤處理常式 (如果有的話)、設定全域錯誤號碼，並傳回 -1。  
  
## <a name="remarks"></a>Remarks  
 **srv_willconvert** 函式會決定是否允許特定的轉換。  
  
 轉換成近似的數值資料類型 SRVFLT4 或 SRVFLT8 可能會造成部分有效位數遺失。 從近似的數值資料類型 SRVFLT4 或 SRVFLT8 轉換成 SRVCHAR 或 SRVTEXT 可能會造成部分有效位數遺失。  
  
 轉換成 SRVFLT*x*、SRVINT*x*、SRVMONEY、SRVMONEY4、SRVDECIMAL 或 SRVNUMERIC 可能會造成溢位 (如果此數字大於目的地的最大值) 或是反向溢位 (如果此數字小於目的地的最小值)。 如果轉換成 SRVCHAR 或 SRVTEXT 時發生溢位，結果值的第一個字元會包含星號 (*) 來指示錯誤。  
  
 將 SRVCHAR 轉換成 SRVBINARY 時，**srv_convert** 會將 SRVCHAR 解譯為十六進位，不論字串是否包含前置 0。 將 SRVBINARY 轉換成 SRVCHAR 時，**srv_convert** 會建立一個十六進位字串，而不含前置 0。 在所有其他狀況下，與 SRVBINARY 資料類型之間的來回轉換純粹是位元複製。  
  
 在某些情況下，將資料類型轉換成它本身會很有幫助。 例如，將 SRVCHAR 轉換成 SRVCHAR 並將 *destlen* 設定為 -1 會將 null 結束字元新增至字串。  
  
 如需資料類型及擴充預存程序 API 資料類型轉換的描述，請參閱[資料類型 &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)。  
  
 **srv_convert** 函式失敗的原因有好幾個：  
  
-   無法使用要求的轉換。  
  
-   轉換導致目的地變數中的有效位數遭到截斷、溢位或遺失。  
  
-   將字元字串轉換成數值資料類型時所發生的語法錯誤。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_setutype &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-setutype-extended-stored-procedure-api.md)   
 [srv_willconvert &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-willconvert-extended-stored-procedure-api.md)  
  
  
