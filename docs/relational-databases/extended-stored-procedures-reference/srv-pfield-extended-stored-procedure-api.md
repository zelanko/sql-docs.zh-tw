---
title: srv_pfield (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_pfield
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfield
ms.assetid: a61e4c1f-e65b-48ea-a7d1-3e1544af389d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 822e8608939d7fb3dbef6872ec92da37e7621865
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62936773"
---
# <a name="srvpfield-extended-stored-procedure-api"></a>srv_pfield (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回資料庫連接的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBCHAR * srv_pfield (  
SRV_PROC *  
srvproc  
,  
int   
field  
,  
int *  
len  
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 識別資料庫連接的指標。  
  
 *field*  
 指定連接上要傳回的資料。  
  
|ReplTest1|傳回值|  
|-----------|-------------|  
|SRV_APPLNAME|用戶端建立連接時所提供的應用程式名稱。|  
|SRV_BCPFLAG|如果用戶端正在準備進行大量複製作業，則為 TRUE 的旗標，否則為 FALSE 的旗標。|  
|SRV_CLIB|讓用戶端與伺服器溝通之程式庫的名稱。|  
|SRV_CPID|用戶端來源電腦上的用戶端處理序識別碼。|  
|SRV_HOST|用戶端建立連接時所提供的用戶端電腦名稱。|  
|SRV_LIBVERS|用戶端程式庫的版本。|  
|SRV_LSECURE|旗標。 如果連接使用整合安全性登入，則為 TRUE。|  
|SRV_NETWORK_MODULE|連接使用的網路程式庫 DLL 名稱。|  
|SRV_NETWORK_VERSION|連接使用的網路程式庫 DLL 版本。|  
|SRV_NETWORK_CONNECTION|傳遞到用於目前 *srvproc* 連線之網路程式庫 DLL 的連接字串。|  
|SRV_PIPEHANDLE|包含連接用戶端之管道控制碼的字串，如果用戶端連接到不使用具名管道的網路，則為 NULL。 若要搭配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用此控制碼當做有效的管道控制碼，請將此字串轉換為整數。|  
|SRV_RMTSERVER|用戶端處理序所登入的伺服器。 如果登入來自用戶端，此值為空字串。|  
|SRV_ROWSENT|*srvproc* 已經針對目前結果集所傳送的資料列數目。|  
|SRV_SPID|*srvproc* 的伺服器執行緒識別碼。 對於擴充預存程序，此值與 **sys.sysprocesses** 的 **kpid** 資料行相同，而且可以隨時變更。|  
|SRV_SPROC_CODEPAGE|伺服器用於解譯多位元組資料的字碼頁。|  
|SRV_STATUS|*srvproc* 的目前狀態：執行中或已關閉|  
|SRV_TYPE|*srvproc* 的連線類型。 如果傳回伺服器，*srvproc* 來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 如果傳回用戶端，*srvproc* 來自 DB 程式庫或 ODBC 用戶端。|  
|SRV_USER|連接的使用者名稱。|  
|||  
  
 *len*  
 這是指向 **int** 變數的指標，該變數含有傳回 *field* 值的長度。 如果 *len* 是 NULL，則不會傳回字串的長度。  
  
## <a name="returns"></a>傳回值  
 以 Null 結束的字串指標，其中包含指定之欄位在 SRV_PROC 結構中的目前值。 如果欄位是空的，則會傳回空字串的有效指標，而且 *len* 包含 0。 如果欄位不明，會傳回 NULL，而且 *len* 包含值 -1。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱[資訊安全開發人員中心](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
  
