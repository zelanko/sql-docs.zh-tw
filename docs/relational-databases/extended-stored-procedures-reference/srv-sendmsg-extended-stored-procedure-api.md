---
title: srv_sendmsg (擴充預存程序 API) | Microsoft Docs
description: 瞭解擴充預存程式 API 中的 srv_sendmsg，以及它如何將訊息傳送至用戶端。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_sendmsg
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_sendmsg
ms.assetid: efcb50b9-f8ff-4121-bf67-05830171b928
author: rothja
ms.author: jroth
ms.openlocfilehash: 3737b6633710a3831cf8cbcb3801263582369dc7
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248235"
---
# <a name="srv_sendmsg-extended-stored-procedure-api"></a>srv_sendmsg (擴充預存程序 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳送訊息給用戶端。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_sendmsg (  
SRV_PROC *  
srvproc  
,  
int  
msgtype  
,  
DBINT  
msgnum  
,  
DBTINYINT  
class  
,   
DBTINYINT  
state  
,  
DBCHAR *  
rpcname  
,  
int   
rpcnamelen  
,  
DBUSMALLINT  
linenum  
,  
DBCHAR *  
message  
,  
int  
msglen   
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (此案例中為接收語言要求的控制代碼)。 此結構包含了一些資訊，擴充預存程序 API 程式庫會使用這些資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *msgtype*  
 這是 SRV_MSG_INFO 或 SRV_MSG_ERROR (取決於伺服器要傳送參考用訊息還是錯誤訊息而定)。  
  
 *msgnum*  
 這是 4 位元組的訊息編號。  
  
 *class*  
 指定錯誤嚴重性。 嚴重性小於或等於 10 視為參考用訊息。  
  
 *state*  
 提供目前訊息的錯誤狀態編號。 錯誤狀態編號會提供有關錯誤內容的資訊。 有效的狀態編號是從 0 到 255。  
  
 *rpcname*  
 目前不支援。  
  
 *rpcnamelen*  
 目前不支援。  
  
 *linenum*  
 這是此訊息在語言命令批次中所適用的行號。 行號從 1 開始。 如果 *linenum* 不會套用到訊息，請將它設定為 0。  
  
 *message*  
 這是要傳送給用戶端之字元字串的指標。  
  
 *msglen*  
 指定 *message* 的長度 (以位元組為單位)。 如果 *message* 是以 null 結尾，請將 *msglen* 設定為 SRV_NULLTERM。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL  
  
## <a name="remarks"></a>備註  
 這個函數會將錯誤或參考用訊息傳送給用戶端。 將會針對每一個要傳送的訊息呼叫此函數一次。  
  
 在使用 **srv_sendrow** 傳送所有資料列 (如果有的話) 之前或之後，都可以依照任何順序使用 **srv_sendmsg** 將訊息傳送給用戶端。 必須在使用 **srv_senddone** 傳送完成狀態以前將所有訊息 (如果有的話) 傳送給用戶端。  
  
 若要以 Unicode 傳送訊息，請使用 **srv_wsendmsg**，而不是 **srv_sendmsg**。  
  
 如需詳細資訊，請參閱 [Unicode 資料和伺服器字碼頁](../../relational-databases/extended-stored-procedures-programming/unicode-data-and-server-code-pages.md)。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
