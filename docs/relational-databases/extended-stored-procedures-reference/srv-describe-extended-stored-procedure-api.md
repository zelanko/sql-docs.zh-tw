---
title: srv_describe (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_describe
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_describe
ms.assetid: 2115600e-5ce7-4be0-9cd3-a1dd1fab0729
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2f219e283078b39364ac7a6ee6e0c877c3760194
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51031875"
---
# <a name="srvdescribe-extended-stored-procedure-api"></a>srv_describe (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 針對資料列中的特定資料行定義資料行名稱以及來源和目的地資料類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_describe (  
SRV_PROC *  
srvproc  
,  
int  
colnumber  
,  
DBCHAR *  
column_name  
,  
int  
namelen  
,  
DBINT  
desttype  
,  
DBINT  
destlen  
,  
DBINT  
srctype  
,  
DBINT  
srclen  
,  
void *  
srcdata  
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (此案例中為傳送資料列的用戶端)。 此結構包含了擴充預存程序 API 程式庫用來管理應用程式與用戶端之間之通訊和資料的所有資訊。  
  
 *colnumber*  
 目前不支援。 必須依序描述資料行。 所有資料行都必須在呼叫 **srv_sendrow** 之前描述。  
  
 *column_name*  
 指定資料所屬的資料行名稱。 這個參數可以是 NULL，因為資料行不需要有名稱。  
  
 *namelen*  
 指定 *column_name* 的長度 (以位元組為單位)。 如果 *namelen* 是 SRV_NULLTERM，則 *column_name* 必須以 null 結束。  
  
 *desttype*  
 指定目的地資料列資料行的資料類型。 這是傳送給用戶端的資料類型。 即使資料為 NULL 仍然必須指定資料類型。如需詳細資訊，請參閱[資料類型 &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)。  
  
 *destlen*  
 指定傳送給用戶端之資料的長度 (以位元組為單位)。 如果是不允許 null 值的固定長度資料類型，則會忽略 *destlen*。 如果是允許 null 值的可變長度資料類型和固定長度資料類型，*destlen* 會指定目的地資料的可能最大長度。  
  
 *srctype*  
 指定來源資料的資料類型。  
  
 *srclen*  
 指定來源資料的長度 (以位元組為單位)。 固定長度的資料類型會忽略這個值。  
  
 *srcdata*  
 提供特定資料行的來源資料位址。 當呼叫 **srv_sendrow** 時，它會在 *srcdata* 上尋找 *colnumber* 的資料。 因此在呼叫 **srv_sendrow** 之前不應該將它釋放。 在 **srv_sendrow** 的呼叫之間可以使用 **srv_setcoldata** 來變更來源資料位址。 配置給 *srcdata* 的記憶體要等到另一個 **srv_setcoldata** 呼叫取代資料行資料或是呼叫 **srv_senddone** 之後，才能釋放。  
  
 如果 *desttype* 為 SRVDECIMAL 或 SRVNUMERIC，則 *srcdata* 參數必須是 DBNUMERIC 或 DBDECIMAL 結構的指標，而且此結構的有效位數及小數位數欄位已設定為您想要的值。 您可以使用 DEFAULTPRECISION 來指定預設有效位數，並使用 DEFAULTSCALE 來指定預設小數位數。  
  
## <a name="returns"></a>傳回值  
 所描述之資料行的編號。 第一個資料行為資料行 1。 若發生錯誤，就會傳回 0。  
  
## <a name="remarks"></a>Remarks  
 在第一次呼叫 **srv_sendrow** 之前，必須針對資料列中的每一個資料行呼叫 **srv_describe** 函式一次。 資料列的資料行可以依照任何順序來描述。  
  
 若要在傳送完整結果集之前變更資料行資料列中來源資料的位置和長度，請分別使用 **srv_setcoldata** 和 **srv_setcollen**。  
  
 如需資料類型及擴充預存程序 API 資料類型轉換的描述，請參閱[資料類型 &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)。  
  
 如果應用程式內的資料行名稱為 Unicode 格式，您需要將它轉換成伺服器的多位元組字碼頁，然後才能呼叫 **srv_describe**。 如需詳細資訊，請參閱 [Unicode 資料和伺服器字碼頁](../../relational-databases/extended-stored-procedures-programming/unicode-data-and-server-code-pages.md)。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_sendrow &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-sendrow-extended-stored-procedure-api.md)   
 [srv_setutype &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-setutype-extended-stored-procedure-api.md)   
 [srv_setcoldata &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-setcoldata-extended-stored-procedure-api.md)  
  
  
